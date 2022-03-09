---
title: 如何：排查中转服务问题
description: 了解如何排查尝试在 Visual Studio SDK 中获取中转服务时可能会发生的几个常见问题。
monikerRange: '>= vs-2019'
ms.custom: SEO-VS-2020
ms.date: 02/18/2022
ms.topic: troubleshooting
helpviewer_keywords:
- brokered services, troubleshooting
ms.assetid: 1972fbf6-246a-41a7-b557-365939c95781
author: aarnott
ms.author: andarno
manager: ansonh
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: bafa7c029ee8b87037e35286dfeb78c32f93602f
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139604948"
---
# <a name="how-to-troubleshoot-brokered-services"></a>如何：排查中转服务问题

中转服务可能会以各种方式失败。
下面介绍了几种常见方法，并介绍了指导调查和可能的修复的建议。

启动调查的一[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]种有用技术是检查活动日志，该日志通常会在中转服务出错时记录错误或警告。[](/visualstudio/extensibility/how-to-use-the-activity-log?view=vs-2022)

## <a name="requesting-a-service"></a>请求服务

中转服务最常见的挑战可能是了解它们通过调用 或 获得的结果或 <xref:Microsoft.ServiceHub.Framework.IServiceBroker.GetProxyAsync%2A?displayProperty=nameWithType> 异常 <xref:Microsoft.ServiceHub.Framework.IServiceBroker.GetPipeAsync%2A?displayProperty=nameWithType>。
有意 <xref:Microsoft.ServiceHub.Framework.IServiceBroker> 从何处以及如何激活中转服务这一关注点中消失。 但是，当出现问题时，有必要更深入地诊断和更正问题。

### <a name="no-service"></a>无服务

当满足以下任一条件 `null` 时，服务请求的结果可能是：

- 请求的服务未注册。 中转服务作者应注册到 或 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute> 手动创作的 pkgdef 文件。
- 请求的服务注册到不向此客户端公开该服务的配置。
  默认范围为 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience.Process?displayProperty=nameWithType>，这意味着中转服务只能在与客户端相同的进程中进行缓冲时激活。
  如果客户端在另一个进程中，并且意图是使中转服务可供其使用，请更改服务注册以扩展其 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience>。
- 请求的服务已<xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience.LiveShareGuest?displayProperty=nameWithType>注册到 ，<xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute.AllowTransitiveGuestClients?displayProperty=nameWithType>Live Share连接存在，但主机未提供中转服务，或者 属性未设置为 `true`。
  通过代理服务公开中转Live Share，请查看[如何保护中转服务](how-to-secure-brokered-service.md)。
- 请求的服务已注册，但缺少有关要初始化的包的信息，以便可以缓冲其工厂。 属性 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute> 自动生成注册，该注册指示属性已应用到的包，以便 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 可根据需要加载该包。
  如果属性应用于错误的包，或者 pkgdef 文件是手动创作的，则此信息可能缺失或不准确。
- 负责 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 提供中转服务的包在初始化期间引发，否则无法实际提供该服务工厂。
  检查活动[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)][日志](/visualstudio/extensibility/how-to-use-the-activity-log?view=vs-2022)，了解包加载失败的证据。
- 服务工厂本身返回 `null`。

### <a name="service-request-throws-exception"></a>服务请求引发异常

当服务工厂引发异常 <xref:Microsoft.ServiceHub.Framework.ServiceCompositionException> 时，服务请求可能会引发 。
这意味着上面列出的会导致结果 `null` 的所有问题都不适用。
查看异常详细信息 (包括内部异常) 以了解问题，并更正客户端或服务工厂。

### <a name="local-service-where-a-remote-one-was-expected"></a>需要远程服务的本地服务

请求可能在本地或远程完成，具体取决于服务注册和 的当前状态 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。
默认作用域是 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience.Process?displayProperty=nameWithType> ，这意味着中转服务只能在与客户端相同的进程中进行缓冲时激活。

当中转服务应<xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience>从 Live Share 主机公开给连接的来宾，但 仅限于本地范围时，来自 Live Share 来宾的请求将激活来自同一台计算机（而不是主机）的中转服务。
更新注册以包含 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience.LiveShareGuest?displayProperty=nameWithType> ，以通过 Live Share。
可能还需要将 设置为 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute.AllowTransitiveGuestClients?displayProperty=nameWithType> `true` 。

