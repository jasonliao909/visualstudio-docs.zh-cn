---
title: 中转服务要素
description: 了解中转服务，这些服务为 VS 功能提供与 RPC 兼容的接口。
monikerRange: '>= vs-2019'
ms.custom: SEO-VS-2020
ms.date: 01/06/2022
ms.topic: conceptual
helpviewer_keywords:
- brokered services, essentials
ms.assetid: d2d4d867-0ba0-4e7e-8557-edbcb65d8400
author: aarnott
ms.author: andarno
manager: ansonh
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ebeeb00bf12b08d7bc17a4b68648073e9618b5bb
ms.sourcegitcommit: 169b7b66d13b7e3c86097b42206dd33389cd9166
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2022
ms.locfileid: "138153479"
---
# <a name="brokered-service-essentials"></a>中转服务要素

中转服务<xref:Microsoft.ServiceHub.Framework.IServiceBroker>是通过 获取的服务，作为与 RPC 兼容的接口公开，使服务及其客户端能够存在于不同的 AppDomain、进程甚至跨计算机 (（如果为 Live Share) ）。
中转服务可能来自主进程 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 或它的一些辅助进程，并且可能由这些进程的任何一个扩展使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

如 (和) [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] <xref:System.IServiceProvider>中所述，可通过 接口获取更多非中转[服务。](../using-and-providing-services.md)
此类服务通常仅在主进程中 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 可用，但公开的功能集比中转服务要大。

来宾[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]上运行的扩展Live Share访问由来宾主机提供的服务子集，以提供Live Share功能。
授权检查应用于Live Share连接，以降低来宾行为不良Live Share影响主机安全Live Share的风险。
选择通过服务公开其服务的中转服务的作者Live Share应负责实现授权检查，如如何提供中转[服务中所述](../how-to-provide-brokered-service.md)。

## <a name="service-broker"></a>服务代理

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 具有一个全局 <xref:Microsoft.ServiceHub.Framework.IServiceBroker>，类似于 (，并且从公开) <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GlobalProvider%2A> 服务的 中检索。
也可通过 MEF 检索它。

可能有其他更 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 特定于上下文的服务代理由特定功能提供，这些特定功能希望将全局代理与自己的一个功能聚合，以提供额外的服务 (或可能抑制某些) 。

是 <xref:Microsoft.ServiceHub.Framework.IServiceBroker> (有意) 一个黑盒，允许客户端获取可能位于本地、其他进程中或其他计算机上的服务。
服务代理可能是应用了策略的一个或多个其他代理的聚合。

根据进程所 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 位于的上下文，此全局 Service Broker 是一组不断变化的其他服务中转站的聚合。
进程中的上下文更改可能会更改可能激活的中转服务集。
例如，当加载解决方案时，与活动解决方案专门相关的服务可能会变得可用。
同一服务也可能在"打开文件夹"视图中提供，但使用不同的后备实现。
服务实现中的更改对于该服务的客户端是透明的，因为两个实现都必须满足相同的协定，但客户端需要在此上下文更改中重新查询服务 (<xref:Microsoft.ServiceHub.Framework.IServiceBroker.AvailabilityChanged> 通过) 通知他们获取新实例。

Service Broker 通常用于获取服务的代理。
也就是说，客户端接收一个存根，该存根不直接接收对服务对象的引用，而是将所有方法调用转发给服务，将结果或异常转发回客户端。
它还可能会将服务引发的事件转发给客户端。
在某些情况下，服务可能支持或要求客户端提供一个"目标对象"，服务可以调用 上的方法来调用回客户端。

## <a name="brokered-service-container"></a>中转服务容器

必须将服务缓冲到 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.IBrokeredServiceContainer> 中，才能从全局 提供 <xref:Microsoft.ServiceHub.Framework.IServiceBroker>。
此服务容器不仅负责向 Service Broker 公开服务工厂，还负责控制哪些客户端有权访问该服务，以及当对该服务的访问发生更改时通知这些客户端。

## <a name="composition-of-a-brokered-service"></a>中转服务的组合

中转服务由以下元素组成：

