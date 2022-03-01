---
title: 如何：使用中转服务
description: 了解如何获取和使用中转服务来访问不同的功能。
monikerRange: '>= vs-2019'
ms.custom: SEO-VS-2020
ms.date: 01/11/2022
ms.topic: how-to
helpviewer_keywords:
- brokered services, consuming
ms.assetid: 2ff7c882-64f5-4545-8622-83bf6199336f
author: aarnott
ms.author: andarno
manager: ansonh
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 2ff3769afa829fc5b5217984e555e1b223e91868
ms.sourcegitcommit: 169b7b66d13b7e3c86097b42206dd33389cd9166
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2022
ms.locfileid: "138153481"
---
# <a name="how-to-consume-a-brokered-service"></a>如何：使用中转服务

本文档介绍与任何中转服务的获取、常规使用和处置相关的所有代码、模式和注意事项。
若要了解如何 *使用* 特定的中转服务，请查看该中转服务的特定文档。

对于本文档中的所有代码，强烈建议激活 c # 的 [可为 null 的引用类型](/dotnet/csharp/nullable-references) 功能。

## <a name="retrieving-an-iservicebroker"></a>检索 IServiceBroker

若要获取中转服务，必须首先具有的 <xref:Microsoft.ServiceHub.Framework.IServiceBroker> 实例。
当代码在 MEF 或 VS 包的上下文中运行时，通常需要全局 service broker。

中转服务本身应使用 <xref:Microsoft.ServiceHub.Framework.IServiceBroker> 在调用其 [服务工厂](xref:Microsoft.VisualStudio.Shell.ServiceBroker.BrokeredServiceFactory) 时分配给它们的。

### <a name="the-global-service-broker"></a>全局 service broker

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 提供了两种方法来获取全局 service broker。

改用 <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GlobalProvider%2A><xref:Microsoft.VisualStudio.Shell.ServiceExtensions.GetServiceAsync%2A> 请求 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.SVsBrokeredServiceContainer> ：

```cs
IBrokeredServiceContainer container = await AsyncServiceProvider.GlobalProvider.GetServiceAsync<SVsBrokeredServiceContainer, IBrokeredServiceContainer>();
IServiceBroker serviceBroker = container.GetFullAccessServiceBroker();
```

从 Visual Studio 2022 开始，在 MEF 激活的扩展中运行的代码可能会导入全局 service broker：

```cs
[Import(typeof(SVsFullAccessServiceBroker))]
IServiceBroker ServiceBroker { get; set; }
```

`typeof`请注意导入属性的参数，此参数是必需的。

针对全局 <xref:Microsoft.ServiceHub.Framework.IServiceBroker> 的每个请求都会生成一个对象的新实例，该实例用作全局中转服务容器的视图。
Service broker 的这个唯一实例允许客户端接收 <xref:Microsoft.ServiceHub.Framework.IServiceBroker.AvailabilityChanged> 客户端使用的唯一事件。
建议扩展中的每个客户端/类使用上述任一方法获取自己的 service broker，而不是获取一个实例并将其共享到整个扩展。
此模式还鼓励安全编码模式，其中，中转服务 *不* 应使用全局 service broker。

> [!Important]
> 的 <xref:Microsoft.ServiceHub.Framework.IServiceBroker> 实现通常不实现 <xref:System.IDisposable> ，但当处理程序存在时 <xref:Microsoft.ServiceHub.Framework.IServiceBroker.AvailabilityChanged> ，不能收集这些对象。
请确保平衡事件处理程序的添加/删除，特别是在进程的生存期内，代码可能会放弃 service broker。

### <a name="context-specific-service-brokers"></a>上下文特定的服务代理

使用适当的 service broker 是中转服务安全模型的重要要求，尤其是在 Live Share 会话的上下文中。

中转服务会自行 <xref:Microsoft.ServiceHub.Framework.IServiceBroker> 激活，应该使用此实例来处理其自身的任何中转服务需求，包括与提供的 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.IBrokeredServiceContainer.Proffer%2A> 服务。
此类代码提供了一个 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.BrokeredServiceFactory> ，用于接收实例化中转服务使用的 service broker。

