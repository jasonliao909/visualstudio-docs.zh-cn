---
title: 为 Word 创建第一个文档级自定义项
description: 为文档级自定义项创建Microsoft Word。 仅在特定文档处于打开状态时，才可提供你在这种解决方案中创建的功能。
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, creating your first project
- Word [Office development in Visual Studio], creating your first project
- document-level customizations [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 7c039abd3a6637afe56e80164cb3add830dc44ea
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122155470"
---
# <a name="walkthrough-create-your-first-document-level-customization-for-word"></a>演练：为 Word 创建第一个文档级自定义项

  本介绍性演练演示了如何创建 Microsoft Office Word 的文档级自定义项。 仅在特定文档处于打开状态时，才可提供你在这种解决方案中创建的功能。 不能使用文档级自定义项进行应用程序范围的更改，例如在任何文档处于打开状态时显示新“功能区”选项卡。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练演示以下任务：

- 创建 Word 文档项目。

- 将文本添加到 Visual Studio 设计器中托管的文档。

- 编写代码，使用 Word 对象模型在自定义文档时打开时向其中添加文本。

- 生成并运行项目，以对其进行测试。

- 清理项目，以便从开发计算机删除不必要的生成文件和安全设置。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件

 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-the-project"></a>创建项目

### <a name="to-create-a-new-word-document-project-in-visual-studio"></a>在 Visual Studio 中创建新的 Word 文档项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在 **“文件”** 菜单上，指向 **“新建”** ，再单击 **“项目”** 。
::: moniker range="vs-2017"
3. 在模板窗格中，展开 **“Visual C#”** 或 **“Visual Basic”**，然后展开 **“Office/SharePoint”**。

4. 在展开的 **Office/SharePoint** 节点下 **，VSTO"外接程序"** 节点。

5. 在项目模板列表中，选择 Word VSTO文档项目。

6. 在" **名称"** 框中，键入 **FirstDocumentCustomization**。

7. 单击“确定”。

8. 从 **向导中选择**"Visual Studio Tools for Office Project **文档"，** 然后单击"确定 **"。**
::: moniker-end
::: moniker range=">=vs-2019"
3. 在"**创建新文档Project** 对话框中，选择 **"Word VSTO文档"** 项目。

     [!INCLUDE[new-project-dialog-search](../vsto/includes/new-project-dialog-search-md.md)]

4. 单击“下一步”。

5. 在"配置新项目"对话框的"名称"框中键入 **FirstWorkbookCustomization，** 然后单击"创建 **"。**

6. 从 **向导中选择**"Visual Studio Tools for Office Project **文档"，** 然后单击"确定 **"。**
::: moniker-end
   - [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建 **FirstDocumentCustomization** 项目，并将 **FirstDocumentCustomization** 文档和 ThisDocument 代码文件添加到项目。 **FirstDocumentCustomization** 文档在设计器中自动打开。

## <a name="close-and-reopen-the-document-in-the-designer"></a>在设计器中关闭并重新打开文档

 如果开发项目时有意或无意关闭了设计器中的文档，则可以重新打开它。

### <a name="to-close-and-reopen-the-document-in-the-designer"></a>若要关闭并重新打开设计器中的文档

1. 单击设计器窗口的 **X** ("关闭) 关闭文档。

2. 在 **解决方案资源管理器** 中，右键单击 **ThisDocument** 代码文件，然后单击 **视图设计器。**

     \- 或 -

     在 **解决方案资源管理器** 中，双击 **ThisDocument** 代码文件。

## <a name="add-text-to-the-document-in-the-designer"></a>在设计器中向文档添加文本

 可以通过修改在设计器中打开的文档来设计自定义的用户界面 (UI)。 例如，可以添加文本、表格或 Word 控件。 有关如何使用设计器的信息，请参阅 Office[环境中Visual Studio项目](../vsto/office-projects-in-the-visual-studio-environment.md)。

### <a name="to-add-text-to-your-document-by-using-the-designer"></a>使用设计器将文本添加到文档

1. 在已在设计器中打开的文档中键入以下文本。

     **This text was added by using the designer.**

## <a name="add-text-to-the-document-programmatically"></a>以编程方式向文档添加文本

 接下来，将代码添加到 ThisDocument 代码文件。 新代码使用 Word 对象模型向文档添加文本的第二个段落。 默认情况下，ThisDocument 代码文件包含以下生成的代码：

- `ThisDocument` 类的部分定义，用于表示文档的编程模型，并提供对 Word 对象模型的访问权限。 有关详细信息，请参阅文档 [宿主项和](../vsto/document-host-item.md) [Word 对象模型概述](../vsto/word-object-model-overview.md)。 `ThisDocument` 类的其余部分是在隐藏代码文件中定义的，不应修改该代码文件。

- `ThisDocument_Startup` 和 `ThisDocument_Shutdown` 事件处理程序。 将在打开或关闭文档时调用这些事件处理程序。 使用这些事件处理程序，可在打开文档时对其进行初始化，并在关闭文档时清理自定义项所使用的资源。 有关详细信息，请参阅[项目中Office事件](../vsto/events-in-office-projects.md)。

### <a name="to-add-a-second-paragraph-of-text-to-the-document-by-using-code"></a>若要使用代码向文档添加文本的第二个段落

1. 在 **解决方案资源管理器** 中，右键单击 **"ThisDocument"，** 然后单击"**查看代码"。**

     将在 Visual Studio 中打开代码文件。

2. 将 `ThisDocument_Startup` 事件处理程序替换为以下代码。 当打开文档时，此代码会将文本第二个段落添加到文档中。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/FirstDocumentCustomization/ThisDocument.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/FirstDocumentCustomization/ThisDocument.cs" id="Snippet1":::

    > [!NOTE]
    > 此代码使用索引值 1 来访问 <xref:Microsoft.Office.Tools.Word.Document.Paragraphs%2A> 属性的第一个段落。 尽管 Visual Basic 和 Visual C# 使用从 0 开始的数组，但 Word 对象模型中大多数集合的数组下限都是 1。 有关详细信息，请参阅在解决方案[中Office代码](../vsto/writing-code-in-office-solutions.md)。

## <a name="test-the-project"></a>测试项目

### <a name="to-test-your-document"></a>测试文档

1. 按 **F5** 生成并运行项目。

     生成项目时，会将代码编译到与该文档相关联的程序集中。 Visual Studio 将该文档和程序集的副本放入项目的生成输出文件夹中，并将开发计算机上的安全设置配置为允许自定义项运行。 有关详细信息，请参阅生成[Office解决方案](../vsto/building-office-solutions.md)。

2. 验证文档中具有以下文本。

     **This text was added by using the designer.**

     **This text was added by using code.**

3. 关闭文档。

## <a name="clean-up-the-project"></a>清理项目

 完成项目开发后，应删除生成输出文件夹中的文件和由生成过程创建的安全设置。

### <a name="to-clean-up-the-completed-project-on-your-development-computer"></a>在开发计算机上清理已完成的项目

1. 在 Visual Studio 中，在 **“生成”** 菜单上，单击 **“清理解决方案”**。

## <a name="next-steps"></a>后续步骤

 既然你已经创建了一个基本的 Word 文档级自定义项，你就可以从下面这些主题中了解有关如何开发自定义项的详细信息：

- 可以在文档级自定义项中执行常规编程任务： [对文档级自定义进行编程](../vsto/programming-document-level-customizations.md)。

- 特定于 Word 文档级自定义项的编程任务 [：Word 解决方案](../vsto/word-solutions.md)。

- 使用 Word 的对象模型 [：Word 对象模型概述](../vsto/word-object-model-overview.md)。

- 自定义 Word 的 UI，例如，将自定义选项卡添加到功能区或创建自己的操作窗格：Office UI[自定义](../vsto/office-ui-customization.md)。

- 使用 Visual Studio 中的 Office 解决方案提供的扩展 Word 对象来执行使用 Word 对象模型 (无法执行的任务，例如，通过使用 Windows Forms 数据绑定模型) ：使用扩展对象自动执行[Word，](../vsto/automating-word-by-using-extended-objects.md)在文档上承载托管控件，以及将 Word 控件绑定到数据。

- 生成和调试 Word 的文档级自定义：生成Office[解决方案](../vsto/building-office-solutions.md)。

- 为 Word 部署文档级自定义项[：部署Office解决方案](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>请参阅

- [Office解决方案开发概述&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [Word 解决方案](../vsto/word-solutions.md)
- [计划文档级自定义项](../vsto/programming-document-level-customizations.md)
- [Word 对象模型概述](../vsto/word-object-model-overview.md)
- [使用扩展对象自动执行 Word](../vsto/automating-word-by-using-extended-objects.md)
- [OfficeUI 自定义](../vsto/office-ui-customization.md)
- [生成Office解决方案](../vsto/building-office-solutions.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [Office项目模板概述](../vsto/office-project-templates-overview.md)
