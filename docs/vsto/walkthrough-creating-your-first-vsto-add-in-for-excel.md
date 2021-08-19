---
title: 演练：为 VSTO 创建第一个Excel
description: 为应用程序创建应用程序级外接程序Microsoft Excel。 无论打开哪些工作簿，你创建的功能都可供应用程序本身使用。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], creating your first project
- Office development in Visual Studio, creating your first project
- add-ins [Office development in Visual Studio], creating your first project
- Excel [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 4a3dedc8a954f278e1446667c0623ea7da5d6fa5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122147591"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-excel"></a>演练：为 VSTO 创建第一个Excel
  本介绍性演练演示如何创建 Microsoft Office Excel 的应用程序级外接程序。 你在此类解决方案中创建的功能可用于应用程序本身，而与所打开的工作簿无关。

 [!INCLUDE[appliesto_xlallapp](../vsto/includes/appliesto-xlallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 本演练演示以下任务：

- 为 Excel 创建 Excel VSTO 外接程序项目。

- 编写代码，使用 Excel 对象模型在保存工作簿时向工作簿中添加文本。

- 生成并运行项目，以对其进行测试。

- 清理已完成的项目，使 VSTO 外接程序在开发计算机上不再自动运行。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目

#### <a name="to-create-a-new-excel-vsto-add-in-project-in-visual-studio"></a>在 Visual Studio 中创建新的 Excel VSTO 外接程序项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在 **“文件”** 菜单上，指向 **“新建”** ，再单击 **“项目”** 。

3. 在模板窗格中，展开 **“Visual C#”** 或 **“Visual Basic”**，然后展开 **“Office/SharePoint”**。

4. 在展开的 **“Office/SharePoint”** 节点下方，选择 **“Office 外接程序”** 节点。

5. 在项目模板列表中，选择 **“Excel 2010 外接程序”** 或 **“Excel 2013 外接程序”**。

6. 在 **“名称”** 框中，键入 **FirstExcelAddIn**。

7. 单击“确定”。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建 **FirstExcelAddIn** 项目，并打开编辑器中的 ThisAddIn 代码文件。

## <a name="write-code-to-add-text-to-the-saved-workbook"></a>编写代码以将文本添加到保存的工作簿
 接下来，将代码添加到 ThisAddIn 代码文件。 新的代码使用 Excel 的对象模型将样本文本插入到活动工作表的第一行。 活动工作表是用户保存工作簿时处于打开状态的工作表。 默认情况下，ThisAddIn 代码文件包含以下生成的代码：

- `ThisAddIn` 类的部分定义。 此类提供代码的入口点，并提供对 Excel 对象模型的访问权限。 有关详细信息，请参阅[Program VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。类的其余部分在不应 `ThisAddIn` 修改的隐藏代码文件中定义。

- `ThisAddIn_Startup` 和 `ThisAddIn_Shutdown` 事件处理程序。 Excel 加载和卸载 VSTO 外接程序时会调用这些事件处理程序。 使用这些事件处理程序，可在加载 VSTO 外接程序对其进行初始化，并在卸载时清理外接程序所使用的资源。 有关详细信息，请参阅[项目中Office事件](../vsto/events-in-office-projects.md)。

### <a name="to-add-a-line-of-text-to-the-saved-workbook"></a>向保存的工作簿中添加一行文本

1. 在 ThisAddIn 代码文件中，将下面的代码添加到 `ThisAddIn` 类中。 新的代码定义 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> 事件的事件处理程序，该事件在保存工作簿时引发。

    用户保存工作簿时，该事件处理程序会将新文本添加到活动工作簿的开头。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelAddInTutorial/ThisAddIn.vb" id="Snippet1":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelAddInTutorial/ThisAddIn.cs" id="Snippet1":::

2. 如果你使用的是 C#，请将以下必需代码添加到 `ThisAddIn_Startup` 事件处理程序中。 此代码用于将 `Application_WorkbookBeforeSave` 事件处理程序与 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> 事件连接在一起。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelAddInTutorial/ThisAddIn.cs" id="Snippet2":::

   为了在保存工作簿后对其进行修改，前面的代码示例使用了以下对象：

- `Application` 类的 `ThisAddIn` 字段。 `Application` 字段返回一个 <xref:Microsoft.Office.Interop.Excel.Application> 对象，该对象表示 Excel 的当前实例。

- `Wb` 事件的事件处理程序的 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> 参数。 `Wb` 参数是一个 <xref:Microsoft.Office.Interop.Excel.Workbook> 对象，用于表示已保存的工作簿。 有关详细信息，请参阅对象[Excel概述](../vsto/excel-object-model-overview.md)。

## <a name="test-the-project"></a>测试项目

### <a name="to-test-the-project"></a>测试项目

1. 按 **F5** 生成并运行项目。

     生成项目时，代码会编译成一个程序集，此程序集包含在项目的生成输出文件夹中。 Visual Studio 还会创建一组注册表项，通过这些注册表项，Excel 能够发现和加载 VSTO 外接程序，Visual Studio 还将开发计算机上的安全设置配置为允许 VSTO 外接程序运行。 有关详细信息，请参阅生成[Office解决方案](../vsto/building-office-solutions.md)。

2. 在 Excel 中，保存工作簿。

3. 验证下面的文本是否已添加到工作簿中。

     **This text was added by using code.**

4. 关闭 Excel。

## <a name="clean-up-the-project"></a>清理项目
 完成项目开发后，请从开发计算机上删除 VSTO 外接程序程序集、注册表项和安全设置。 否则，每次在开发计算机上打开 Excel 时，VSTO 外接程序都将继续运行。

### <a name="to-clean-up-the-completed-project-on-your-development-computer"></a>在开发计算机上清理已完成的项目

1. 在 Visual Studio 中，在 **“生成”** 菜单上，单击 **“清理解决方案”**。

## <a name="next-steps"></a>后续步骤
 既然你已经创建了一个基本的 Excel VSTO 外接程序，就可以从下面这些主题中了解有关如何开发外 VSTO 加载项的详细信息：

- 可以在外接程序中执行VSTO常规编程任务：VSTO[外接程序 。](../vsto/programming-vsto-add-ins.md)

- 特定于外接程序的编程Excel VSTO任务：Excel[解决方案](../vsto/excel-solutions.md)。

- 使用 对象模型[Excel：Excel对象模型概述](../vsto/excel-object-model-overview.md)。

- 自定义 (UI) 用户界面Excel，例如，将自定义选项卡添加到功能区或创建自己的自定义任务窗格：Office [UI 自定义](../vsto/office-ui-customization.md)。

- 生成和调试VSTO的外接程序：Excel[生成Office解决方案](../vsto/building-office-solutions.md)。

- 为 VSTO 部署外接程序[Excel：部署Office解决方案](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>请参阅
- [Office解决方案开发概述&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [Excel解决方案](../vsto/excel-solutions.md)
- [程序VSTO外接程序](../vsto/programming-vsto-add-ins.md)
- [Excel对象模型概述](../vsto/excel-object-model-overview.md)
- [OfficeUI 自定义](../vsto/office-ui-customization.md)
- [生成Office解决方案](../vsto/building-office-solutions.md)
- [部署Office解决方案](../vsto/deploying-an-office-solution.md)
- [Office项目模板概述](../vsto/office-project-templates-overview.md)
