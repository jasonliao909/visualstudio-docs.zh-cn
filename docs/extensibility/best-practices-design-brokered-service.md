---
title: 设计中转服务的最佳方案
description: 设计、演变和实现中转服务的最佳方案。
monikerRange: '>= vs-2019'
ms.custom: SEO-VS-2020
ms.date: 01/07/2022
ms.topic: conceptual
helpviewer_keywords:
- brokered services, providing
ms.assetid: e186883e-9390-4dc0-9f21-62662a16df11
author: aarnott
ms.author: andarno
manager: ansonh
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: efb1d0fa3b65237e62bbd1824406de65dab67d31
ms.sourcegitcommit: 169b7b66d13b7e3c86097b42206dd33389cd9166
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2022
ms.locfileid: "138153489"
---
# <a name="best-practices-for-designing-a-brokered-service"></a>设计中转服务的最佳方案

遵循为 StreamJsonRpc [的 RPC 接口](https://github.com/microsoft/vs-streamjsonrpc/blob/master/doc/dynamicproxy.md) 记录常规指南和限制。

此外，以下准则适用于中转服务。

## <a name="method-signatures"></a>方法签名

所有方法都应采用 参数 <xref:System.Threading.CancellationToken> 作为最后一个参数。
此参数 *通常不应* 是可选参数，因此调用方不太可能意外省略参数。
即使方法的 <xref:System.Threading.CancellationToken> 实现应该很简单，提供 也允许客户端在将请求传输到服务器之前取消自己的请求。
它还允许服务器的实现发展为成本更高，而无需更新 方法，以在以后添加取消作为选项。

请考虑 *避免* RPC 接口上同一方法的多个重载。
虽然重载解析通常 (并且应编写测试来验证它是否执行) ，但它依赖于尝试基于每个重载的参数类型反化参数，从而导致第一次引发异常作为选择重载的常规部分。
由于我们希望最大程度地减少成功路径中引发的第一机会异常数，因此最好只具有一个给定名称的方法。

## <a name="parameter-and-return-types"></a>参数和返回类型

请记住，通过 RPC 交换的所有参数和返回值 *都只是数据*。
它们全部序列化，并通过线路发送。
在这些数据类型上定义的任何方法仅对该数据的本地副本进行操作，并且无法与生成它的 RPC 服务通信。
此序列化行为的唯一例外是 StreamJsonRpc 支持的特殊类型。[](https://github.com/microsoft/vs-streamjsonrpc/blob/main/doc/exotic_types.md)

请考虑使用 [`ValueTask<T>`](xref:System.Threading.Tasks.ValueTask%601) over [`Task<T>`](xref:System.Threading.Tasks.Task%601) 作为方法的返回类型，因为 [`ValueTask<T>`](xref:System.Threading.Tasks.ValueTask%601) 产生的分配更少。
例如，使用非泛型 (， <xref:System.Threading.Tasks.Task> <xref:System.Threading.Tasks.ValueTask> <xref:System.Threading.Tasks.ValueTask>) 不太重要，但仍可能更可取。
请注意该 API 上 [`ValueTask<T>`](xref:System.Threading.Tasks.ValueTask%601) 介绍的 对 的使用限制。 此[博客](https://devblogs.microsoft.com/dotnet/understanding-the-whys-whats-and-whens-of-valuetask/)[文章和视频](/shows/on-net/understanding-how-to-use-task-and-valuetask)还有助于确定使用哪种类型。

## <a name="custom-data-types"></a>自定义数据类型

请考虑将所有数据类型都定义为不可变，这样无需复制即可跨进程更安全地共享数据，并且有助于向使用者强调，他们无法在不放置另一个 RPC 的情况下更改为响应查询而接收的数据。

使用 时，将 `class` `struct` <xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor.Formatters.UTF8?displayProperty=nameWithType>数据类型定义为 而不是 ，这样可以避免在使用 Newtonsoft.Json 时 (重复) 的开销。
如果使用 时 *不会发生* 装箱， <xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor.Formatters.MessagePack?displayProperty=nameWithType> 因此，如果已提交到该格式化程序，则结构可能是合适的选项。

请考虑在<xref:System.IEquatable%601>数据类型上<xref:System.Object.GetHashCode><xref:System.Object.Equals(System.Object)>实现和重写 和 方法，使客户端能够有效地存储、比较和重用接收的数据，因为它是否等于在另一时间接收的数据。

使用 支持 <xref:Microsoft.VisualStudio.RpcContracts.JsonConverters.DiscriminatedTypeJsonConverter%601> 使用 JSON 序列化多态类型。

### <a name="collections"></a>集合

在 RPC 方法签名中使用只读集合接口 (<xref:System.Collections.Generic.IReadOnlyList%601> <xref:System.Collections.Generic.List%601> `T[]` 例如) 而不是具体类型（例如 (）或) ，这允许更高效的反序列化。

避免<xref:System.Collections.Generic.IEnumerable%601>。
它缺少属性 `Count` 会导致代码效率低下，并意味着可能后期生成数据，这不适用于 RPC 方案。
请 <xref:System.Collections.Generic.IReadOnlyCollection%601> 改为对无序集合或 <xref:System.Collections.Generic.IReadOnlyList%601> 有序集合使用 。

以 <xref:System.Collections.Generic.IAsyncEnumerable%601> 为例。
任何其他集合类型或 <xref:System.Collections.Generic.IEnumerable%601> 将导致在一条消息中发送整个集合。
使用 <xref:System.Collections.Generic.IAsyncEnumerable%601> 允许小型初始消息，为接收方提供从集合获取尽可能多的项（以异步方式枚举）的方式。
[详细了解此新模式](https://github.com/microsoft/vs-streamjsonrpc/blob/master/doc/asyncenumerable.md)。

## <a name="observer-pattern"></a>观察者模式

请考虑 [在界面中使用](/dotnet/standard/events/observer-design-pattern) 观察者设计模式。
这是客户端订阅数据的一种简单方法，无需存在许多适用于下一部分所述的传统事件模型的错误。

观察器模式可能很简单：

```cs
Task<IDisposable> SubscribeAsync(IObserver<YourDataType> observer);
```

上面<xref:System.IDisposable>使用的 <xref:System.IObserver%601> 和 类型是 StreamJsonRpc 中的两种处理类型，因此它们获得特殊封送行为，而不是序列化为简单数据。[](https://github.com/microsoft/vs-streamjsonrpc/blob/main/doc/exotic_types.md)

## <a name="events"></a>事件

由于多种原因，事件在 RPC 上可能会出现问题，建议改为使用上述观察者模式。

请记住，当服务和客户端在单独的进程中时，服务无法查看客户端附加的事件处理程序数。
<xref:StreamJsonRpc.JsonRpc> 将始终只附加一个负责将事件传播到客户端的处理程序。
客户端可能在远端附加了零个或多个处理程序。

大多数 RPC 客户端在首次连接时不会连接事件处理程序。
避免引发第一个事件，直到客户端在接口上调用"Subscribe\*"方法以指示对接收事件的兴趣和就绪情况。

如果事件指示状态 (（例如，添加到集合) 的新项）的增量，请考虑引发所有过去的事件，或描述所有当前数据，就像客户端订阅以帮助它们"同步"，而事件处理代码一样。

如果客户端可能想要表示对一部分数据或通知感兴趣，请考虑接受上述"订阅\*"方法的额外参数，以减少转发这些通知所需的网络流量和 CPU。

如果还公开事件以接收更改通知，或者主动阻止客户端将事件与 事件结合使用，请考虑不提供返回当前值的方法。
订阅数据事件并调用方法获取当前值的客户端将针对该值的更改进行竞争，并缺少更改事件或不知道如何将一个线程上的更改事件与另一个线程上获取的值进行协调。
此关注点对于任何接口都是一般性的，不仅仅是在 RPC 上。

## <a name="naming-conventions"></a>命名约定

- `Service`在 RPC 接口上使用 后缀和简单`I`前缀。
- 请勿对 SDK 中的 `Service` 类使用 后缀。 库或 RPC 包装器应该使用准确描述其功能的名称，避免使用术语"服务"。
- 避免在接口或成员名称中使用术语"remote"。 请记住，中转服务在本地方案中的适用情况与远程方案一样多。

## <a name="version-compatibility-concerns"></a>版本兼容性问题

我们希望向其他扩展公开或通过 Live Share 公开的任何给定中转服务向前和向后兼容，这意味着，我们假设客户端可能比服务旧或新，并且功能应大致等于两个适用版本中较小版本的客户端。

首先，让我们回顾一下中断性变更术语：

- **二进制中断性** 变更：一种 API 更改，会导致针对以前版本的程序集编译的其他托管代码在运行时无法绑定到新代码。 示例包括：
  - 更改现有公共成员签名。
  - 重命名公共成员。
  - 删除公共类型。
  - 将抽象成员添加到类型或接口的任何成员。

  但以下不是 *二* 进制中断性变更：
  - 将非抽象成员添加到类或结构。
  - 向现有 (接口实现添加) 非抽象类。

- **协议中断性变更**：某些数据类型或 RPC 方法调用的序列化形式更改，使远程方无法正确反序列化并处理它。 示例包括：
  - 将所需参数添加到 RPC 方法。
  - 从以前保证为非 null 的数据类型中删除成员。
  - 添加一个要求，即方法调用必须置于其他预先存在的操作之前。
  - 添加、删除或更改控制该成员中数据的序列化名称的字段或属性的属性。
  -  (MessagePack) ：更改<xref:System.Runtime.Serialization.DataMemberAttribute.Order?displayProperty=nameWithType>`KeyAttribute`现有成员的属性或整数。

  但 *以下不是协议* 中断性变更：
  - 向数据类型添加可选成员。
  - 将成员添加到 RPC 接口。
  - 向现有方法添加可选参数。
  - 将表示整数或 float 的参数类型更改为具有更大长度或精度的参数类型 (例如 `int` `long` ，为 或 `float` `double`) 。
  - 重命名参数。 从技术上来说，这是对使用 JSON-RPC <xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor> 命名参数的客户端的中断，但默认情况下使用位置参数的客户端不会受参数名称更改的影响。 这与客户端源代码是否使用命名参数语法无关，参数重命名将是 *源中断性* 变更。

- **行为中断性变更**：对中转服务的实现的更改，可添加或更改行为，使旧客户端可能出现故障。 示例包括：
  - 不再初始化以前始终初始化的数据类型的成员。
  - 在以前可能成功完成的条件下引发异常。
  - 返回错误，错误代码与之前返回的错误代码不同。

  但以下不是 *行为* 中断性变更：
  - 引发新的异常类型 (因为所有异常都包装 <xref:StreamJsonRpc.RemoteInvocationException> 在) 。

当需要中断性变更时，可以通过注册和提供新的服务名字对象来安全地进行这些更改。
此名字对象可以共享同一名称，但版本号更高。
如果没有二进制中断 *性* 变更，原始 RPC 接口可能可重复使用。 否则，请定义新服务版本的新接口。
通过继续注册、提供和支持旧版本，避免中断旧客户端。

我们希望避免所有此类中断性变更，但向 RPC 接口添加成员除外。

### <a name="adding-members-to-rpc-interfaces"></a><a name="AddingInterfaceMembers"></a> 将成员添加到 RPC 接口

*不要将* 成员添加到 [RPC](how-to-provide-brokered-service.md#ClientRpcTarget) 客户端回调接口，因为许多客户端可能实现该接口，添加成员会导致在加载这些类型时引发 CLR<xref:System.TypeLoadException>，但不实现新的接口成员。
如果必须添加成员以在 RPC 客户端回调目标上调用，请定义可能派生自原始) 的新接口 (，然后遵循标准过程，以递增版本号来缓冲中转服务，并提供指定了更新的客户端接口类型的描述符。

可以将 *成员* 添加到定义中转服务的 RPC 接口。
这不是协议中断性变更，只是对实现服务的人的二进制中断性变更，但你可能也会更新服务来实现该新成员。
由于[](how-to-consume-brokered-service.md#TestingBrokeredClients)我们的指导是，除了中转服务本身 (之外，任何人都不应实现 RPC 接口，并且测试应该使用模拟框架) ，因此将成员添加到 RPC 接口不应破坏任何人。

这些新成员应具有 xml 文档注释，用于标识哪个服务版本首先添加了该成员。
如果较新的客户端在未实现 方法的较旧服务上调用 方法，该客户端可以捕获 <xref:StreamJsonRpc.RemoteMethodNotFoundException>。 但是，该客户端 (，并且) 预测失败并避免首先调用。
将成员添加到现有服务的最佳方案包括：

- 如果这是服务版本中的第一个更改：在添加成员并声明新描述符时，在服务名字对象上升级次要版本。
- 更新服务以注册和提供新版本以及旧版本。
- 如果有中转服务的客户端，请更新客户端以请求较新版本，如果较新版本作为 null 返回，则回退到请求旧版本。

## <a name="see-also"></a>另请参阅
- [如何提供中转服务](how-to-provide-brokered-service.md)
