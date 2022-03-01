---
title: 如何：提供中转服务
description: 了解如何设计、创建、注册和提供中转服务供自己和他人使用。
monikerRange: '>= vs-2019'
ms.custom: SEO-VS-2020
ms.date: 01/07/2022
ms.topic: how-to
helpviewer_keywords:
- brokered services, providing
ms.assetid: e09556bb-41e4-46e2-a14d-47e09d67f8a1
author: aarnott
ms.author: andarno
manager: ansonh
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f3b112a8c29537e1a600038ac462b1c35bd75057
ms.sourcegitcommit: 169b7b66d13b7e3c86097b42206dd33389cd9166
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2022
ms.locfileid: "138153490"
---
# <a name="how-to-provide-a-brokered-service"></a>如何：提供中转服务

中转服务由以下元素组成：

- [声明](#ServiceInterface) 服务功能并充当服务及其客户端之间的协定的接口。
- [该接口](#ServiceImplementation) 的实现。
- [一个服务名字对象](#ServiceMoniker) ，用于为服务分配名称和版本。
- [一个描述符](#ServiceRpcDescriptor) ，它将服务名字对象与用于在必要时处理 RPC 的行为组合在一起。
- 要么[提供服务工厂，](#ProfferService)[再向](#ServiceRegistration) VS 包注册中转服务，要么[使用 MEF 进行这两项。](#MEF)

下面详细介绍了上述每一项。

对于本主题中所有代码，强烈建议激活 C# 的可 [为空引用类型](/dotnet/csharp/nullable-references) 功能。

## <a name="the-service-interface"></a><a name="ServiceInterface"></a> 服务接口

服务接口可能是标准 .NET 接口 (通常用 C#) <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor>编写，但应符合派生类型设置的准则，服务将使用该派生类型来确保当客户端和服务在不同进程中运行时，可以通过 RPC 使用该接口。
这些限制通常包括不允许使用属性和索引器，并且大多数或所有方法返回 `Task` 或其他异步兼容的返回类型。

是 <xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor> 中转服务的建议派生类型。
当客户端和服务需要 <xref:StreamJsonRpc> RPC 进行通信时，此类将利用 库。
StreamJsonRpc 对服务接口应用某些限制， [如下所述](https://github.com/microsoft/vs-streamjsonrpc/blob/main/doc/dynamicproxy.md)。

接口 *可能* 派生自 <xref:System.IDisposable>、 <xref:System.IAsyncDisposable?displayProperty=fullName>甚至 <xref:Microsoft.VisualStudio.Threading.IAsyncDisposable?displayProperty=fullName> ，但系统不需要此接口。
生成的客户端代理将采用任一 <xref:System.IDisposable> 方式实现。

简单的计算器服务接口可以声明为如下所示：

```csharp
public interface ICalculator
{
    ValueTask<double> AddAsync(double a, double b, CancellationToken cancellationToken);
    ValueTask<double> SubtractAsync(double a, double b, CancellationToken cancellationToken);
}
```

尽管此接口上的方法的实现可能不需要异步方法，但我们始终在此接口上使用异步方法签名，因为此接口用于生成可能远程调用此服务的客户端代理，这当然需要异步方法签名。

接口可以声明事件，这些事件可用于通知其客户端服务中发生的事件。

<a name="ClientRpcTarget"></a> 除了事件 <xref:Microsoft.ServiceHub.Framework.ServiceActivationOptions.ClientRpcTarget?displayProperty=nameWithType> 或观察者设计模式外，需要"回叫"客户端的中转服务可以定义另一个接口，该接口充当协定，客户端必须在请求服务时通过 属性实现并提供协定。
此类接口应符合与中转服务接口相同的设计模式和限制，但增加了版本控制限制。

有关 [设计性能高、](best-practices-design-brokered-service.md) 面向未来的 RPC 接口的提示，请查看设计中转服务最佳做法。

与实现服务的程序集不同，在非重复程序集中声明此接口非常有用，以便其客户端可以引用接口，而无需服务公开其更多实现详细信息。
将接口程序集作为一个NuGet包提供，供其他扩展引用，同时保留自己的扩展以提供服务实现，这也可能很有用。

请考虑将`netstandard2.0`声明服务接口的程序集作为目标，以确保无论服务是运行 .NET Framework、.NET Core、.NET 5 或更高版本，都可以轻松地从任何 .NET 进程调用。

### <a name="testing"></a>正在测试

自动测试应连同服务接口 *一起编写，* 以验证接口的 RPC 就绪情况。

测试应验证通过 接口传递的所有数据是否可序列化。

你可能会发现 <xref:Microsoft.VisualStudio.Sdk.TestFramework.BrokeredServiceContractTestBase%602> [Microsoft.VisualStudio.Sdk.TestFramework.Xunit](https://www.nuget.org/packages/microsoft.visualstudio.sdk.testframework.xunit) 包中的 类可用于派生接口测试类。
此类包括接口的一些基本约定测试、用于协助常见断言（如事件测试）的方法等。

#### <a name="methods"></a>方法

断言每个参数和返回值已完全序列化。
如果使用上述测试基类，可能如下所示：

```csharp
public interface IYourService
{
    Task<bool> SomeOperationAsync(YourStruct arg1);
}

public static class Descriptors
{
    public static readonly ServiceRpcDescriptor YourService = new ServiceJsonRpcDescriptor(
        new ServiceMoniker("YourCompany.YourExtension.YourService", new Version(1, 0)),
        clientInterface: null,
        ServiceJsonRpcDescriptor.Formatters.MessagePack,
        ServiceJsonRpcDescriptor.MessageDelimiters.BigEndianInt32LengthHeader,
        new MultiplexingStream.Options { ProtocolMajorVersion = 3 })
        .WithExceptionStrategy(StreamJsonRpc.ExceptionProcessing.ISerializable);
}

public class YourServiceMock : IYourService
{
    internal YourStruct? SomeOperationArg1 { get; set; }

    public Task<bool> SomeOperationAsync(YourStruct arg1, CancellationToken cancellationToken)
    {
        this.SomeOperationArg1 = arg1;
        return true;
    }
}

public class BrokeredServiceTests : BrokeredServiceContractTestBase<IYourService, YourServiceMock>
{
    public BrokeredServiceTests(ITestOutputHelper logger)
        : base(logger, Descriptors.YourService)
    {
    }

    [Fact]
    public async Task SomeOperation()
    {
        var arg1 = new YourStruct
        {
            Field1 = "Something",
        };
        Assert.True(await this.ClientProxy.SomeOperationAsync(arg1, this.TimeoutToken));
        Assert.Equal(arg1.Field1, this.Service.SomeOperationArg1.Value.Field1);
    }
}
```

如果声明多个同名的方法，请考虑测试重载解析。
可以针对 `internal` 用于存储该方法的参数的每个方法向模拟服务添加一个字段，以便测试方法可以调用该方法，然后验证是否使用正确的参数调用了正确的方法。

#### <a name="events"></a>事件

在接口上声明的任何事件也应测试 RPC 就绪情况。
如果在 RPC 序列化期间由于事件"发后忘记"而失败，则从中转服务引发的事件不会导致测试失败。

如果使用的是上面提到的测试基类，则此行为已内置于一些帮助程序方法中，可能如下所示 (为简洁起见，省略了未更改) ：

```cs
public interface IYourService
{
    event EventHandler<int> NewTotal;
}

public class YourServiceMock : IYourService
{
    public event EventHandler<int>? NewTotal;

    internal void RaiseNewTotal(int arg) => this.NewTotal?.Invoke(this, arg);
}

public class BrokeredServiceTests : BrokeredServiceContractTestBase<IYourService, YourServiceMock>
{
    [Fact]
    public async Task NewTotal()
    {
        await this.AssertEventRaisedAsync<int>(
            (p, h) => p.NewTotal += h,
            (p, h) => p.NewTotal -= h,
            s => s.RaiseNewTotal(50),
            a => Assert.Equal(50, a));
    }
}
```

## <a name="implementing-the-service"></a><a name="ServiceImplementation"></a> 实现服务

服务类应实现在上一步中声明的 RPC 接口。
服务可以实现 <xref:System.IDisposable> 或除用于 RPC 的接口以外的任何其他接口。
在客户端上生成的 <xref:System.IDisposable>代理将仅实现服务接口 ，并且可能实现一些其他选择接口来支持系统，因此强制转换到服务实现的其他接口将在客户端上失败。

请考虑上面使用的计算器示例，我们在此处实现该示例：

```csharp
internal class Calculator : ICalculator
{
    public ValueTask<double> AddAsync(double a, double b, CancellationToken cancellationToken)
    {
        return new ValueTask<double>(a + b);
    }

    public ValueTask<double> SubtractAsync(double a, double b, CancellationToken cancellationToken)
    {
        return new ValueTask<double>(a - b);
    }
}
```

由于方法主体本身不需要 <xref:System.Threading.Tasks.ValueTask%601> 是异步的，因此我们将返回值显式包装在构造的返回类型中，以符合服务接口。

### <a name="implementing-the-observable-design-pattern"></a>实现可观测设计模式

如果在服务接口上提供观察程序订阅，它可能如下所示：

```cs
Task<IDisposable> SubscribeAsync(IObserver<YourDataType> observer);
```

参数 <xref:System.IObserver%601> 通常需要延长此方法调用的生存期，以便客户端可以在方法调用完成后继续接收更新，直到客户端释放返回的值 <xref:System.IDisposable> 。
为方便此操作，服务类可能包含订阅 <xref:System.IObserver%601> 集合，然后，对状态进行的任何更新都会枚举这些订阅以更新所有订阅者。
请确保集合的枚举彼此是线程安全的，尤其是在该集合上可能会通过其他订阅或这些订阅的处置发生的变化。

请注意，通过 发布的所有 <xref:System.IObserver%601.OnNext%2A> 更新都保留向服务引入状态更改的顺序。

所有订阅最终都应<xref:System.IObserver%601.OnCompleted%2A><xref:System.IObserver%601.OnError%2A>通过调用 或 终止，以避免客户端和 RPC 系统上的资源泄漏。
这包括有关应显式完成所有剩余订阅的服务处置。

详细了解观察者[设计模式，](/dotnet/standard/events/observer-design-pattern)[以及如何实现可](/dotnet/standard/events/how-to-implement-a-provider)观测数据提供程序，尤其是考虑 [RPC](https://github.com/microsoft/vs-streamjsonrpc/blob/main/doc/observer.md)。

### <a name="disposable-services"></a>可释放服务

服务类不一定可释放，但当客户端将代理释放给服务或者客户端和服务之间的连接丢失时，将释放这些服务。
可释放接口按此顺序测试 ： <xref:System.IAsyncDisposable?displayProperty=fullName>、 <xref:Microsoft.VisualStudio.Threading.IAsyncDisposable?displayProperty=fullName>、 <xref:System.IDisposable>。
只有服务类实现此列表的第一个接口将用于释放服务。

在考虑处置时，请记住线程安全性。
当 <xref:System.IDisposable.Dispose%2A> 服务中的其他代码正在运行时，可以在任何线程上调用方法 (例如，如果正在删除连接) 。

### <a name="throwing-exceptions"></a>引发异常

引发异常时，请考虑使用 <xref:StreamJsonRpc.LocalRpcException> 特定的 [ErrorCode](xref:StreamJsonRpc.LocalRpcException.ErrorCode) 引发 ，以便控制 客户端在 中接收的错误代码 <xref:StreamJsonRpc.RemoteInvocationException>。
与分析异常消息或类型不同，向客户端提供错误代码可以使它们基于错误的性质进行分支。

根据 JSON-RPC 规范，错误代码必须大于 -32000，包括正数。

### <a name="consuming-other-brokered-services"></a>使用其他中转服务

当中转服务本身需要访问<xref:Microsoft.ServiceHub.Framework.IServiceBroker><xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute.AllowTransitiveGuestClients>另一个中转服务时，建议使用提供给其服务工厂的 ，但当中转服务注册设置 标志时，这一点尤其重要。

如果计算器服务需要其他中转服务来实现其行为，为了符合此准则，我们将修改 构造函数以接受 <xref:Microsoft.ServiceHub.Framework.IServiceBroker>：

```csharp
internal class Calculator : ICalculator
{
    private readonly State state;
    private readonly IServiceBroker serviceBroker;

    internal class Calculator(State state, IServiceBroker serviceBroker)
    {
        this.state = state;
        this.serviceBroker = serviceBroker;
    }

    // ...
}
```

详细了解如何[保护中转服务和](how-to-secure-brokered-service.md)[使用中转服务](how-to-consume-brokered-service.md)。

### <a name="stateful-services"></a>有状态服务

#### <a name="per-client-state"></a>每个客户端状态

将为请求该服务的每个客户端创建此类的新实例。
上述类上的 `Calculator` 字段将存储每个客户端可能唯一的值。
假设我们添加一个计数器，该计数器每次执行操作时递增：

```csharp
internal class Calculator : ICalculator
{
    int operationCounter;

    public ValueTask<double> AddAsync(double a, double b, CancellationToken cancellationToken)
    {
        this.operationCounter++;
        return new ValueTask<double>(a + b);
    }

    public ValueTask<double> SubtractAsync(double a, double b, CancellationToken cancellationToken)
    {
        this.operationCounter++;
        return new ValueTask<double>(a - b);
    }
}
```

应编写中转服务，以遵循线程安全做法。
使用建议的 时 <xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor>，与客户端的远程连接可能包括并发执行服务的方法，如本文档 [中所述](https://github.com/microsoft/vs-streamjsonrpc/blob/main/doc/resiliency.md)。
当客户端与服务共享进程和 AppDomain 时，客户端可能会从多个线程并发调用服务。
上述示例的线程安全实现可能会使用 <xref:System.Threading.Interlocked.Increment(System.Int32@)?displayProperty=nameWithType> 递增 `operationCounter` 字段。

#### <a name="shared-state"></a>共享状态

如果状态是服务需要在其所有客户端之间共享，则此状态应在不同的类中定义，该类由 VS 包实例化，并作为参数传递给服务的构造函数。

假设我们希望上面 `operationCounter` 定义的 对服务的所有客户端的所有操作进行计数。
我们需要将 字段提升为此新的状态类：

```csharp
internal class Calculator : ICalculator
{
    private readonly State state;

    internal class Calculator(State state)
    {
        this.state = state;
    }

    public ValueTask<double> AddAsync(double a, double b, CancellationToken cancellationToken)
    {
        this.state.IncrementCounter();
        return new ValueTask<double>(a + b);
    }

    public ValueTask<double> SubtractAsync(double a, double b, CancellationToken cancellationToken)
    {
        this.state.IncrementCounter();
        return new ValueTask<double>(a - b);
    }

    internal class State
    {
        private int operationCounter;

        internal int OperationCounter => this.operationCounter;

        internal void IncrementCounter() => Interlocked.Increment(ref this.operationCounter);
    }
}
```

现在，我们有一种简洁且可测试的方式来管理服务多个实例中的共享 `Calculator` 状态。
稍后在编写代码以向服务提供内容时，我们将了解如何 `State` 创建此类一次，以及如何与服务每个 `Calculator` 实例共享此类。

在处理共享状态时，线程安全尤为重要，因为无法对多个客户端计划其调用进行假设，因此永远不会同时进行调用。

如果共享状态类需要访问其他中转服务，则它应使用全局 Service Broker，而不是分配给中转服务单个实例的上下文中转站之一。
设置 标志时，在中转[](how-to-secure-brokered-service.md)<xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute.AllowTransitiveGuestClients?displayProperty=nameWithType>服务内使用全局 Service Broker 会带来安全隐患。

### <a name="security-concerns"></a>安全注意事项

如果使用 标志<xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute.AllowTransitiveGuestClients?displayProperty=nameWithType>注册中转服务，则安全性是一个考虑因素，这会使参与共享会话的其他计算机上其他用户Live Share访问。

在 [设置 标志之前，](how-to-secure-brokered-service.md) 请查看如何保护中转服务并提供必要的安全 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute.AllowTransitiveGuestClients> 缓解措施。

## <a name="the-service-moniker"></a><a name="ServiceMoniker"></a> 服务名字对象

中转服务必须具有可序列化的名称和版本，客户端可以请求该服务。
是 <xref:Microsoft.ServiceHub.Framework.ServiceMoniker> 这两条信息的方便包装器。

服务名字对象类似于 CLR 类型的程序集限定全名。
它必须全局唯一，因此应包含公司名称，以及扩展名作为服务名称本身的前缀。

在字段中定义此 `static readonly` 名字对象以在其他地方使用可能很有用：

```csharp
public static readonly ServiceMoniker Moniker = new ServiceMoniker("YourCompany.Extension.Calculator", new Version("1.0"));
```

虽然服务的大多数使用可能不会直接使用名字对象，但通过管道而不是代理进行通信的客户端将需要名字对象。

## <a name="the-service-descriptor"></a><a name="ServiceRpcDescriptor"></a> 服务描述符

服务描述符将服务名字对象与运行 RPC 连接和创建本地或远程代理所需的行为相结合。
描述符负责有效地将 RPC 接口转换为线路协议。
此服务描述符是 派生类型的 <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor>实例。
描述符必须可供将使用代理访问此服务的所有客户端使用。
提供服务还需要此描述符。

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 定义一个此类派生类型，并建议其用于所有服务： <xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor>。
此描述符 <xref:StreamJsonRpc> 利用其 RPC 连接，并创建本地服务的高性能本地代理，以模拟某些远程行为，例如包装 服务在 中引发的异常 <xref:StreamJsonRpc.RemoteInvocationException>。

支持 <xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor> 为 JSON-RPC <xref:StreamJsonRpc.JsonRpc> 协议的 JSON 或 MessagePack 编码配置 类。
建议使用 MessagePack 编码，因为它更紧凑，性能可能高 10 倍。

我们可以为计算器服务定义描述符，如下所示：

```csharp
/// <summary>
/// The descriptor for the calculator brokered service.
/// Use the <see cref="ICalculator"/> interface for the client proxy for this service.
/// </summary>
public static readonly ServiceRpcDescriptor CalculatorService = new ServiceJsonRpcDescriptor(
    Moniker,
    Formatters.MessagePack,
    MessageDelimiters.BigEndianInt32LengthHeader,
    new MultiplexingStream.Options { ProtocolMajorVersion = 3 })
    .WithExceptionStrategy(StreamJsonRpc.ExceptionProcessing.ISerializable);
```

如上所示，可以选择格式化程序以及分隔符。
由于并非所有组合都有效，因此建议采用以下任一组合：

<xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor.Formatters> | <xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor.MessageDelimiters> | 最适用于
--|--|--
<xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor.Formatters.MessagePack> | <xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor.MessageDelimiters.BigEndianInt32LengthHeader> | 高性能
<xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor.Formatters.UTF8> (JSON)  | <xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor.MessageDelimiters.HttpLikeHeaders> | 与其他 JSON-RPC 系统互操作

`MultiplexingStream.Options`通过指定 对象作为最终参数，客户端和服务之间共享的 RPC 连接只是 [MultiplexingStream](https://github.com/AArnott/Nerdbank.Streams/blob/main/doc/MultiplexingStream.md) 上的一个通道，该通道与 JSON-RPC 连接共享，以便通过 [JSON-RPC](https://github.com/microsoft/vs-streamjsonrpc/blob/main/doc/oob_streams.md) 高效传输大型二进制数据。

该<xref:StreamJsonRpc.ExceptionProcessing.ISerializable?displayProperty=nameWithType>策略会导致将服务引发的异常序列化并保留为<xref:System.Exception.InnerException?displayProperty=nameWithType><xref:StreamJsonRpc.RemoteInvocationException>客户端上引发的 的 。
如果没有此设置，客户端上会提供不太详细的异常信息。

提示：将描述符公开为 <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor> ，而不是用作实现详细信息的任何派生类型。
这样，你以后可以更灵活地更改实现详细信息，而无需 API 中断性变更。

在描述符的 xml 文档注释中包括对服务接口的引用，以便用户更轻松地使用服务。
另请引用服务接受的接口作为客户端 RPC 目标（如果适用）。

某些更高级的服务可能也接受或要求客户端提供符合某个接口的 RPC 目标对象。
对于这种情况，请使用具有 <xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor.%23ctor%2A> 参数 `Type clientInterface` 的构造函数来指定客户端应提供 的实例的接口。

### <a name="versioning-the-descriptor"></a>对描述符进行版本控制

随着时间的推移，你可能希望递增服务的版本。
在这种情况下，应为每个想要支持的版本定义描述符，为每个版本使用 <xref:Microsoft.ServiceHub.Framework.ServiceMoniker> 特定于唯一的版本。
同时支持多个版本可以促进向后兼容性，通常只需使用一个 RPC 接口。

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]遵循此模式及其 <xref:Microsoft.VisualStudio.VisualStudioServices> 类，<xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor>`virtual`将原始 类定义为嵌套类下的属性，该嵌套类表示添加该中转服务的第一个发布。
当我们需要更改服务的线路协议或添加/更改功能时， [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] `override` 在返回新 的更高版本的嵌套类中声明属性 <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor>。

对于由扩展定义和提供 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的服务，只需声明原始服务旁边的另一个描述符属性即可。
例如，假设 1.0 服务使用 UTF8 (JSON) 格式化程序，并且你意识到切换到 MessagePack 可提供显著的性能优势。
由于更改格式化程序是一项网络协议中断性变更，因此需要递增中转服务版本号和第二个描述符。
这两个描述符可能如下所示：

```csharp
public static readonly ServiceJsonRpcDescriptor CalculatorService = new ServiceJsonRpcDescriptor(
    new ServiceMoniker("YourCompany.Extension.Calculator", new Version("1.0")),
    Formatters.UTF8,
    MessageDelimiters.HttpLikeHeaders,
    new MultiplexingStream.Options { ProtocolMajorVersion = 3 })
    );

public static readonly ServiceJsonRpcDescriptor CalculatorService1_1 = new ServiceJsonRpcDescriptor(
    new ServiceMoniker("YourCompany.Extension.Calculator", new Version("1.1")),
    Formatters.MessagePack,
    MessageDelimiters.BigEndianInt32LengthHeader,
    new MultiplexingStream.Options { ProtocolMajorVersion = 3 });
```

尽管我们声明了两个描述符 (及更高版本，但我们必须提供和注册两个服务) 只需使用一个服务接口和实现就可以实现这一点，使支持多个服务版本的开销非常低。

## <a name="proffering-the-service"></a><a name="ProfferService"></a> 提供服务

当请求进入时，必须创建中转服务，该请求通过称为"提供服务"的步骤进行排列。

### <a name="the-service-factory"></a>服务工厂

改用 <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GlobalProvider%2A><xref:Microsoft.VisualStudio.Shell.ServiceExtensions.GetServiceAsync%2A> <xref:Microsoft.VisualStudio.Shell.ServiceBroker.SVsBrokeredServiceContainer>请求 。
然后， <xref:Microsoft.VisualStudio.Shell.ServiceBroker.IBrokeredServiceContainer.Proffer%2A?displayProperty=nameWithType> 调用该容器以提供服务。

在下面的示例中，我们使用前面 `CalculatorService` 声明的 字段（设置为 的实例）提供服务 <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor>。
我们将服务工厂（即委托）传递给它 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.BrokeredServiceFactory> 。

```cs
IBrokeredServiceContainer container = await AsyncServiceProvider.GlobalProvider.GetServiceAsync<SVsBrokeredServiceContainer, IBrokeredServiceContainer>();
container.Proffer(
    CalculatorService,
    (moniker, options, serviceBroker, cancellationToken) => new ValueTask<object?>(new CalculatorService()));
```

中转服务通常每个客户端实例化一次。
这与其他 [VS 服务不同，](using-and-providing-services.md)这些服务通常实例化一次，并跨所有客户端共享。
每个客户端创建一个服务实例可以提供更好的安全性，因为每个服务和/ <xref:System.Globalization.CultureInfo> 或它的连接可以保留有关客户端操作的授权级别、首选级别等的每个客户端状态。接下来我们将看到，它还允许更有趣的服务接受特定于此请求的参数。

> [!Important]
> 偏离此准则并返回共享服务实例（而不是向每个客户端返回新实例）的服务工厂永远不应实现其服务，因为第一个释放其代理的客户端将导致在其他客户端使用该实例之前处置共享服务实例。<xref:System.IDisposable>

在更高级的情况下， `CalculatorService` 如果构造函数需要共享状态 <xref:Microsoft.ServiceHub.Framework.IServiceBroker>对象和 ，则我们可以提供工厂，如下所示：

```csharp
var state = new CalculatorService.State();
container.Proffer(
    CalculatorService,
    (moniker, options, serviceBroker, cancellationToken) => new ValueTask<object?>(new CalculatorService(state, serviceBroker)));
```

本地 `state` 变量位于 *服务* 工厂外部，因此仅创建一次，并跨所有实例化服务共享。

更高级的是，如果服务需要访问 <xref:Microsoft.ServiceHub.Framework.ServiceActivationOptions> (例如，在客户端 RPC 目标对象上调用方法) 也可以传入的方法：

```csharp
var state = new CalculatorService.State();
container.Proffer(CalculatorService, (moniker, options, serviceBroker, cancellationToken) =>
    new ValueTask<object?>(new CalculatorService(state, serviceBroker, options)));
```

在这种情况下，服务构造函数可能如下所示<xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor>`typeof(IClientCallbackInterface)`，假定 是使用 作为构造函数参数之一创建的：

```csharp
internal class Calculator(State state, IServiceBroker serviceBroker, ServiceActivationOptions options)
{
    this.state = state;
    this.serviceBroker = serviceBroker;
    this.options = options;
    this.clientCallback = (IClientCallbackInterface)options.ClientRpcTarget;
}
```

现在 `clientCallback` ，只要服务想要调用客户端，就可以调用此字段，直到释放连接。

递增 上的版本时 <xref:Microsoft.ServiceHub.Framework.ServiceMoniker>，必须提供要响应其客户端请求的每个中转服务版本。
为此，可以调用 方法 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.IBrokeredServiceContainer.Proffer%2A?displayProperty=nameWithType> ，其中每个方法 <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor> 仍受支持。

如果 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.BrokeredServiceFactory> 服务工厂是基于 <xref:Microsoft.ServiceHub.Framework.ServiceMoniker> 名字对象创建多个服务的共享方法，则委托采用 作为参数。
此名字对象来自客户端，包括预期服务的版本。
通过向服务构造函数转发此名字对象，服务可能会模拟特定服务版本的异常行为，以匹配客户端可能期望的行为。

除非将在 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.AuthorizingBrokeredServiceFactory> 中转服务类 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.IBrokeredServiceContainer.Proffer%2A?displayProperty=nameWithType> 内使用 ， <xref:Microsoft.ServiceHub.Framework.Services.IAuthorizationService> 否则请避免将 委托与 方法一起使用。
*必须使用*<xref:Microsoft.ServiceHub.Framework.Services.IAuthorizationService>中转服务类释放此 ，以避免内存泄漏。

## <a name="registering-the-service"></a><a name="ServiceRegistration"></a> 注册服务

除非首先注册了中转服务，否则将中转服务缓冲到全局中转服务容器会引发 。
注册为容器提供了一种提前了解哪些中转服务可能可用，以及请求这些服务时要加载哪些 VS 包以执行缓冲代码的方式。
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]这样可以快速启动，而无需提前加载所有扩展，但能够在其中转服务的客户端请求时加载所需的扩展。

可以通过将 应用于派生类 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute> 完成 <xref:Microsoft.VisualStudio.Shell.AsyncPackage>注册。
这是唯一可以设置 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience> 的位置。

```csharp
[ProvideBrokeredService("YourCompany.Extension.Calculator", "1.0", Audience = ServiceAudience.Local)]
```

<xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute.Audience>默认值为 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience.Process?displayProperty=nameWithType>，它仅向同一进程中的其他代码公开中转服务。
通过设置 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience.Local?displayProperty=nameWithType>，可以选择将中转服务公开给属于同一会话的其他 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 进程。

如果中转服务 *必须* 公开给Live Share来宾，则必须<xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute.Audience>包含 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience.LiveShareGuest?displayProperty=nameWithType> ，<xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute.AllowTransitiveGuestClients?displayProperty=nameWithType>并且 属性设置为 `true`。
**设置这些标志可能会引入** 严重的安全漏洞，如果不首先遵循如何保护中转服务中的 [指南，则不应这样做](how-to-secure-brokered-service.md)。

递增 上的版本时 <xref:Microsoft.ServiceHub.Framework.ServiceMoniker>，必须注册要响应其客户端请求的每个中转服务版本。
通过支持比中转服务的最新版本更多的功能，有助于保持旧版中转服务版本的客户端的后向兼容性，这在考虑 Live Share [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 方案（其中每个共享会话的 版本可能不同）时可能特别有用。

## <a name="use-mef-to-proffer-and-register-your-service"></a><a name="MEF"></a> 使用 MEF 提供和注册服务

**[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]这需要 2022 Update 2 或更高版本。**

中转服务可以通过 MEF [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 导出，而不是使用包导出，如前两部分所述。
这需要考虑以下权衡：

权衡 | 包缓冲区 | MEF Export — MEF 导出
--|--|--
可用性 | ✅ 中转服务在 VS 启动时立即可用。 | ⚠️ 在进程中初始化 MEF 之前，中转服务的可用性可能会延迟。 这通常很快，但在 MEF 缓存过时时可能需要几秒钟时间。
跨平台就绪情况 | ⚠️Visual Studio特定Windows必须创作特定代码。 | ✅程序集中的中转服务可以加载到 Visual Studio 中Windows，Visual Studio for Mac。

若要通过 MEF 而不是 VS 包导出中转服务，请执行：

1. 确认没有与最后两个部分相关的代码。 具体而言，应该没有调用 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.IBrokeredServiceContainer.Proffer%2A?displayProperty=nameWithType> 的代码，并且不应 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute> 将 应用于包 (（如果有) ）。
1. 在中转 `IExportedBrokeredService` 服务类上实现 接口。
1. 避免构造函数中出现任何主线程依赖项或导入属性资源组。 `IExportedBrokeredService.InitializeAsync`使用 方法初始化中转服务，允许使用主线程依赖项。
1. `ExportBrokeredServiceAttribute`将 应用于中转服务类，指定有关服务名字对象、受众以及所需的任何其他注册相关信息的信息。
1. 如果类需要处置，请实现 <xref:System.IDisposable> <xref:System.IAsyncDisposable> 而不是 ，因为 MEF 拥有服务的生存期，并且仅支持同步处置。
1. 确保文件 `source.extension.vsixmanifest` 将包含中转服务的项目作为 MEF 程序集列出。

作为 MEF 部分，中转服务 *可能会* 导入默认作用域中任何其他 MEF 部件。
执行此操作时，请务必使用 而不是 <xref:System.ComponentModel.Composition.ImportAttribute?displayProperty=fullName> <xref:System.Composition.ImportAttribute?displayProperty=fullName>。
这是因为 必须派生 `ExportBrokeredServiceAttribute` 自 <xref:System.ComponentModel.Composition.ExportAttribute?displayProperty=fullName> 并在整个类型中使用相同的 MEF 命名空间。

中转服务在能够导入一些特殊导出方面是唯一的：

- <xref:Microsoft.ServiceHub.Framework.IServiceBroker>，它应用于获取其他中转服务。
- <xref:Microsoft.ServiceHub.Framework.ServiceMoniker>，在导出多个版本的中转服务并需要检测客户端请求的版本时，这会很有用。
- <xref:Microsoft.ServiceHub.Framework.ServiceActivationOptions>，当您要求客户端提供特殊参数或客户端回调目标时，这会很有用。
- <xref:Microsoft.ServiceHub.Framework.Services.AuthorizationServiceClient>如果需要执行安全检查（如 [如何保护中转服务](how-to-secure-brokered-service.md)）中所述，这会很有用。
此对象 *不* 需要由你的类释放，因为当你的中转服务被释放时，它将自动释放。

中转服务 *不能* 使用 MEF <xref:System.ComponentModel.Composition.ImportAttribute> 来获取其他中转服务。
相反，它可以 `[Import]` <xref:Microsoft.ServiceHub.Framework.IServiceBroker> 以传统方式查询中转服务。
有关详细信息，请参阅 [如何使用中转服务](how-to-consume-brokered-service.md)。

示例如下：

```cs
using System;
using System.ComponentModel.Composition;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceHub.Framework;
using Microsoft.ServiceHub.Framework.Services;
using Microsoft.VisualStudio.Shell.ServiceBroker;

[ExportBrokeredService("Calc", "1.0")]
internal class MefBrokeredService : IExportedBrokeredService, ICalculator
{
    internal static ServiceRpcDescriptor SharedDescriptor { get; } = new ServiceJsonRpcDescriptor(
        new ServiceMoniker("Calc", new Version("1.0")),
        clientInterface: null,
        ServiceJsonRpcDescriptor.Formatters.MessagePack,
        ServiceJsonRpcDescriptor.MessageDelimiters.BigEndianInt32LengthHeader,
        new MultiplexingStream.Options { ProtocolMajorVersion = 3 });

    // IExportedBrokeredService
    public ServiceRpcDescriptor Descriptor => SharedDescriptor;

    [Import]
    IServiceBroker ServiceBroker { get; set; } = null!;

    [Import]
    ServiceMoniker ServiceMoniker { get; set; } = null!;

    [Import]
    ServiceActivationOptions Options { get; set; }

    // IExportedBrokeredService
    public Task InitializeAsync(CancellationToken cancellationToken)
    {
        return Task.CompletedTask;
    }

    public ValueTask<int> AddAsync(int a, int b, CancellationToken cancellationToken = default)
    {
        return new(a + b);
    }

    public ValueTask<int> SubtractAsync(int a, int b, CancellationToken cancellationToken = default)
    {
        return new(a - b);
    }
}
```

### <a name="exporting-multiple-versions-of-your-brokered-service"></a>导出多个版本的中转服务

`ExportBrokeredServiceAttribute`可以多次应用到中转服务，以提供中转服务的多个版本。

你的 `IExportedBrokeredService.Descriptor` 属性的实现应返回一个描述符，其中包含与客户端请求的名字对象匹配的名字对象。

请考虑以下示例：计算器服务使用 UTF8 格式导出1.0，以后再添加1.1 导出，以获得使用 MessagePack 格式的 wins 性能。

```cs
[ExportBrokeredService("Calc", "1.0")]
[ExportBrokeredService("Calc", "1.1")]
internal class MefBrokeredService : IExportedBrokeredService, ICalculator
{
    internal static ServiceRpcDescriptor SharedDescriptor1_0 { get; } = new ServiceJsonRpcDescriptor(
        new ServiceMoniker("Calc", new Version("1.0")),
        clientInterface: null,
        ServiceJsonRpcDescriptor.Formatters.UTF8,
        ServiceJsonRpcDescriptor.MessageDelimiters.HttpLikeHeaders,
        new MultiplexingStream.Options { ProtocolMajorVersion = 3 });

    internal static ServiceRpcDescriptor SharedDescriptor1_1 { get; } = new ServiceJsonRpcDescriptor(
        new ServiceMoniker("Calc", new Version("1.1")),
        clientInterface: null,
        ServiceJsonRpcDescriptor.Formatters.MessagePack,
        ServiceJsonRpcDescriptor.MessageDelimiters.BigEndianInt32LengthHeader,
        new MultiplexingStream.Options { ProtocolMajorVersion = 3 });

    // IExportedBrokeredService
    public ServiceRpcDescriptor Descriptor =>
        this.ServiceMoniker.Version == SharedDescriptor1_0.Moniker.Version ? SharedDescriptor1_0 :
        this.ServiceMoniker.Version == SharedDescriptor1_1.Moniker.Version ? SharedDescriptor1_1 :
        throw new NotSupportedException();

    [Import]
    ServiceMoniker ServiceMoniker { get; set; } = null!;
}
```

## <a name="see-also"></a>另请参阅
- [设计中转服务的最佳做法](best-practices-design-brokered-service.md)
- [如何保护中转服务](how-to-secure-brokered-service.md)
- [中转服务基础](internals/brokered-service-essentials.md)
- [如何获取中转服务](how-to-consume-brokered-service.md)
- [使用和提供中转服务](use-and-provide-brokered-services.md)