## <a name="retrieving-a-brokered-service-proxy"></a>检索中转服务代理

通常使用 <xref:Microsoft.ServiceHub.Framework.IServiceBroker.GetProxyAsync%2A> 方法来检索中转服务。

<xref:Microsoft.ServiceHub.Framework.IServiceBroker.GetProxyAsync%2A>方法将需要 <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor> 和服务接口作为泛型类型参数。
你请求的中转服务上的文档应指示获取描述符的位置以及要使用的接口。
对于附带 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的中转服务，使用的接口应显示在描述符的 IntelliSense 文档中。
了解如何在[发现可用中转服务](internals/discover-available-brokered-services.md)中查找中转服务的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 描述符。

```csharp
IServiceBroker broker; // Acquired as described earlier in this topic
IMyService? myService = await broker.GetProxyAsync<IMyService>(serviceDescriptor, cancellationToken);
using (myService as IDisposable)
{
    Assumes.Present(myService); // Throw if service was not available
    await myService.SayHelloAsync();
}
```

与所有中转服务请求一样，以上代码将激活中转服务的新实例。
使用服务后，上面的代码将代理作为执行退出 `using` 块。

> [!IMPORTANT] 
> *如果服务接口不是从 <xref:System.IDisposable> 派生* 的，则必须释放每个检索到的代理。
> 处置非常重要，因为代理通常具有支持它的 i/o 资源，防止其被垃圾回收。
> 处置终止了 i/o，允许对代理进行垃圾回收。
> 将条件转换 <xref:System.IDisposable> 用于进行处置，并为强制转换做好准备，以避免在实际实现 <xref:System.IDisposable> 的代理或代理中出现异常 `null` 。

