---
title: Service Essentials |Microsoft Docs
description: 了解服务，这些服务是供另一个 VSPackage 使用的接口。 VSPackage 中的服务可以替代内置或其他服务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, essentials
ms.assetid: fbe84ad9-efe1-48b1-aba3-b50b90424d47
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 66b5689c2212104608361ccc07a799051e4627eb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600865"
---
# <a name="service-essentials"></a>服务基础知识
服务是两个 VSPackage 之间的协定。 一个 VSPackage 提供一组特定的接口供另一个 VSPackage 使用。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 本身是 VSPackage 的集合，它向其他 VSPackage 提供服务。

 例如，可以使用 SVsActivityLog 服务获取 IVsActivityLog 接口，该接口可用于写入活动日志。 有关详细信息，请参阅 [如何：使用活动日志](../../extensibility/how-to-use-the-activity-log.md)。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 还提供一些未注册的内置服务。 VSPackage 可以通过提供服务替代来替换内置或其他服务。 任何服务只允许一个服务重写。

 服务没有可发现性。 因此，必须知道 (SID) 的服务标识符，并且必须知道该服务提供的接口。 服务的参考文档提供了此信息。

- 提供服务的 VSPackage 称为"服务提供商"。

- 提供给其他 VSPackage 的服务称为全局服务。

- 仅可用于实现这些服务的 VSPackage 或它创建的任何对象的服务称为本地服务。

- 替换内置服务或由其他包提供的服务称为服务替代。

- 服务或服务替代按需加载，即当服务提供程序提供的服务由另一个 VSPackage 请求时加载。

- 为了支持按需加载，服务提供商使用 注册其全局服务 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 有关详细信息，请参阅 [如何：提供服务](../../extensibility/how-to-provide-a-service.md)。

- 获取服务后，使用 [QueryInterface](/cpp/atl/queryinterface) (非托管) 或强制转换 (托管) 以获取所需的接口，例如：

  ```vb
  TryCast(GetService(GetType(SVsActivityLog)), IVsActivityLog)
  ```

  ```csharp
  GetService(typeof(SVsActivityLog)) as IVsActivityLog;
  ```

- 托管代码按类型引用服务，而非托管代码按 GUID 引用服务。

- 加载 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage 时，它会将服务提供商传递给 VSPackage，使 VSPackage 能够访问全局服务。 这称为"正在"VSPackage。

- VSPackage 可以是所创建对象的服务提供商。 例如，窗体可能会向其框架发送颜色服务请求，这可能将请求传递给 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- 深度嵌套或完全未站点化托管对象可能要求 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 直接访问全局服务。

<a name="how-to-use-getglobalservice"></a>

## <a name="use-getglobalservice"></a>使用 GetGlobalService

有时，可能需要从尚未站点化的工具窗口或控制容器获取服务，或者已使用不知道所需的服务的服务提供商进行站点化。 例如，你可能想要从 控件内写入活动日志。 有关这些方案和其他方案的信息，请参阅 [如何：排查服务问题](../../extensibility/how-to-troubleshoot-services.md)。

可以通过调用静态Visual Studio获取大多数服务 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 。

<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 依赖于在首次对派生自 Package 的任何 VSPackage 进行站点化时初始化的缓存服务提供程序。 必须保证满足此条件，否则为 null 服务做好准备。

幸运的是， <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 大多数情况下都正常工作。

- 如果 VSPackage 提供的服务仅由另一个 VSPackage 知道，则请求该服务的 VSPackage 在加载提供服务之前会进行站点处理。

- 如果工具窗口是由 VSPackage 创建的，则 VSPackage 在工具窗口创建之前会进行站点设置。

- 如果控件容器由 VSPackage 创建的工具窗口承载，则 VSPackage 将先进行站点化，然后再创建控件容器。

### <a name="to-get-a-service-from-within-a-tool-window-or-control-container"></a>从工具窗口或控件容器中获取服务

- 在构造函数、工具窗口或控件容器中插入此代码：

    ```csharp
    IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;
        if (log == null) return;
    ```

    ```vb
    Dim log As IVsActivityLog = TryCast(Package.GetGlobalService(GetType(SVsActivityLog)), IVsActivityLog)
    If log Is Nothing Then
        Return
    End If
    ```

    此代码获取 SVsActivityLog 服务，并强制转换到 IVsActivityLog 接口，该接口可用于写入活动日志。 有关示例，请参阅 [如何：使用活动日志](../../extensibility/how-to-use-the-activity-log.md)。

## <a name="see-also"></a>另请参阅

- [可用服务的列表](../../extensibility/internals/list-of-available-services.md)
- [使用并提供服务](../../extensibility/using-and-providing-services.md)
- [强制转换和类型转换](/dotnet/csharp/programming-guide/types/casting-and-type-conversions)
- [强制转换](/cpp/cpp/casting)