- 声明服务功能并充当服务及其客户端之间的协定的接口。
- 该接口的实现。
- 一 <xref:Microsoft.ServiceHub.Framework.ServiceMoniker> 个 ，用于为服务分配名称和版本。
- 一 <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor> 个 ，它将 <xref:Microsoft.ServiceHub.Framework.ServiceMoniker> 与用于在必要时处理 RPC 的行为组合在一起。
- 用于提供服务工厂的代码
- 服务注册

### <a name="service-interface"></a>服务接口

这可能是标准 .NET 接口 (用 C#) 。
若要允许中转服务客户端和服务存在于不同的进程中并通过 RPC <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor> 进行通信，此接口必须遵循服务将使用的 指定的限制。
这些限制通常包括不允许使用属性和索引器，并且大多数或所有方法返回 <xref:System.Threading.Tasks.Task> 或其他异步兼容的返回类型。

### <a name="brokered-service-monikers-and-descriptors"></a>中转服务名字对象和描述符

激活服务需要知道其名字对象。
由于名字对象包含在服务的描述符中，因此客户端通常只能处理 <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor>。
描述符添加在中转服务及其客户端之间设置 RPC 连接所需的行为，或在需要时序列化与 的 RPC 调用时的行为 <xref:System.IO.Stream>。

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 建议对中转 <xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor> 服务使用派生类型，当客户端和服务需要 RPC 进行通信时，使用 StreamJsonRpc 库。
StreamJsonRpc 对服务接口应用某些限制， [如下所述](https://github.com/microsoft/vs-streamjsonrpc/blob/main/doc/dynamicproxy.md)。

很少需要直接使用描述符。
相反，它通常从 或 <xref:Microsoft.VisualStudio.VisualStudioServices> 提供服务的库获取，然后用作 的参数 <xref:Microsoft.ServiceHub.Framework.IServiceBroker.GetProxyAsync%2A>。

和 类<xref:Microsoft.ServiceHub.Framework.ServiceMoniker><xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor>都是不可变的，因此可以安全地共享为字段`static readonly`或属性。
<xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor>任何其他派生类型都应是不可变的。

可 <xref:Microsoft.ServiceHub.Framework.ServiceMoniker> 序列化。
不可 <xref:Microsoft.ServiceHub.Framework.ServiceJsonRpcDescriptor> 序列化。

### <a name="service-audience"></a>服务受众

每个中转服务都使用 中的一系列标志进行注册 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience>。
这些标志控制将公开中转服务的客户端和连接。

典型的选择是 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience.Local?displayProperty=nameWithType>，它向会话中的任何本地进程公开 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 服务。
使用此设置时，即使实时共享会话处于活动状态，服务也始终在本地激活。

<xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience.LiveShareGuest?displayProperty=nameWithType>添加 标志时，Live Share中转服务的请求的来宾通过与托管主机的远程连接获取该中转Live Share代理。

在 上定义的任何标志组合 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience> 都是合法的。
可以在不同时设置 标志的情况下设置 标志，例如，仅向 Live Share 来宾公开中转服务 (从 Live Share 主机) 公开，并且永远不会在本地 (其中客户端和服务位于同一进程) 。<xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience.LiveShareGuest> <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience.Local>

<xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience.RemoteExclusiveServer>和 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience.RemoteExclusiveClient> 标志已弃用。

当客户端请求中转 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.ServiceAudience> 服务时，它不需要知道该服务的是什么，也不需要知道服务将激活在何处。
但是，对于服务记录此值以及使用服务的开发人员来说，了解服务可能激活在何处，以便他们可以预测各种上下文中可能来自该服务的数据类型以及服务何时可用，这可能很有用。

## <a name="composition-of-a-brokered-client"></a>中转客户端的组合

当客户端请求中转`null`<xref:Microsoft.ServiceHub.Framework.ServiceActivationFailedException>服务时，它要么在服务不可用时返回，要么在服务激活失败时引发 ，要么 *获取该服务的* 代理。
无论中转服务是在客户端的同一进程中激活还是在不同的进程中激活，都使用代理。
此代理有助于跨本地和远程服务案例使用模式，使客户端无需知道服务所在的位置。

## <a name="see-also"></a>另请参阅

- [发现可用的中转服务](discover-available-brokered-services.md)
- [使用和提供中转服务](../use-and-provide-brokered-services.md)
- [如何提供中转服务](../how-to-provide-brokered-service.md)。
- [如何获取中转服务](../how-to-consume-brokered-service.md)。