> [!IMPORTANT]
> 中转服务的注册必须同时存在于Live Share主机上，以支持来宾从主机激活中转服务。
>
> 通过代理服务公开中转Live Share，请查看[如何保护中转服务](how-to-secure-brokered-service.md)。

## <a name="proffering-a-service"></a>提供服务

中转服务必须从 <xref:Microsoft.VisualStudio.Shell.AsyncPackage> 类进行缓冲，除非中转服务是通过 MEF 导出的，如如何提供中转 [服务中所述](how-to-provide-brokered-service.md)。

如果满足以下任一条件，则尝试提供中转服务会引发异常：

- 所缓冲服务的名字对象与已注册 (服务的) 名称和版本不完全匹配。
- 工厂已针对同一服务名字对象进行了缓冲。

对 的调用的结果是 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.IBrokeredServiceContainer.Proffer%2A?displayProperty=nameWithType> <xref:System.IDisposable>。
释放此值后，中转服务对新请求不可用。
当中转服务与某些上下文（如打开的解决方案）具有特定相关性时，可能适合仅在该上下文处于活动状态时提供中转服务。
释放包时，不需要保留和释放此值。

## <a name="tracing-rpc-between-client-and-service"></a>跟踪客户端和服务之间的 RPC

建立客户端和服务之间的连接后，跟踪其通信可能会很有用，尤其是在它们位于不同的进程中时。

默认情况下，跨进程的中转服务之间的通信跟踪 (因此 RPC) 在 目录中的 .svclog `%TEMP%\VSLogs` 文件中记录。
最好使用服务跟踪查看器查看 [这些 xml 文件](/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe#using-the-service-trace-viewer-tool)。
此工具可以一次打开多个 .svclog 文件，将它们拼结在一起形成一个多方图，使了解客户端和服务之间的 RPC 变得更加容易。

中转服务本身可以直接跟踪以添加到这些 .svclog 跟踪文件，进一步帮助诊断中转服务行为。
调用"报告 `%TEMP%\VSLogs` 问题"命令并且用户选择共享日志时，可能会收集保存到 的任何跟踪。

若要跟踪自己的消息，使消息易于发现并与其他 .svclog 跟踪组合在一起，代码 (中转服务) 是否可以执行如下所示操作：

```cs
// Define your log's ID, a namespace-like fully qualified name.
// In general it is expected that you follow you team's assembly namespace.
// Also an optional parameter, the ServiceMoniker for your service
var myLogId = new LogId("Microsoft.SomeTeam.MyLogName", serviceId: null);

var requestedLevel = new LoggingLevelSettings(SourceLevels.Warning | SourceLevels.ActivityTracing);
var myLogOptions = new LoggerOptions(requestedLevel, PrivacyFlags.MayContainPrivateInformation);

TraceSource myTraceSource;
using (TraceConfiguration traceConfig = await TraceConfiguration.CreateTraceConfigurationInstanceAsync(serviceBroker, ownsServiceBroker: false, cancellationToken))
{
    myTraceSource = await traceConfig.RegisterLogSourceAsync(myLogId, myLogOptions, traceSource: null, cancellationToken);
}
```

`myTraceSource`现在可以用于跟踪，因为它添加了相应的侦听器，用于将跟踪写入 .svclog 文件。
如果已有想要<xref:System.Diagnostics.TraceSource>使用的 <xref:Microsoft.VisualStudio.LogHub.TraceConfiguration.RegisterLogSourceAsync%2A> ，请将其传递给 方法并放弃结果，因为侦听器将添加到现有 。<xref:System.Diagnostics.TraceSource>

从为远程客户端服务的中转服务进行跟踪时，会自动将活动分配给运行代码的 ，该活动允许将 svclog 与客户端的 svclog 拼结在一起，以便使用服务跟踪查看器查看整体视图。[](/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe#using-the-service-trace-viewer-tool)<xref:System.Threading.ExecutionContext>

## <a name="see-also"></a>另请参阅
- [使用和提供中转服务](use-and-provide-brokered-services.md)
- [如何：获取中转服务](how-to-consume-brokered-service.md)
- [如何：提供中转服务](how-to-provide-brokered-service.md)
- [发现可用的中转服务](internals/discover-available-brokered-services.md)
