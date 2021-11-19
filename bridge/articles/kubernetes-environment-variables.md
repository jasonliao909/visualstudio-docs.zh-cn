---
title: 使用 Kubernetes 服务环境变量进行服务间通信
ms.date: 02/12/2021
description: 了解如何将 Kubernetes service 环境变量与 Bridge 结合使用，以便在 Kubernetes 群集中以非提升用户身份启用服务到服务通信
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

当你与同一 Kubernetes 群集中的其他服务进行通信（例如，使用 HTTP 请求）时，通常会在请求的 URL 中使用硬编码的服务名称，但这不会在某些使用 Bridge 到 Kubernetes 的情况下工作。 本文介绍如何使用 Kubernetes 服务环境变量指定连接 URL。

## <a name="avoid-redirection-failures"></a>避免重定向失败

通过修改主机名解析将网络流量重定向到其自己的服务版本，桥接 Kubernetes 来重置流量。 重定向在大多数情况下都有效，但在桥到 Kubernetes 进程的权限受到限制的情况下，例如，请求来自非提升的用户帐户或使用 VS Code 远程 SSH 时失败。 这是因为，为了启用重定向服务的名称解析，桥接 Kubernetes 需要修改 hosts 文件，但当桥到 Kubernetes 从非提升用户帐户运行时，这是不可能的。 若要解决此问题，可以编写代码以使用 Kubernetes 服务环境变量，而不是使用硬编码的服务名称。

## <a name="environment-variables-table"></a>环境变量表

下表显示了群集中的任何服务提供的 Kubernetes 服务环境变量，以及在端口上使用 TCP 协议的示例服务。 *Servicename* 是服务的名称，已转换为大写，并将连字符转换为下划线，因此，名为 web api 的服务将生成名为 WEB_API_SERVICE_HOST 的环境变量。

| 名称 | 示例 | 说明 |
| - | - | - |
| *servicename* _SERVICE_HOST | 10.0.0.11 | 服务主机的名称 |
| *servicename* _SERVICE_PORT | 6379 | 服务的端口 |
| *servicename* _PORT | tcp://10.0.0.11:6379 | URL，其中包含协议、IP 地址和端口。 |
| *servicename* \_PORT_ *portnumber* _ *协议* | tcp://10.0.0.11:6379 | URL，其中包含协议、IP 地址和端口。 |
| *servicename* \_PORT_ *portnumber* _ *协议* _PROTO| tcp | 协议标识符。 |
| *servicename* \_PORT_ *portnumber* _ *协议* _PORT | 6379 | TCP 的端口号。 |
| *servicename* \_PORT_ *portnumber* _ *协议* _ADDR | 10.0.0.11 | TCP 的 IP 地址。 |

因此，如果服务命名为 web api，则变量 WEB_API_SERVICE_HOST 和 WEB_API_SERVICE_PORT 等。 Kubernetes 创建的默认环境变量在 [Kubernetes 文档](https://kubernetes.io/docs/concepts/services-networking/service/#environment-variables)中进行了介绍。 有关支持的协议的信息，请参阅 [支持的协议](https://kubernetes.io/docs/concepts/services-networking/service/#protocol-support)。

## <a name="environment-variables-in-source-code"></a>源代码中的环境变量

若要使服务能够在没有提升权限的情况下在 Kubernetes 中运行，请将对主机名的任何硬编码引用替换为环境变量。 下面的示例在名为 mywebapi 的 .NET 服务中显示此内容，以 c # 编写：

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

若要将代码更新为使用环境变量，请查找主机名和 update 的任何匹配项，以使用从环境变量 *servicename* _SERVICE_HOST 获取的值。

即使在调用该服务时，通常不指定目标服务使用的端口，也需要使用 *servicename* _SERVICE_PORT 环境变量。 如果指定端口，则允许桥到 Kubernetes，以避免当特定端口在开发计算机上不可用时所发生的冲突。 你不需要更改服务侦听的端口以使其正常工作：只需确保当你的服务调用其他服务时，它将同时使用 *servicename* _SERVICE_HOST 和 *servicename* _SERVICE_PORT 环境变量调用它们。

如果在群集中的其他位置重复使用相同的代码，就可以这样做，因为这些环境变量可在群集中的每个 pod 中使用。 如果在 Kubernetes 群集之外重复使用相同的代码，则必须设置等效的环境变量，或为新平台或托管服务适当地修改代码。

## <a name="set-vs-code-to-use-kubernetes-service-environment-variables"></a>将 VS Code 设置为使用 Kubernetes 服务环境变量

如果在远程计算机上使用 VS Code 或以普通用户身份运行 VS Code，则还需要将 VS Code 配置为使用 Kubernetes 服务环境变量。 打开 "任务 json"，查找标签为 "" 的任务， `bridge-to-kubernetes.service` 并添加 `usekubernetesServiceEnvironmentVariables` 具有值的属性 `true` ，如以下代码所示：

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

仅当你以普通用户的身份运行 VS Code 时，或者如果你正在使用远程会话，但如果你修改了代码（如本文所述），则设置此属性不会造成任何伤害。

## <a name="next-steps"></a>后续步骤

若要详细了解 [如何将桥配置为 Kubernetes](configure-bridge-to-kubernetes.md)，请参阅 Kubernetes 配置的详细信息。
