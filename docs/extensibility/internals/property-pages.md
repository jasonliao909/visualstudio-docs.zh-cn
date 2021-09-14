---
title: 属性页|Microsoft Docs
description: 了解如何在 Visual Studio SDK 中为新项目类型使用"属性页"，从而允许用户查看和更改项目属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- configuration options, changing properties
- property pages
- property pages, changing configuration options
ms.assetid: b9b3e6e8-1e30-4c89-9862-330265dcf38c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 63660d52f6b5707d4e667da07e5d4ccfa38dae7d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602560"
---
# <a name="property-pages"></a>属性页
用户可以使用属性页查看和更改与项目配置相关的和独立的属性。 "**属性页**"按钮在"属性"窗口或解决方案资源管理器工具栏上为提供所选对象的属性页视图的对象启用。 属性页由环境创建，可用于解决方案和项目。 但是，它们还可用于使用配置依赖属性的项目项。 当项目中的文件需要不同的编译器开关设置以正确生成时，可能会使用此功能。

## <a name="using-property-pages"></a>使用属性页
 如果属性页已显示，并且选择 (例如，从解决方案更改到项目) ，则页面中显示的信息会更改以显示新选择的属性。 如果对象上没有支持属性页的属性，则属性页为空。

 如果选择了多个对象，则属性页将显示所有选定项的属性交集。 如果所选项不包含与配置相关的属性，并且单击了解决方案资源管理器工具栏上的"属性页"按钮，则焦点将属性窗口。 有关属性和选择属性窗口，请参阅扩展 [属性](../../extensibility/internals/extending-properties.md)。

 如果为多个对象显示属性，并且你在属性页上更改了值，则对象的所有值都设置为新值，即使它们最初不同，并且显示单个对象的属性时页为空。

 中提供了两种常规类型的 **ProjectProperty Pages** 对话框 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 例如，对于Visual Basic，属性页使用字段格式显示，如以下屏幕截图所示。 在本部分稍后显示的第二个中，属性页承载的属性网格类似于在"属性窗口"中发现的属性网格。

 ![Visual Basic字段格式](../../extensibility/internals/media/vsvbproppages.gif "vsVBPropPages")Project树结构的"属性页"对话框中的"属性页"

 "属性页"对话框中的树结构不是使用 构建的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 。 环境基于 和 接口传递给它的级别名称 <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages> <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage> 来生成它。

 属性页上只有两个顶级 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 类别可用：

- 通用属性，显示所选对象与配置无关的信息。 因此，选择其中一个"通用属性"子类别时，对话框顶部的"配置配置服务器"和"配置"选项将不可用。

- 配置属性，其中包含与解决方案或项目的调试、优化和生成参数相关的配置相关信息。

  无法创建任何其他顶级类别，但可以选择不在 的实现中显示其中一个 `IVsPropertyPage` 类别。 例如，如果没有为对象显示任何与配置无关的属性，可以选择不显示"通用属性"类别。 如果在配置对象中实现时从项的浏览对象和配置属性实现，则显示"通用属性" (实现 、 和相关接口的 `ISpecifyPropertyPages` `ISpecifyPropertyPages` `IVsCfg` `IVsProjectCfg`) 。

  在顶级类别下显示的每个类别都表示单独的属性页。 对话框中可用的类别和子类别条目由 和 的实现 `ISpecifyPropertyPages` 确定 `IVsPropertyPage` 。

  `IDispatch` 选择容器中的项的 对象，这些项具有要显示在属性页上实现以 `ISpecifyPropertyPages` 枚举类 ID 列表的属性。 类 ID 作为变量传递给 ，用于 `ISpecifyPropertyPages` 实例化属性页。 类的 ID 列表也会传递到 ， `IVsPropertyPage` 以创建对话框左侧的树结构。 然后，属性页将信息传递回实现的对象，并 `IDispatch` `ISpecifyPropertyPages` 填写每页的信息。

  对于选择容器中的每个对象，使用 `IDispatch` 检索浏览对象的属性。

  在 `Help::DisplayTopicFromF1Keyword` VSPackage 中实现 可提供"帮助"按钮的功能。

  有关详细信息，请参阅 `IDispatch` `ISpecifyPropertyPages` MSDN 库中的 和 。

  示例中显示的第二种类型的属性页承载属性网格的一种形式，如以下屏幕截图所示。

  ![VC 属性页](../../extensibility/internals/media/vsvcproppages.gif "vsVCPropPages") 包含属性网格的"属性页"对话框

  vsmanaged.h (中声明的接口和) 用于在对话框或窗口中创建和填充 `IVSMDPropertyBrowser` `IVSMDPropertyGrid` 属性网格。

  项目的体系结构与以前版本的 发生了很大的变化 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 具体而言，哪个项目处于活动状态的概念已更改。 在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中，没有活动项目的概念。 在以前的开发环境中，活动项目是生成和部署命令的项目默认为 ，而不考虑上下文。 现在，解决方案控制和配置哪些生成和部署命令适用于哪些项目。

  以前的活动项目现在以以下三种不同方式之一捕获：

- 启动项目

   可以从解决方案的属性页指定一个或多个项目，当用户按 F5 或从"生成"菜单中选择"运行"时，将启动该项目。 其工作方式类似于旧活动项目，即其名称以粗体解决方案资源管理器显示。

   可以通过调用 来检索启动项目作为自动化模型中的属性 `DTE.Solution.SolutionBuild.StartupProjects` 。 在 VSPackage 中，调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> 或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> 方法。 `IVsSolutionBuildManager` 作为服务在 `QueryService` SID_SVsSolutionBuildManager。 有关详细信息，请参阅配置[Project和](../../extensibility/internals/project-configuration-object.md)[解决方案配置](../../extensibility/internals/solution-configuration.md)。

- 活动解决方案生成配置

   [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 具有一个活动解决方案配置，通过实现 在自动化模型中可用 `DTE.Solution.SolutionBuild.ActiveConfiguration` 。 解决方案配置是一个集合，其中包含解决方案中每个项目的一个项目配置 (每个项目可以在多个平台上具有多个配置，但名称) 。 有关解决方案的属性页详细信息，请参阅解决方案 [配置](../../extensibility/internals/solution-configuration.md)。

- Project选定

   实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A> 方法以检索所选项目层次结构和项目项。 在 DTE 中，将使用 `SelectedItems.SelectedItem.Project` 和 `SelectedItems.SelectedItem.ProjectItem` 方法。 核心文档中这些标题下有示例 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 代码。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [项目配置对象](../../extensibility/internals/project-configuration-object.md)
- [解决方案配置](../../extensibility/internals/solution-configuration.md)
