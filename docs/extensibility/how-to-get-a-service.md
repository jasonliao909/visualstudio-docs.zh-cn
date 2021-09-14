---
title: 如何：获取服务|Microsoft Docs
description: 了解如何获取Visual Studio服务以访问不同的功能。 可以使用 VSPackage 获取大多数服务。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- services, consuming
ms.assetid: 1f000020-8fb7-4e39-8e1e-2e38c7fec3d4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 810211f79bd04bcba9b59dcf60e16e14d19bc702
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600771"
---
# <a name="how-to-get-a-service"></a>如何：获取服务

通常需要获取不同的Visual Studio才能访问不同的功能。 通常，Visual Studio服务提供了一个或多个可以使用的接口。 可以从 VSPackage 获取大多数服务。

派生自 且已正确进行站点化的任何 VSPackage <xref:Microsoft.VisualStudio.Shell.Package> 都可以请求任何全局服务。 由于 `Package` 类实现 <xref:System.IServiceProvider> ，因此派生自 的任何 VSPackage `Package` 也是服务提供商。

当 Visual Studio 加载 <xref:Microsoft.VisualStudio.Shell.Package> 时，它会在初始化过程中将 对象 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 传递给 方法。 这称为 *"托管* VSPackage"。 `Package`类包装此服务提供程序，并提供 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 获取服务的方法。

## <a name="getting-a-service-from-an-initialized-vspackage"></a>从初始化的 VSPackage 获取服务

1. 每个Visual Studio扩展都从 VSIX 部署项目开始，该项目将包含扩展资产。 创建名为 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的 VSIX 项目 `GetServiceExtension` 。 可以通过搜索"vsix"在"新建Project"找到 VSIX 项目模板。 

2. 现在，添加名为 **GetServiceCommand 的自定义命令项模板**。 在"**添加新项"对话框中**，转到 **"Visual C#**  >  **扩展性"，** 然后选择"**自定义命令"。** 在 **窗口底部的** "名称"字段中，将命令文件名更改为 *GetServiceCommand.cs*。 若要详细了解如何创建自定义命令，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

3. 在 *GetServiceCommand.cs* 中，删除 方法 `MenuItemCommand` 的主体并添加以下代码：

   ```csharp
   IVsActivityLog activityLog = ServiceProvider.GetService(typeof(SVsActivityLog)) as IVsActivityLog;
   if (activityLog == null) return;
   System.Windows.Forms.MessageBox.Show("Found the activity log service.");

   ```

    此代码获取 SVsActivityLog 服务，并强制转换到接口，该接口可用于 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> 写入活动日志。 有关示例，请参阅 [如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。

4. 生成项目并启动调试。 这将显示实验实例。

5. 在实验 **实例** 的"工具"菜单上，找到" **调用 GetServiceCommand"** 按钮。 单击此按钮时，应会看到一个消息框，显示" **找到活动日志服务"。**

## <a name="getting-a-service-from-a-tool-window-or-control-container"></a>从工具窗口或控件容器获取服务

有时，可能需要从尚未站点化的工具窗口或控制容器获取服务，或者已使用不知道所需的服务的服务提供商进行站点化。 例如，你可能想要从 控件内写入活动日志。

静态方法依赖于缓存的服务提供程序，该提供程序在首次对派生自 的任何 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> VSPackage 进行站点化时 <xref:Microsoft.VisualStudio.Shell.Package> 进行初始化。

由于 VSPackage 构造函数是在站点化 VSPackage 之前调用的，因此全局服务通常从 VSPackage 构造函数中不可用。 有关 [解决方法，请参阅如何：](../extensibility/how-to-troubleshoot-services.md) 对服务进行故障排除。

下面是在工具窗口或其他非 VSPackage 元素中获取服务的方法示例。

```csharp
IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;
if (log == null) return;
```

## <a name="getting-a-service-from-the-dte-object"></a>从 DTE 对象获取服务

还可以从 对象获取 <xref:EnvDTE.DTEClass> 服务。 但是，必须从 VSPackage 或调用静态方法获取 DTE 对象作为 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 服务。

DTE 对象实现 ，可用于通过使用 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 查询服务 <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> 。

下面是如何从 DTE 对象获取服务。

```csharp
// Start with the DTE object, for example: 
// using EnvDTE;
// DTE dte = (DTE)GetService(typeof(DTE));

ServiceProvider sp = new ServiceProvider((Microsoft.VisualStudio.OLE.Interop.IServiceProvider)dte);
if (sp != null)
{
    IVsActivityLog log = sp.GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log != null)
    {
        System.Windows.Forms.MessageBox.Show("Found the activity log service.");
    }
}
```

## <a name="see-also"></a>另请参阅

- [如何：提供服务](../extensibility/how-to-provide-a-service.md)
- [使用和提供服务](../extensibility/using-and-providing-services.md)
- [服务要素](../extensibility/internals/service-essentials.md)
