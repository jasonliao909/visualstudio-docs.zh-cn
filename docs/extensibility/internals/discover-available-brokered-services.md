---
title: 发现可用的中转服务
description: 发现 Visual Studio 和 Visual Studio SDK 支持的可用服务，包括用于获取每个服务的接口的服务描述符。
monikerRange: '>= vs-2019'
ms.custom: SEO-VS-2020
ms.date: 01/07/2022
ms.topic: reference
helpviewer_keywords:
- brokered services, Visual Studio
- Visual Studio, brokered services
ms.assetid: 724eb24b-b87c-4971-a2e7-adee7afc03b2
author: aarnott
ms.author: andarno
manager: ansonh
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a4b8ea8c41b4c543437a5ffba29d0aa462cb3dc0
ms.sourcegitcommit: 169b7b66d13b7e3c86097b42206dd33389cd9166
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2022
ms.locfileid: "138153486"
---
# <a name="discovering-available-brokered-services"></a>发现可用的中转服务

中转服务可以通过 或其 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 扩展公开。
本文档介绍如何发现 公开的中转服务 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

请参阅扩展的文档来发现自己的中转服务。

## <a name="visual-studio-services-class"></a>Visual Studio服务类

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]和 Visual Studio SDK 提供了许多中转服务。
这些服务都可以通过 通常 <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor> 可从 类获取的 来 <xref:Microsoft.VisualStudio.VisualStudioServices> 访问。

其他中转服务可能存在，并记录有特定  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 功能。

类 <xref:Microsoft.VisualStudio.VisualStudioServices> 为 的各种主要或次要版本声明静态属性 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。
其中每个属性都返回一个类的实例，该类声明公开 <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor> 中转服务的 的属性。
这样，就可以轻松发现特定版本的 支持的中转服务集 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

例如，中转解决方案服务 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 是在 2019 Update 5 中引入的。
可以使用 <xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor> 如下所示的代码从 VisualStudioServices.VS2019_5Services.SolutionService 获取此服务的 ：

```csharp
ServiceRpcDescriptor descriptor = Microsoft.VisualStudio.VisualStudioServices.VS2019_5.SolutionService;
```

## <a name="version-considerations"></a>版本注意事项

考虑到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 扩展面向的最低所需版本，扩展应该使用 类中的最新可用 VS <xref:Microsoft.VisualStudio.VisualStudioServices> 发布属性使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中转服务。
以前面的解决方案 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 服务示例为例，这意味着面向 2019 Update 9 或更高版本的扩展应从 VisualStudioServices.VS2019_9 属性获取 VisualStudioServices.VS2019_5Services.SolutionService 描述符。
让我们将上一个示例更新为以下代码：

```csharp
ServiceRpcDescriptor descriptor = Microsoft.VisualStudio.VisualStudioServices.VS2019_9.SolutionService;
```

从 的最新版本 <xref:Microsoft.VisualStudio.VisualStudioServices> 属性获取描述符可确保服务 RPC 尽可能高效，并且服务本身将提供最新行为。
更新扩展[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]<xref:Microsoft.VisualStudio.VisualStudioServices>[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]以需要较新版本时，请考虑查看 类的所有使用，并更新对描述符的引用，以使用最新版本的属性来匹配目标版本。

使用 的较<xref:Microsoft.ServiceHub.Framework.ServiceRpcDescriptor><xref:Microsoft.VisualStudio.VisualStudioServices>旧版本属性获取的中转服务可以模拟其行为，就像在旧版本中一样，包括可能重现异常行为或功能限制。

以 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 特定版本 为目标并[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]运行的扩展可能会请求中转服务，该服务最终通过特定连接Live Share激活。
在这种情况下，远程进程 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 可能运行与本地进程不同的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 版本。
当 Live Share 主机不提供所请求版本的中转服务时，Live Share来宾在 Live Share 会话期间对中转服务的请求可能会失败。

考虑在中转服务不可用时包括回退计划。
此回退计划可能包括从 <xref:Microsoft.VisualStudio.VisualStudioServices> 上的旧版本属性再次请求中转服务，因为如果 Live Share 主机是旧版本的 ，则可能会成功[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。
请记住，这样做时，服务接口的一些成员可能在服务实现本身上不可用。

即使寄送后 [，](../best-practices-design-brokered-service.md#AddingInterfaceMembers) 中转服务也可以将成员添加到其服务接口。
请注意接口的每个成员上的 IntelliSense 文档，查看该成员是否提及了所需的最低服务版本。

尝试调用远程服务实际未实现的成员将引发 <xref:StreamJsonRpc.RemoteMethodNotFoundException>。

## <a name="see-also"></a>另请参阅

- [使用和提供中转服务](../../extensibility/use-and-provide-brokered-services.md)
