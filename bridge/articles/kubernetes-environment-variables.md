---
title: 将 Kubernetes 服务环境变量用于服务间的通信
ms.date: 02/12/2021
description: 了解如何将 Kubernetes 服务环境变量与 Bridge to Kubernetes 结合使用，以便在 Kubernetes 群集中以非提升用户身份启用服务间的通信
ms.author: ghogen
author: ghogen
manager: jmartens
ms.topic: conceptual
ms.technology: bridge
ms.custom: contperf-fy22q1
ms.openlocfilehash: 5094bbea491fb1f40c281e35ae520b17e08c9d78
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832954"
---
# <a name="kubernetes-service-environment-variables"></a>Kubernetes 服务环境变量

与同一 Kubernetes 群集中的另一个服务（例如与 HTTP 请求）通信时，通常会在请求的 URL 中使用硬编码的服务名称，但在使用 Bridge to Kubernetes 的某些情况下是行不通的。 本文介绍了如何使用 Kubernetes 服务环境变量指定连接 URL。

## <a name="avoid-redirection-failures"></a>避免重定向失败

通过修改主机名称解析以将网络流量重定向到其自己的服务版本，Bridge to Kubernetes 可以重排流量。 在大多数情况下重定向都有效，但是在 Bridge to Kubernetes 进程权限受限时会失败，例如，从非提升用户帐户发出请求或者使用 VS Code Remote SSH 时。 原因是，为了启用重定向服务的名称解析，Bridge to Kubernetes 需要更改主机文件，但 Bridge to Kubernetes 以非提升用户帐户运行时不可行。 若要解决此问题，可以编写代码以使用 Kubernetes 服务环境变量，而不是使用硬编码的服务名称。

## <a name="environment-variables-table"></a>环境变量表

下表介绍了群集中任意服务可用的 Kubernetes 服务环境变量，例如端口上使用 TCP 协议的服务。 servicename 是服务的名称（已转换成大写，并将连字符转换为下划线），例如，名为 web-api 的服务生成名为 WEB_API_SERVICE_HOST 的环境变量。

| 名称 | 示例 | 说明 |
| - | - | - |
| servicename_SERVICE_HOST | 10.0.0.11 | 服务主机的名称 |
| servicename_SERVICE_PORT | 6379 | 服务的端口 |
| servicename_PORT | tcp://10.0.0.11:6379 | 包含协议、IP 地址和端口的 URL。 |
| servicename\_PORT_portnumber_protocol | tcp://10.0.0.11:6379 | 包含协议、IP 地址和端口的 URL。 |
| servicename\_PORT_portnumber_protocol_PROTO| tcp | 协议标识符。 |
| servicename\_PORT_portnumber_protocol_PORT | 6379 | TCP 的端口号。 |
| servicename\_PORT_portnumber_protocol_ADDR | 10.0.0.11 | TCP 的 IP 地址。 |

因此，如果服务名为 web-api，则变量为 WEB_API_SERVICE_HOST 和 WEB_API_SERVICE_PORT 等。 [Kubernetes 文档](https://kubernetes.io/docs/concepts/services-networking/service/#environment-variables)中介绍了 Kubernetes 创建的默认环境变量。 有关支持的协议的信息，请参阅[支持的协议](https://kubernetes.io/docs/concepts/services-networking/service/#protocol-support)。

## <a name="environment-variables-in-source-code"></a>源代码中的环境变量

若要启用服务以在 Bridge to Kubernetes 中运行（不具有提升权限），请将任意硬编码引用替换为具有环境变量的主机名。 以下示例介绍了用 C# 编写的名为 mywebapi 的 .NET 服务中的这种情况：

```csharp
    using var client = new HttpClient();
    var host = Environment.GetEnvironmentVariable("MYWEBAPI_SERVICE_HOST");
    var port = Environment.GetEnvironmentVariable("MYWEBAPI_SERVICE_PORT");
    var request = new HttpRequestMessage();
    request.RequestUri = new Uri($"http://{host}:{port}/api/data");
    var response = await client.SendAsync(request);
```

Node.js 中的示例如下所示：

```js
    server.get("/api/data", function (req, res) {
        var options = {
            host: process.env.MYWEBAPI_SERVICE_HOST,
            port: process.env.MYWEBAPI_SERVICE_PORT,
            path: '/api/data',
            method: 'GET'
        };
        var req = http.request(options, function(response) {
            res.setHeader('Content-Type', 'application/json');
            var responseString = '';
            //another chunk of data has been received, so append it to `responseString`
            response.on('data', function (chunk) {
                responseString += chunk;
            });
            response.on('end', function () {
                res.send(responseString);
            });
        });

        req.on('error', function(e) {
            console.log('problem with request: ' + e.message);
          });

          req.end();
    });
```

若要更新代码以使用环境变量，请查找任何出现的主机名，并更新为使用从环境变量 servicename_SERVICE_HOST 获取的值。

即使在调用服务时通常不指定目标服务使用的端口，仍将需要使用 servicename_SERVICE_PORT environment 变量。 通过指定端口，可以让 Bridge to Kubernetes 在开发计算机上的特定端口不可用时避免冲突。 无需更改服务对其进行侦听以正常工作的端口：只需要确保在服务调用其它服务时，它使用 servicename_SERVICE_HOST 和 servicename_SERVICE_PORT 环境变量进行调用。

在群集中的其他位置重复使用相同代码也是可行的，因为这些环境变量可用于群集中的每个 pod。 如果在 Kubernetes 群集之外重复使用相同代码，则必须设置等效环境变量，或为新平台或托管服务适当地修改代码。

## <a name="set-vs-code-to-use-kubernetes-service-environment-variables"></a>设置 VS Code 以使用 Kubernetes 服务环境变量

如果正在通过远程计算机使用 VS Code 或以普通用户身份运行 VS Code，还需要配置 VS Code 以使用 Kubernetes 服务环境变量。 打开 tasks.json，找到具有标签 `bridge-to-kubernetes.service` 的任务，并添加具有值 `true` 的属性 `usekubernetesServiceEnvironmentVariables`，如以下代码所示：

```json
    "tasks": [
        {
            "label": "bridge-to-kubernetes.service",
            "type": "bridge-to-kubernetes.service",
            "service": "bikes",
            "ports": [
                3000
            ],
            "useKubernetesServiceEnvironmentVariables": true
        }
    ]
```

只有当以普通用户身份运行 VS Code 或使用远程会话时才需要该设置，但是如果你已按本文所述修改了代码，则无需设置该属性。

## <a name="next-steps"></a>后续步骤

若要详细了解 Bridge to Kubernetes 配置，请参阅[如何配置 Bridge to Kubernetes](configure-bridge-to-kubernetes.md)。