请确保安装最新的 NuGet [servicehub.host.clr.](https://www.nuget.org/packages/Microsoft.ServiceHub.Analyzers)包，并保持启用 ISBxxxx 分析器规则以帮助防止此类泄漏。

对代理的处置将导致处置专用于该客户端的中转服务。

如果你的代码需要中转服务，并且在服务不可用时无法完成其工作，则在代码拥有用户体验而不是引发异常的情况下，你可能希望向用户显示错误对话框。

### <a name="client-rpc-targets"></a>客户端 RPC 目标

某些中转服务接受或要求客户端 RPC 目标 "回调"。
此类选项或要求应位于该特定中转服务的文档中。
对于 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中转服务，此信息应包含在描述符的 IntelliSense 文档中。

在这种情况下，客户端可能会按如下所示使用 <xref:Microsoft.ServiceHub.Framework.ServiceActivationOptions.ClientRpcTarget?displayProperty=nameWithType> ：

```csharp
IMyService? myService = await broker.GetProxyAsync<IMyService>(
    serviceDescriptor,
    new ServiceActivationOptions
    {
        ClientRpcTarget = new MyCallbackObject(),
    },
    cancellationToken);
```

## <a name="invoking-the-client-proxy"></a>调用客户端代理

请求中转服务的结果是由代理实现的服务接口的实例。
此代理会在每个方向上转发调用和事件，在与直接调用服务时可能会出现的行为有一些重要差异。

### <a name="observer-pattern"></a>观察者模式

如果服务协定采用类型 <xref:System.IObserver%601> 为的参数，则可以在 [如何实现观察程序](/dotnet/standard/events/how-to-implement-an-observer)中了解有关如何构造此类类型的详细信息。

<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>可以使用 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.AsObserver%2A> 扩展方法来改编实现 <xref:System.IObserver%601> 。
反应性框架中的 [system.web](/previous-versions/dotnet/reactive-extensions/hh229899(v=vs.103)) 类是自行实现接口的另一种替代方法。

### <a name="exceptions-thrown-from-the-proxy"></a>代理引发的异常

- <xref:StreamJsonRpc.RemoteInvocationException>对于从中转服务引发的任何异常都应引发。 可以在中 <xref:System.Exception.InnerException%2A> 找到原始异常。
这是远程托管服务的自然行为，因为它是来自 <xref:StreamJsonRpc.JsonRpc> 的行为。
当服务为本地服务时，本地代理以相同方式包装所有异常，以便客户端代码只能有一个适用于本地和远程服务的异常路径。
  - <xref:StreamJsonRpc.RemoteInvocationException.ErrorCode%2A>如果服务文档建议根据你可以对其进行分支的特定条件设置特定代码，请检查属性。
  - 捕获 <xref:StreamJsonRpc.RemoteRpcException> 更广泛的错误，这是的基本类型 <xref:StreamJsonRpc.RemoteInvocationException> 。
- 当与远程服务的连接断开或承载服务的进程崩溃时，预期 <xref:StreamJsonRpc.ConnectionLostException> 会从任何调用中引发。
这主要是在可远程获取服务时要考虑的问题。

## <a name="caching-of-the-proxy"></a>代理 Caching

激活中转服务和关联的代理会有一定的费用，当服务来自远程进程时，尤其如此。
当频繁使用中转服务来保证在多个调用中缓存代理时，可以将代理存储在该类的字段中。
包含类在其 `Dispose` 方法中应该是可释放和处置代理。
请看以下示例：

```csharp
class MyExtension : IDisposable
{
    readonly IServiceBroker serviceBroker;
    IMyService? serviceProxy;

    internal MyExtension(IServiceBroker serviceBroker)
    {
        this.serviceBroker = serviceBroker;
    }

    async Task SayHiAsync(CancellationToken cancellationToken)
    {
        if (this.serviceProxy is null)
        {
            this.serviceProxy = await this.serviceBroker.GetProxyAsync<IMyService>(serviceDescriptor, cancellationToken);
            Assumes.Present(this.serviceProxy);
        }

        await this.serviceProxy.SayHelloAsync();
    }

    public void Dispose()
    {
        (this.serviceProxy as IDisposable)?.Dispose();
    }
}
```

上述代码大致正确，但它并不考虑与 `SayHiAsync` 之间 `Dispose` 的争用情况。
此代码还不考虑 <xref:Microsoft.ServiceHub.Framework.IServiceBroker.AvailabilityChanged> 那些应该会导致以前获取的代理和下次需要代理的获取的事件。

<xref:Microsoft.ServiceHub.Framework.ServiceBrokerClient>类设计用于处理这些争用和失效条件，以帮助确保自己的代码简单。
请考虑此已更新的示例，该示例使用此帮助器类来缓存代理：

```csharp
class MyExtension : IDisposable
{
    readonly ServiceBrokerClient serviceBrokerClient;

    internal MyExtension(IServiceBroker serviceBroker)
    {
        this.serviceBrokerClient = new ServiceBrokerClient(serviceBroker);
    }

    async Task SayHiAsync(CancellationToken cancellationToken)
    {
        using var rental = await this.serviceBrokerClient.GetProxyAsync<IMyService>(descriptor, cancellationToken);
        Assumes.Present(rental.Proxy); // Throw if service is not available
        IMyService myService = rental.Proxy;
        await myService.SayHelloAsync();
    }

    public void Dispose()
    {
        // Disposing the ServiceBrokerClient will dispose of all proxies
        // when their rentals are released.
        this.serviceBrokerClient.Dispose();
    }
}
```

上述代码仍负责处置 <xref:Microsoft.ServiceHub.Framework.ServiceBrokerClient> 和每个代理租用。
处理和使用代理之间的争用条件是由 <xref:Microsoft.ServiceHub.Framework.ServiceBrokerClient> 对象处理的，该对象会在其自身处置时处置每个缓存的代理，或在该代理的最后一租赁发布后（以最后一个为准）。

### <a name="important-caveats-regarding-the-servicebrokerclient"></a>有关 `ServiceBrokerClient`

- <xref:Microsoft.ServiceHub.Framework.ServiceBrokerClient> 仅基于 <xref:Microsoft.ServiceHub.Framework.ServiceMoniker> 唯一索引缓存的代理。
如果传入 <xref:Microsoft.ServiceHub.Framework.ServiceActivationOptions> 了并且缓存的代理已可用，则将返回缓存的代理而不使用 <xref:Microsoft.ServiceHub.Framework.ServiceActivationOptions> ，这会导致服务产生意外行为。
请考虑在这种情况下直接使用 <xref:Microsoft.ServiceHub.Framework.IServiceBroker> 。

- 不要在字段中存储从 <xref:Microsoft.ServiceHub.Framework.ServiceBrokerClient.GetProxyAsync%2A?displayProperty=nameWithType> 获取的 <xref:Microsoft.ServiceHub.Framework.ServiceBrokerClient.Rental%601> 。
代理已缓存在一个方法 <xref:Microsoft.ServiceHub.Framework.ServiceBrokerClient> 的范围之外。
如果需要更好地控制代理的生存期（特别是由于 <xref:Microsoft.ServiceHub.Framework.IServiceBroker.AvailabilityChanged> 事件而获取），请直接使用 <xref:Microsoft.ServiceHub.Framework.IServiceBroker> 并将服务代理存储在字段中。

- 创建并存储 <xref:Microsoft.ServiceHub.Framework.ServiceBrokerClient> 到字段而不是局部变量。 如果在方法中创建并将其用作本地变量，则它不会直接使用 <xref:Microsoft.ServiceHub.Framework.IServiceBroker> 添加任何值，但现在必须释放客户端和租赁)  (两个对象，而不是 (服务) 。

### <a name="choosing-between-iservicebroker-and-servicebrokerclient"></a>在 IServiceBroker 和 ServiceBrokerClient 之间进行选择

两者都是用户友好的，默认值应该是 <xref:Microsoft.ServiceHub.Framework.IServiceBroker> 。

类别| <xref:Microsoft.ServiceHub.Framework.IServiceBroker> | <xref:Microsoft.ServiceHub.Framework.ServiceBrokerClient>
--|--|--
用户友好|是|是
需要处置|否|是
管理代理的生存期|不是。 所有者必须在使用代理时处置代理。|是的，只要它们有效，它们将保持活动状态并重复使用。
适用于无状态服务|是|是
适用于有状态服务|是|否
在将事件处理程序添加到代理时适用|是|否
旧代理失效时要通知的事件| <xref:Microsoft.ServiceHub.Framework.IServiceBroker.AvailabilityChanged> | <xref:Microsoft.ServiceHub.Framework.ServiceBrokerClient.Invalidated>

<xref:Microsoft.ServiceHub.Framework.ServiceBrokerClient> 为您提供了一种便捷的方法，使您能够快速而频繁地重复使用代理，在这种情况下，您不会注意到，在顶级操作之间的下层服务是否已更改。

但如果你确实关心这些问题并想要自行管理代理的生存期，或者需要事件处理程序 (这意味着你需要管理代理) 的生存期，则应使用 <xref:Microsoft.ServiceHub.Framework.IServiceBroker> 。

## <a name="resilience-to-service-disruptions"></a>服务中断的复原能力

中转服务有几种可能的服务中断：

- [服务不可用](#ServiceActivationFailures)。
- 与以前获取的中转服务的 [连接已断开](#DroppedConnections) 。
- [服务可用性的更改](#ServiceAvailabilityChanges)应在以后请求该服务时进行。

### <a name="brokered-service-activation-failures"></a><a name="ServiceActivationFailures"></a> 中转服务激活失败

如果可用的服务请求可满足中转服务请求，但服务工厂引发了未经处理的异常，则会将返回到客户端， <xref:Microsoft.ServiceHub.Framework.ServiceActivationFailedException> 以便它们可以了解并向用户报告失败。

当中转服务请求无法与任何可用的服务匹配时， `null` 将返回到客户端。
在这种情况下， <xref:Microsoft.ServiceHub.Framework.IServiceBroker.AvailabilityChanged> 将在和该服务以后可用时引发。

服务请求可能被拒绝，因为该服务不存在，但由于提供的版本低于请求的版本。
你的备用计划可能包括通过客户端知道的更低版本重试服务请求，并能够与进行交互。

如果来自所有失败版本检查的延迟很明显，则客户端可以 VisualStudioServices.VS2019_4Services 请求 RemoteBrokeredServiceManifest，以充分了解远程源中可用的服务和版本。

### <a name="handling-dropped-connections"></a><a name="DroppedConnections"></a> 处理删除的连接

成功获取的中转服务代理可能会因发生了断开连接或托管它的进程中的故障而失败。
此类中断后，对该代理所做的任何调用都将导致 <xref:StreamJsonRpc.ConnectionLostException> 引发。

中转服务客户端可以通过处理 <xref:StreamJsonRpc.JsonRpc.Disconnected> 事件主动检测并响应此类连接丢弃。
若要到达此事件，必须将代理强制转换为 <xref:StreamJsonRpc.IJsonRpcClientProxy> 以获取 <xref:StreamJsonRpc.JsonRpc> 对象。
此强制转换应按照条件进行，以便在服务为本地时正常失败。

```csharp
if (this.myService is IJsonRpcClientProxy clientProxy)
{
    clientProxy.JsonRpc.Disconnected += JsonRpc_Disconnected;
}

void JsonRpc_Disconnected(object? sender, JsonRpcDisconnectedEventArgs args)
{
    if (args.Reason == DisconnectedReason.RemotePartyTerminated)
    {
        // consider reacquisition of the service.
    }
}
```

### <a name="handling-service-availability-changes"></a><a name="ServiceAvailabilityChanges"></a> 处理服务可用性更改

如果传输服务客户端应通过处理 <xref:Microsoft.ServiceHub.Framework.IServiceBroker.AvailabilityChanged> 事件来重新查询先前查询的中转服务，则该客户端可能会收到通知。
在请求中转服务 *之前* ，应添加此事件的处理程序，以确保在执行服务请求后不久引发的事件不会由于争用情况而丢失。

当只请求一个异步方法的执行持续时间请求中转服务时，不建议处理此事件。
此事件与客户端最为相关，该客户端将其代理长期存储在较长的时间，以便需要对服务更改进行补偿，并将其放在一个位置以刷新其代理。

可能会在任何线程上引发此事件，可能会并发到使用事件描述的服务的代码。

几次状态更改可能导致引发此事件，包括：

- 正在打开或关闭的解决方案或文件夹。
- 开始 Live Share 会话。
- 刚发现的动态注册的中转服务。

受影响的中转服务仅会导致此事件引发到以前请求该服务的客户端，不管该请求是否已完成。

每个服务请求后，每个服务最多会引发一次此事件。
例如，如果客户端请求服务 **A** ，并且服务 **B** 发生可用性更改，则不会将任何事件引发到该客户端。
稍后，当服务 **A** 遇到可用性变化时，客户端将接收事件。
如果客户端不重新请求服务 **A**，则的后续可用性更改 **不会导致** 向该客户端发出进一步的通知。
客户端再次请求后，就可以接收有关该 **服务的下** 一条通知。

当服务变为可用、不再可用时，或遇到要求所有之前的服务客户端重新查询服务的实现更改时，会引发事件。

<xref:Microsoft.ServiceHub.Framework.ServiceBrokerClient>在返回任何租金后，会自动处理与缓存的代理相关的可用性更改事件，并在其所有者请求服务时请求服务的新实例，并请求服务的新实例。
当服务是无状态的，并且不要求你的代码将事件处理程序附加到代理时，此类可大大简化你的代码。

## <a name="retrieving-a-brokered-service-pipe"></a>检索中转服务管道

尽管通过代理访问中转服务是最常用且最方便的方法，但在高级方案中，最好还是需要请求管道发送到该服务，以便客户端可以直接控制 RPC 或直接与其他数据类型通信。

可以通过 <xref:Microsoft.ServiceHub.Framework.IServiceBroker.GetPipeAsync%2A> 方法获取中转服务的管道。
此方法使用 <xref:Microsoft.ServiceHub.Framework.ServiceMoniker> 而 <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor> 不是，因为不需要使用描述符提供的 RPC 行为。
如果有描述符，可以通过 <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor.Moniker%2A?displayProperty=nameWithType> 属性从它获取名字对象。

当管道绑定到 i/o 时，它们不符合垃圾回收的条件。
当不再使用这些管道时，请始终完成这些管道，以避免内存泄漏。

在以下代码片段中，将激活中转服务，并向其提供直接管道。
然后，客户端将文件的内容发送到服务并断开连接。

```csharp
async Task SendMovieAsync(string movieFilePath, CancellationToken cancellationToken)
{
    IServiceBroker serviceBroker;
    IDuplexPipe? pipe = await serviceBroker.GetPipeAsync(serviceMoniker, cancellationToken);
    if (pipe is null)
    {
        throw new InvalidOperationException($"The brokered service '{serviceMoniker}' is not available.");
    }

    try
    {
        // Open the file optimized for async I/O
        using FileStream fs = new FileStream(movieFilePath, FileMode.Open, FileAccess.Read, FileShare.Read, bufferSize: 4096, useAsync: true);
        await fs.CopyToAsync(pipe.Output.AsStream(), cancellationToken);
    }
    catch (Exception ex)
    {
        // Complete the pipe, passing through the exception so the remote side understands what went wrong.
        await pipe.Input.CompleteAsync(ex);
        await pipe.Output.CompleteAsync(ex);
        throw;
    }
    finally
    {
        // Always complete the pipe after successfully using the service.
        await pipe.Input.CompleteAsync();
        await pipe.Output.CompleteAsync();
    }
}
```

## <a name="testing-brokered-service-clients"></a><a name="TestingBrokeredClients"></a> 测试中转服务客户端

在测试扩展时，中转服务是模拟的合理依赖项。
当模拟传输服务时，我们建议使用模拟框架，该框架代表你实现接口，并将所需的代码注入你的客户端将调用的特定成员。
这样， [在将成员添加到中转服务接口时](best-practices-design-brokered-service.md#AddingInterfaceMembers)，您的测试就可以继续编译和运行而不中断。

当使用 [VisualStudio](https://www.nuget.org/packages/microsoft.visualstudio.sdk.testframework) 来测试扩展时，您的测试可以包含标准代码，以提供您的客户端代码可查询和运行的模拟服务。
例如，假设你想要在测试中模拟 VisualStudioServices。
可以通过以下代码提供模型：

```cs
IBrokeredServiceContainer sbc = await AsyncServiceProvider.GlobalProvider.GetServiceAsync<SVsBrokeredServiceContainer, IBrokeredServiceContainer>();
Mock<IFileSystem> mockFileSystem = new Mock<IFileSystem>();
sbc.Proffer(VisualStudioServices.VS2022.FileSystem, (ServiceMoniker moniker, ServiceActivationOptions options, IServiceBroker serviceBroker, CancellationToken cancellationToken) => new ValueTask<object?>(mockFileSystem.Object));
```

模拟中转服务容器不需要首先 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 注册提供服务。

测试中的代码可以像平时一样获取中转服务，只不过在测试下，它将获得模拟，而不是在下 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 运行时所获得的实际模型：

```cs
IBrokeredServiceContainer sbc = await AsyncServiceProvider.GlobalProvider.GetServiceAsync<SVsBrokeredServiceContainer, IBrokeredServiceContainer>();
IServiceBroker serviceBroker = sbc.GetFullAccessServiceBroker();
IFileSystem? proxy = await serviceBroker.GetProxyAsync<IFileSystem>(VisualStudioServices.VS2022.FileSystem);
using (proxy as IDisposable)
{
    Assumes.Present(proxy);
    await proxy.DeleteAsync(new Uri("file://some/file"), recursive: false, null, this.TimeoutToken);
}
```

## <a name="see-also"></a>另请参阅

- [发现可用的中转服务](internals/discover-available-brokered-services.md)
- [中转服务基础](internals/brokered-service-essentials.md)
