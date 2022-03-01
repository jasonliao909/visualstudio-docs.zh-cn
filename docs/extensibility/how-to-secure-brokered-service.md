---
title: 如何：保护中转服务
description: 了解如何保护中转服务，以在服务上Live Share。
monikerRange: '>= vs-2019'
ms.custom: SEO-VS-2020
ms.date: 01/11/2022
ms.topic: how-to
helpviewer_keywords:
- brokered services, providing
ms.assetid: c766c23d-3768-44ec-b778-c323369ac40d
author: aarnott
ms.author: andarno
manager: ansonh
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: bd5691a881f349409bdaa65a8e959a6c2a0e7c78
ms.sourcegitcommit: 169b7b66d13b7e3c86097b42206dd33389cd9166
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2022
ms.locfileid: "138153483"
---
# <a name="how-to-secure-a-brokered-service"></a>如何：保护中转服务

中转服务默认仅对本地用户以及 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 激活它的会话所涉及的进程可用。
在这些默认值下，中转服务的安全注意事项与在这些进程中运行的其他代码没有什么不同，其中包括：

- 从威胁模型的角度来看，在进程中运行的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 扩展假定是完全受信任的。 进程外扩展应该将Visual Studio调用视为跨越信任边界。
- 代码必须验证入口点的参数，以确认它们属于预期模式/范围。
- 从磁盘读取数据时，请考虑数据可能已被篡改。
- 从网络或 Internet 接收数据时，在分析或反数据时请谨慎，以避免常见漏洞。

向标志集注册服务时，有几个重要的其他安全 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute.AllowTransitiveGuestClients?displayProperty=nameWithType> 注意事项适用。
本文的其余部分重点介绍这些注意事项。

## <a name="authorization-checks-for-sensitive-operations"></a>针对敏感操作的授权检查

### <a name="acquiring-the-authorization-service"></a>获取授权服务

中转服务应具有采用 作为参数 <xref:Microsoft.ServiceHub.Framework.Services.AuthorizationServiceClient> 的构造函数。
参数应存储在 字段中，并释放在服务的 方法 <xref:System.IDisposable.Dispose> 中。

```csharp
class Calculator : ICalculator, IDisposable
{
    private readonly AuthorizationServiceClient authorizationService;

    internal Calculator(AuthorizationServiceClient authorizationService)
    {
        this.authorizationService = authorizationService;
    }

    public void Dispose()
    {
        this.authorizationService.Dispose();
    }
}
```

为支持此新参数，你稍微更改了一些服务工厂。
请提供委托 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.BrokeredServiceFactory> ， <xref:Microsoft.VisualStudio.Shell.ServiceBroker.IBrokeredServiceContainer.Proffer%2A?displayProperty=nameWithType> 而不是向方法提供 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.AuthorizingBrokeredServiceFactory> 。
此委托接收 <xref:Microsoft.ServiceHub.Framework.Services.AuthorizationServiceClient> 需要传递给中转服务的 。

对 proffer 代码的此更改可能如下所示：

```diff
 container.Proffer(
     CalculatorService,
-    (moniker, options, serviceBroker, cancellationToken) => new ValueTask<object?>(new CalculatorService()));
+    (moniker, options, serviceBroker, authorizationService, cancellationToken) => new ValueTask<object?>(new CalculatorService(authorizationService)));
```

### <a name="using-the-authorization-service"></a>使用授权服务

任何可能会泄露敏感信息或更改用户状态的操作都应使用 在授权服务中进行检查 <xref:Microsoft.ServiceHub.Framework.Services.AuthorizationServiceClient.AuthorizeOrThrowAsync%2A?displayProperty=nameWithType>。

若要断言调用方是代码的所有者 (标识与 Live Share 主机) 的运算符相同，则可能会使用以下代码：

```csharp
private static readonly ProtectedOperation ClientIsOwner = WellKnownProtectedOperations.CreateClientIsOwner();

public ValueTask ResetOperationCounterAsync(CancellationToken cancellationToken)
{
    // Resetting the counter should only be allowed if the user is the owner.
    await this.authorizationService.AuthorizeOrThrowAsync(ClientIsOwner, cancellationToken);

    // Proceed with the operation.
    this.operationCounter = 0;
}
```

其他各种授权级别在 类中 <xref:Microsoft.VisualStudio.RpcContracts.WellKnownProtectedOperations> 定义。

当服务客户端在同一台计算机和用户帐户中运行时，始终批准所有授权检查。
它们也全部获得批准，Live Share与主机在同一个Microsoft 帐户下运行。

当请求的操作未 *获得授权* 时， <xref:Microsoft.ServiceHub.Framework.Services.AuthorizationServiceClient.AuthorizeOrThrowAsync%2A> 将引发 <xref:System.UnauthorizedAccessException>。
Live Share主机<xref:Microsoft.ServiceHub.Framework.Services.ProtectedOperation>可能会通知所有者失败的尝试，如果识别 ，则主机有机会授予完成该操作所需的权限，以便客户端的后续尝试可能会成功。

