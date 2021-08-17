---
title: 如何：向应用程序添加自定义任务窗格
description: 了解如何使用 Visual Studio Tools for Office (VSTO) 外接程序向应用程序添加自定义任务窗格。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- task panes [Office development in Visual Studio], adding to application
- custom task panes [Office development in Visual Studio], adding to application
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 3477930ba181f4a0f33d8711e882cda8ba63af17
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122026364"
---
# <a name="how-to-add-a-custom-task-pane-to-an-application"></a>如何：向应用程序添加自定义任务窗格
  你可以通过使用 VSTO 外接程序向上面列出的应用程序添加自定义任务窗格。 有关详细信息，请参阅 [自定义任务窗格](../vsto/custom-task-panes.md)。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="add-a-custom-task-pane-to-an-application"></a>向应用程序添加自定义任务窗格

### <a name="to-add-a-custom-task-pane-to-an-application"></a>若要向应用程序添加自定义任务窗格

1. 为上面列出的应用程序之一打开或创建 VSTO 外接程序项目。 有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

2. 在 **“项目”** 菜单上，单击 **“添加用户控件”**。

3. 在 " **添加新项** " 对话框中，将新用户控件的名称更改为 " **MyUserControl**"，然后单击 " **添加**"。

     用户控件将在设计器中打开。

4. 将 "**工具箱**" 中的一个或多个 Windows 窗体控件添加到用户控件。

5. 打开 **ThisAddIn** 或 **ThisAddIn** 代码文件。

6. 将以下代码添加到 `ThisAddIn` 类。 此代码将 `MyUserControl` 和 <xref:Microsoft.Office.Tools.CustomTaskPane> 的实例声明为 `ThisAddIn` 类的成员。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneBasic/ThisAddIn.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneBasic/ThisAddIn.cs" id="Snippet1":::

7. 将以下代码添加到 `ThisAddIn_Startup` 事件处理程序中。 此代码通过将 <xref:Microsoft.Office.Tools.CustomTaskPane> 对象添加到 `MyUserControl` 集合来创建新 `CustomTaskPanes` 。 代码还将显示任务窗格。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneBasic/ThisAddIn.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneBasic/ThisAddIn.cs" id="Snippet2":::

    > [!NOTE]
    > 此代码将自定义任务窗格与应用程序中的活动窗口关联。 对于某些应用程序，你可能想要修改此代码以确保任务窗格与应用程序中的其他文档或项目一起显示。 有关详细信息，请参阅 [自定义任务窗格](../vsto/custom-task-panes.md)。

## <a name="see-also"></a>请参阅
- [OfficeUI 自定义](../vsto/office-ui-customization.md)
- [自定义任务窗格](../vsto/custom-task-panes.md)
- [演练：从自定义任务窗格自动化应用程序](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)
