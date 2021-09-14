---
title: 演练：从 Visual C# 项目中的 VBA 调用代码
description: 了解如何在文档级自定义项中调用方法，Microsoft Excel工作簿中的 Visual Basic for Applications (VBA) 调用方法。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], calling code from VBA
- Word [Office development in Visual Studio], calling code from VBA
- Visual C# [Office development in Visual Studio], calling code from VBA
- workbooks [Office development in Visual Studio], calling code from VBA
- VBA [Office development in Visual Studio], calling code in document-level customizations
- Office documents [Office development in Visual Studio, Visual Basic for Applications and
- calling code from VBA
- document-level customizations [Office development in Visual Studio], calling code
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 1556eab077a56bc3b6880cc9a0a413e782f98c2d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602212"
---
# <a name="walkthrough-call-code-from-vba-in-a-visual-c-project"></a>演练：从 Visual C# 项目中的 VBA 调用代码
  此演练演示如何从工作簿的 Visual Basic for Applications (VBA) 代码调用 Microsoft Office Excel 文档级自定义项中的方法。 该过程包括三个基本步骤：向 `Sheet1` 主机项类添加方法、向工作簿中的 VBA 代码公开方法，然后从工作簿的 VBA 代码中调用该方法。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 虽然本演练具体使用的是 Excel，但其中所阐释的概念同样适用于 Word 的文档级项目。

 本演练演示以下任务：

- 创建包含 VBA 代码的工作簿。

- 使用 Excel 中的“信任中心”信任工作薄的位置。

- 向 `Sheet1` 主机项类添加方法。

- 提取 `Sheet1` 主机项类的接口。

- 向 VBA 代码公开方法。

- 从 VBA 代码中调用方法。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Excel

## <a name="create-a-workbook-that-contains-vba-code"></a>创建包含 VBA 代码的工作簿
 第一步是创建一个启用宏的工作簿，该工作簿包含简单的 VBA 宏。 工作簿必须已经包含 VBA 代码，然后你才能向 VBA 公开自定义项中的代码。 否则，Visual Studio 将无法修改 VBA 项目以允许 VBA 代码调入自定义项程序集。

 如果已经拥有包含要使用的 VBA 代码的工作薄，则可以跳过此步骤。

### <a name="to-create-a-workbook-that-contains-vba-code"></a>创建包含 VBA 代码的工作薄

1. 启动 Excel。

2. 将活动文档另存为 Excel Macro-Enabled **工作簿 (\* .xlsm**) **名称 WorkbookWithVBA**。 将其保存在一个方便的位置，例如桌面。

3. 在功能区上，单击 **“开发人员”** 选项卡。

    > [!NOTE]
    > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅 [功能区 上的"如何：显示开发人员"选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

4. 在 **“代码”** 组中，单击 **“Visual Basic”**。

     将打开 Visual Basic 编辑器。

5. 在 **“项目”** 窗口中，双击 **“ThisWorkbook”**。

     将打开 `ThisWorkbook` 对象的代码文件。

6. 将下面的 VBA 代码添加到代码文件。 此代码定义一个不执行任何操作的简单函数。 此函数的唯一用途是确保 VBA 项目存在于工作簿中。 这是本演练中的后续步骤所必需的。

    ```vb
    Sub EmptySub()
    End Sub
    ```

7. 保存文档并退出 Excel。

## <a name="create-the-project"></a>创建项目
 现在，你可以创建一个 Excel 文档级项目，这个项目使用先前创建的启用宏的工作簿。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在 **“文件”** 菜单上，指向 **“新建”** ，再单击 **“项目”** 。

3. 在模板窗格中，展开 **“Visual C#”**，然后展开 **“Office/SharePoint”**。

4. 选择“Office 外接程序”  节点。

5. 在项目模板列表中，选择 **“Excel 2010 工作簿”** 或 **“Excel 2013 工作簿”** 项目。

6. 在“名称”  框中，键入 **CallingCodeFromVBA**。

7. 单击“确定”。

     将打开“Visual Studio Tools for Office 项目向导”  。

8. 选择 **“复制现有文档”**，然后在 **“现有文档的完整路径”** 框中，指定先前创建的 **WorkbookWithVBA** 工作薄的位置。 如果正在使用自己的启用宏的工作簿，则改为指定此工作簿的位置。

9. 单击“完成”  。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]在设计器 **中打开 WorkbookWithVBA** 工作簿，并将 **CallingCodeFromVBA** 项目添加到 **解决方案资源管理器。**

## <a name="trust-the-location-of-the-workbook"></a>信任工作簿的位置
 必须先信任要运行的工作簿中的 VBA，然后才可向工作簿中的 VBA 代码公开解决方案中的代码。 有多种方法可实现此目的。 在本演练中，将通过在 Excel 的 **“信任中心”** 信任工作薄的位置来完成此任务。

### <a name="to-trust-the-location-of-the-workbook"></a>信任工作薄的位置

1. 启动 Excel。

2. 单击 **“文件”** 选项卡。

3. 单击 **“Excel 选项”** 按钮。

4. 在类别窗格中，单击 **“信任中心”**。

5. 在细节窗格中，单击 **“信任中心设置”**。

6. 在类别窗格中，单击 **“受信任位置”**。

7. 在细节窗格中，单击 **“添加新位置”**。

8. 在“Microsoft Office 受信任位置”  对话框中，浏览到包含 **CallingCodeFromVBA** 项目的文件夹。

9. 选择 **“同时信任此位置的子文件夹”**。

10. 在 **“Microsoft Office 受信任位置”** 对话框中，单击 **“确定”**。

11. 在 **“信任中心”** 对话框中，单击 **“确定”**。

12. 在 **“Excel 选项”** 对话框中，单击 **“确定”**。

13. 退出 **Excel。**

## <a name="add-a-method-to-the-sheet1-class"></a>向 Sheet1 类添加方法
 既然已设置 VBA 项目，请向可以从 VBA 代码中调用的 `Sheet1` 主机项类添加一个公共方法。

### <a name="to-add-a-method-to-the-sheet1-class"></a>向 Sheet1 类添加方法

1. 在 **“解决方案资源管理器”** 中，右键单击 **“Sheet1.cs”**，然后单击 **“查看代码”**。

     **Sheet1.cs** 文件将在代码编辑器中打开。

2. 将以下代码添加到 `Sheet1` 类。 `CreateVstoNamedRange` 方法在指定的范围创建一个新的 <xref:Microsoft.Office.Tools.Excel.NamedRange> 对象。 此方法还会为 <xref:Microsoft.Office.Tools.Excel.NamedRange.Selected> 的 <xref:Microsoft.Office.Tools.Excel.NamedRange>事件创建一个事件处理程序。 在本演练中，稍后将从文档的 VBA 代码中调用 `CreateVstoNamedRange` 方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/CallingCodeFromVBA/Sheet1.cs" id="Snippet2":::

3. 将以下方法添加到 `Sheet1` 类。 此方法将替代 <xref:Microsoft.Office.Tools.Excel.WorksheetBase.GetAutomationObject%2A> 方法，以返回 `Sheet1` 类的当前实例。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/CallingCodeFromVBA/Sheet1.cs" id="Snippet3":::

4. 在 `Sheet1` 类声明的第一行前面应用下列特性。 这些特性使类对于 COM 可见，但不生成类接口。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/CallingCodeFromVBA/Sheet1.cs" id="Snippet1":::

## <a name="extract-an-interface-for-the-sheet1-class"></a>提取 Sheet1 类的接口
 必须先创建一个定义 `CreateVstoNamedRange` 方法的公共接口，并向 COM 公开此接口，然后才可向 VBA 代码公开此方法。

### <a name="to-extract-an-interface-for-the-sheet1-class"></a>提取 Sheet1 类的接口

1. 在 **Sheet1.cs** 代码文件中，单击 `Sheet1` 类中的任意位置。

2. 在 **“重构”** 菜单中，单击 **“提取接口”**。

3. 在 **“提取接口”** 对话框中，在 **“选择构成接口的公共成员”** 框中，单击 `CreateVstoNamedRange` 方法项。

4. 单击“确定”。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会生成名为 `ISheet1`的新接口，并修改 `Sheet1` 的定义，以便实现 `ISheet1` 接口。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 还会在代码 **编辑器中打开 ISheet1.cs** 文件。

5. 在 **ISheet1.cs** 文件中，将 `ISheet1` 接口声明替换为以下代码。 此代码使 `ISheet1` 接口成为公共接口，并且应用 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 特性使该接口对于 COM 可见。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/CallingCodeFromVBA/ISheet1.cs" id="Snippet4":::

6. 生成项目。

## <a name="expose-the-method-to-vba-code"></a>向 VBA 代码公开 方法
 若要向工作簿中的 VBA 代码公开 `CreateVstoNamedRange` 方法，请将 **主机项的** “ReferenceAssemblyFromVbaProject” `Sheet1` 属性设置为 **“True”**。

### <a name="to-expose-the-method-to-vba-code"></a>向 VBA 代码公开方法

1. 在 **解决方案资源管理器** 中，双击 **Sheet1.cs**。

     **WorkbookWithVBA** 文件将在设计器中打开，并且 Sheet1 可见。

2. 在 **“属性”** 窗口中，选择 **“ReferenceAssemblyFromVbaProject”** 属性，并将值更改为 **“True”**。

3. 在显示的消息中单击 **“确定”** 。

4. 生成项目。

## <a name="call-the-method-from-vba-code"></a>从 VBA 代码调用方法
 现在可以从工作簿的 VBA 代码中调用 `CreateVstoNamedRange` 方法。

> [!NOTE]
> 在本演练中，将在调试项目时向工作薄中添加 VBA 代码。 在下次生成项目时，添加到此文档中的 VBA 代码将被覆盖，因为 Visual Studio 会将生成输出文件夹中的文档替换为主项目文件夹中文档的副本。 如果想要保存 VBA 代码，可以将其复制到项目文件夹中的文档。 有关详细信息，请参阅 [合并 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)。

### <a name="to-call-the-method-from-vba-code"></a>从 VBA 代码调用方法

1. 按 **F5** 运行项目。

2. 在 **“开发人员”** 选项卡上的 **“代码”** 组中，单击 **“Visual Basic”**。

     将打开 Visual Basic 编辑器。

3. 在 **“插入”** 菜单上，单击 **“模块”**。

4. 向新模块添加以下代码。

     此代码调用自定义项程序集中的 `CreateTable` 方法。 宏通过使用全局 `GetManagedClass` 方法来访问你向 VBA 代码公开的 `Sheet1` 主机项类，从而访问此方法。 `GetManagedClass` 方法是你之前在本演练中设置 **“ReferenceAssemblyFromVbaProject”** 属性时自动生成的。

    ```vb
    Sub CallVSTOMethod()
        Dim VSTOSheet1 As CallingCodeFromVBA.Sheet1
        Set VSTOSheet1 = GetManagedClass(Sheet1)
        Call VSTOSheet1.CreateVstoNamedRange(Sheet1.Range("A1"), "VstoNamedRange")
    End Sub
    ```

5. 按 **F5**。

6. 在打开的工作簿中，单击 **“Sheet1”** 上的单元格 **“A1”**。 验证是否显示消息框。

7. 退出 Excel 而不保存更改。

## <a name="next-steps"></a>后续步骤
 在以下主题中，你可以了解有关从 VBA 调用 Office 解决方案中的代码的详细信息：

- 从 VBA 调用 Visual Basic 自定义项的主机项中的代码。 此过程不同于 Visual C# 过程。 有关详细信息，请参阅[演练：在 Visual Basic 项目中调用 VBA 中的代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)。

- 从 VBA 调用 VSTO 外接程序中的代码。 有关详细信息，请参阅[演练：从 VBA 调用 VSTO 外接程序中的代码](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)。

## <a name="see-also"></a>另请参阅
- [合并 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)
- [程序文档级自定义项](../vsto/programming-document-level-customizations.md)
- [如何：在 Visual Basic 项目中向 VBA 公开代码](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)
- [如何：在 Visual C&#35; 项目中向 VBA 公开代码](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)
- [演练：在 Visual Basic 项目中调用 VBA 中的代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)