在本地 <xref:Microsoft.ServiceHub.Framework.Services.AuthorizationServiceClient> 缓存所有授权检查，以便快速执行重复的授权检查。
例如，如果用户的权限集发生更改 (，Live Share主机更改来宾) 的权限，则会自动刷新本地缓存。

## <a name="consuming-other-brokered-services"></a>使用其他中转服务

当中转服务本身需要访问另一个中转服务 <xref:Microsoft.ServiceHub.Framework.IServiceBroker> 时，它应使用提供给其服务工厂的 。
它 *不应* 使用全局 Service Broker，因为不知道此特定中转服务实例的上下文及其客户端必须激活和调用其他行为的授权。

如果计算器服务需要其他中转服务来实现其行为，我们将修改 构造函数以接受 <xref:Microsoft.ServiceHub.Framework.IServiceBroker>：

```csharp
internal class Calculator : ICalculator
{
    private readonly IServiceBroker serviceBroker;
    private readonly AuthorizationServiceClient authorizationService;

    internal class Calculator(IServiceBroker serviceBroker, AuthorizationServiceClient authorizationService)
    {
        this.serviceBroker = serviceBroker;
        this.authorizationService = authorizationService;
    }
}
```

此附加参数将影响服务工厂的缓冲代码：

```diff
 container.Proffer(
     CalculatorService,
     (moniker, options, serviceBroker, authorizationService, cancellationToken)
-        => new ValueTask<object?>(new CalculatorService(authorizationService)));
+        => new ValueTask<object?>(new CalculatorService(serviceBroker, authorizationService)));
```

### <a name="limited-brokered-service-availability"></a>有限的中转服务可用性

如果中转服务的客户端是 Live Share 来宾 (与主机) <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute.AllowTransitiveGuestClients> 的所有者位于不同的帐户下，则上下文服务代理将仅激活其他已设置 标志作为安全预防措施的中转服务。
尝试激活不符合资格的中转服务将引发 <xref:System.UnauthorizedAccessException>。

<xref:Microsoft.VisualStudio.Shell.ServiceBroker.ProvideBrokeredServiceAttribute.AllowTransitiveGuestClients>如果中转服务需要另一个缺少 标志的中转服务，可以使用全局 Service Broker 来获取它，但必须考虑从该服务获取的中转服务不知道不受信任的来宾是最终客户端。
应遵循下一部分中有关调用其他 VS 服务或其他 API 的所有相同预防措施。

详细了解如何 [使用中转服务](how-to-consume-brokered-service.md)。

## <a name="consuming-other-vs-services-or-other-apis"></a>使用其他 VS 服务或其他 API

在向 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] Live Share 来宾公开的中转服务中允许调用标准服务、第三方库或标准 .NET API，但应仔细编写此类调用，并首先验证所有输入。

应仔细检查文件路径或 URL，以确保它们有效，并且位于来宾有权访问的预期子路径内。
例如，如果中转服务允许基于路径读取或写入文件，应检查路径是否位于打开的解决方案下，并且来宾实际上具有写入权限（如果适用）。
正确验证文件路径可能很难 `..` 考虑和其他方法，使其看起来像以正确的前缀开头的路径，但随后转义允许的解决方案目录。

在调用未 <xref:Microsoft.ServiceHub.Framework.Services.AuthorizationServiceClient> 内置有其自己的权限检查的任何 API 之前，请根据情况使用上述部分中所述的 来断言客户端具有权限。
**只应假定内置于 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]** 中的中转服务包含其自己的授权检查，这依赖于使用上下文服务代理获取这些中转服务，如上一部分所述。

所有其他 API[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]（包括使用全局 Service Broker 获取的非中转服务或中转服务）可能在你指示它们时执行，而不考虑 Live Share 来宾的权限级别，因此你自己的授权检查对于保护 Live Share 主机的安全性至关重要。

避免从中转服务公开另一个 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中转服务已公开的功能，因为它会增加攻击面。

## <a name="sharing-state-across-brokered-service-instances"></a>跨中转服务实例共享状态

当中转服务需要跨服务的多个实例共享状态时，此数据可能会向具有不同权限集的多个用户公开。
对于中转服务来说，保护这些用户的数据至关重要。
使用 [STRIDE 模型](/azure/security/develop/threat-modeling-tool-threats#stride-model) 来帮助识别、分类并最终缓解威胁。

你可以决定将共享状态视为受信任状态，因此授予其执行在内部所需的任何操作的权限 (例如访问 VS 服务或使用全局 service Broker) 。
在这种情况下，单个中转服务实例应负责保护对共享状态进行调用，以确保所有输入都适合使用授权服务授予其自己的用户权限。

此[Microsoft Threat Modeling Tool](/azure/security/develop/threat-modeling-tool)是一个有用的工具，用于保护共享状态和用户。

## <a name="see-also"></a>另请参阅
- [安全开发概述](/azure/security/develop/secure-dev-overview)
- [如何：提供中转服务](how-to-provide-brokered-service.md)
- [设计中转服务最佳做法](best-practices-design-brokered-service.md)
- [中转服务 Essentials](internals/brokered-service-essentials.md)
- [使用和提供中转服务](use-and-provide-brokered-services.md)
