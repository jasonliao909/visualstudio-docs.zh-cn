---
title: 使用扩展性接口自定义 UI 功能
description: 了解中Office开发工具Visual Studio提供扩展性接口来帮助你自定义 UI 功能。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ICustomTaskPaneConsumer interface
- IRibbonExtensibility interface
- UI customizing [Office development in Visual Studio]
- user interfaces [Office development in Visual Studio], customizing
- application-level add-ins [Office development in Visual Studio], extensibility interfaces
- customizing UI features [Office development in Visual Studio]
- FormRegionStartup interface
- add-ins [Office development in Visual Studio], extensibility interfaces
- extensibility interfaces [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 4e4c37a90774cdbd148900a8df9ddb6b3d58bb1c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122106531"
---
# <a name="customize-ui-features-by-using-extensibility-interfaces"></a>使用扩展性接口自定义 UI 功能
  Visual Studio 中的 Office 开发工具提供了一些类和设计器，使用它们在 VSTO 外接程序中创建自定义任务窗格、功能区自定义项和 Outlook 窗体区域时可处理许多实现细节。 不过，如果你有特殊要求，也可以自己为每项功能实现 *扩展性接口* 。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

## <a name="overview-of-extensibility-interfaces"></a>扩展性接口概述
 Microsoft Office 定义了一组扩展性接口，COM VSTO 外接程序可通过实现这些接口来自定义某些功能，例如功能区。 这些接口完全控制可通过其访问的功能。 不过，实现这些接口需要掌握一些有关托管代码中的 COM 互操作性的知识。 在某些情况下，对于熟悉 .NET Framework 的开发人员而言，这些接口的编程模型也并不直观。

 使用 Visual Studio 中的 Office 项目模板创建 VSTO 外接程序时，不必实现扩展性接口来自定义功能区之类的功能。 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 可为你实现这些接口。 相反，你可以使用 Visual Studio 提供的更为直观的类和设计器。 不过，只要你愿意，你仍然可以直接在 VSTO 外接程序中实现扩展性接口。

 有关为这些功能提供的Visual Studio和设计器的详细信息，[请参阅自定义任务](../vsto/custom-task-panes.md)窗格、功能区设计器 和[创建Outlook窗体区域](../vsto/creating-outlook-form-regions.md)。 [](../vsto/ribbon-designer.md)

## <a name="extensibility-interfaces-you-can-implement-in-a-vsto-add-in"></a>可以在外接程序中VSTO扩展性接口
 下表列出了你可以实现的扩展性接口以及支持这些接口的应用程序。

|接口|说明|应用程序|
|---------------|-----------------|------------------|
|<xref:Microsoft.Office.Core.IRibbonExtensibility>|实现此接口可自定义功能区 UI。 **注意：** 可以将功能区 **(XML)** 项添加到项目，以在外接程序VSTO <xref:Microsoft.Office.Core.IRibbonExtensibility> 生成默认实现。 有关更多信息，请参见 [Ribbon XML](../vsto/ribbon-xml.md)。|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)]<br /><br /> InfoPath 2010<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Project<br /><br /> Visio<br /><br /> Word|
|<xref:Microsoft.Office.Core.ICustomTaskPaneConsumer>|实现此接口可创建自定义任务窗格。|Excel<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> 单词|
|<xref:Microsoft.Office.Interop.Outlook.FormRegionStartup>|实现此接口可创建 Outlook 窗体区域。|Outlook|

 Microsoft Office 还定义了其他一些扩展性接口，例如 <xref:Microsoft.Office.Core.IBlogExtensibility>、 <xref:Microsoft.Office.Core.EncryptionProvider>和 <xref:Microsoft.Office.Core.SignatureProvider>。 Visual Studio 不支持在使用 Office 项目模板创建的 VSTO 外接程序中实现这些接口。

## <a name="use-extensibility-interfaces"></a>使用扩展性接口
 要使用扩展性接口自定义 UI 功能，请在 VSTO 外接程序项目中实现相应的接口。 然后，重写 <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> 方法以返回实现该接口的类的实例。

 有关演示如何在 VSTO for Outlook 外接程序中实现 、 和 接口的示例应用程序，请参阅 Office 开发示例中的 UI 管理器 <xref:Microsoft.Office.Core.IRibbonExtensibility> <xref:Microsoft.Office.Core.ICustomTaskPaneConsumer> <xref:Microsoft.Office.Interop.Outlook.FormRegionStartup> [示例](../vsto/office-development-samples.md)。

### <a name="example-of-implementing-an-extensibility-interface"></a>实现扩展性接口的示例
 下面的代码示例演示用于创建自定义任务窗格的 <xref:Microsoft.Office.Core.ICustomTaskPaneConsumer> 接口的简单实现。 此示例定义两个类：

- `TaskPaneHelper` 类实现 <xref:Microsoft.Office.Core.ICustomTaskPaneConsumer> 以创建和显示自定义任务窗格。

- `TaskPaneUI` 类提供任务窗格的 UI。 `TaskPaneUI` 类的属性使类对于 COM 可见，从而使 Microsoft Office 应用程序能够发现该类。 在此示例中，UI 是一个空 <xref:System.Windows.Forms.UserControl>，但你可以通过修改代码来添加控件。

  > [!NOTE]
  > 要向 COM 公开 `TaskPaneUI` 类，你必须同时为项目设置“为 COM 互操作注册”  属性。

  :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_SimpleExtensibilityInterface/ThisAddIn.vb" id="Snippet1":::
  :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_SimpleExtensibilityInterface/ThisAddIn.cs" id="Snippet1":::

  有关实现 的详细信息，请参阅 <xref:Microsoft.Office.Core.ICustomTaskPaneConsumer> [2007](/previous-versions/office/developer/office-2007/aa338197(v=office.12)) Office 文档中的"创建自定义Microsoft Office窗格。

### <a name="example-of-overriding-the-requestservice-method"></a>重写 RequestService 方法的示例
 下面的代码示例演示如何重写 <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> 方法以从前面的代码示例中返回 `TaskPaneHelper` 类的实例。 它将检查 *serviceGuid* 参数的值以确定请求的是哪个接口，然后返回实现该接口的对象。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_SimpleExtensibilityInterface/ThisAddIn.vb" id="Snippet2":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_SimpleExtensibilityInterface/ThisAddIn.cs" id="Snippet2":::

## <a name="see-also"></a>请参阅
- [Office开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [程序VSTO外接程序](../vsto/programming-vsto-add-ins.md)
- [开发Office解决方案](../vsto/developing-office-solutions.md)
- [从其他 VSTO 解决方案调用外接程序Office代码](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)
- [如何：在 Office 创建Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
