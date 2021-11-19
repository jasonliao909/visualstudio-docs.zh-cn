---
title: 演练：为 SharePoint 创建 Web 部件 | Microsoft Docs
description: 为 SharePoint 创建 Web 部件。 Web 部件使用户能够使用浏览器直接更改 SharePoint 网站页面的内容、外观和行为。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], developing
- Web Parts [SharePoint development in Visual Studio], creating
- Web Parts [SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 9bdeb3397c3c958912010af9f822b48a66add8e6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126667477"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint"></a>演练：为 SharePoint 创建 Web 部件

Web 部件使用户能够使用浏览器直接修改 SharePoint 网站页的内容、外观和行为。 本演练演示如何使用 Visual Studio 2010 中的 Web 部件项模板创建 Web 部件。

Web 部件在数据网格中显示员工。 用户指定包含员工数据的文件的位置。 用户还可以筛选数据网格，以便仅在列表中显示作为经理的员工。

本演练演示以下任务：

- 使用 Visual Studio Web 部件项模板创建 Web 部件。

- 创建可由 Web 部件用户设置的属性。 此属性指定员工数据文件的位置。

- 通过将控件添加到 Web 部件控件集合来呈现 Web 部件中的内容。

- 创建一个新的菜单项（称为谓词），该项会显示在呈现的 Web 部件的谓词菜单中。 谓词使用户能够修改 Web 部件中显示的数据。

- 在 SharePoint 中测试 Web 部件。

    > [!NOTE]
    > 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件

- 支持的 Microsoft Windows 和 SharePoint 版本。

- Visual Studio 2017 或 Azure DevOps Services。

## <a name="create-an-empty-sharepoint-project"></a>创建一个空的 SharePoint 项目

首先，创建一个空的 SharePoint 项目。 稍后，将使用 Web 部件项模板将 Web 部件添加到该项目中。

1. 使用“以管理员身份运行”选项启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，选择“文件” > “新建” > “项目”  。

3. 在“新建项目”对话框中，展开要使用的语言下的“SharePoint”节点，然后选择“2010”节点  。

4. 在“模板”窗格中，选择“SharePoint 2010 项目”，然后选择“确定”按钮  。

     此时将显示“SharePoint 自定义向导”。 使用此向导可以选择用于调试项目的网站以及解决方案的信任级别。

5. 选择“部署为场解决方案”选项按钮，然后选择“完成”按钮以接受默认的本地 SharePoint 网站 。

## <a name="add-a-web-part-to-the-project"></a>向项目添加 Web 部件

向项目添加一个 Web 部件项。 该 Web 部件项会添加 Web 部件代码文件。 稍后，你将向 Web 部件代码文件添加代码，以呈现 Web 部件的内容。

1. 在菜单栏上，依次选择“项目” > “添加新项”。

2. 在“添加新项”对话框的“已安装的模板”窗格中，展开“SharePoint”节点，然后选择“2010”节点   。

3. 在 SharePoint 模板列表中，选择“Web 部件”模板，然后选择“添加”按钮 。

     Web 部件项显示在解决方案资源管理器中 。

## <a name="rendering-content-in-the-web-part"></a>在 Web 部件中呈现内容

可以通过将控件添加到 Web 部件类的控件集合来指定要在 Web 部件中显示的控件。

1. 在解决方案资源管理器中，打开“WebPart1.vb”（在 Visual Basic 中）或“WebPart1.cs”（在 C# 中） 。

     将在代码编辑器中打开 Web 部件代码文件。

2. 将以下指令添加到 Web 部件代码文件的顶部。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet1":::

3. 将以下代码添加到 `WebPart1` 类。 此代码声明以下字段：

   - 用于在 Web 部件中显示员工的数据网格。

   - 在用于筛选数据网格的控件上显示的文本。

   - 数据网格无法显示数据时显示错误的标签。

   - 包含员工数据文件路径的字符串。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet2":::

4. 将以下代码添加到 `WebPart1` 类。 此代码将一个名为 `DataFilePath` 的自定义属性添加到 Web 部件。 自定义属性是用户可以在 SharePoint 中设置的属性。 此属性可获取和设置用于填充数据网格的 XML 数据文件的位置。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet3":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet3":::

5. 将 `CreateChildControls` 方法替换为以下代码。 此代码执行以下任务：

   - 添加在上一步中声明的数据网格和标签。

   - 将数据网格绑定到包含员工数据的 XML 文件。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet4":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet4":::

6. 将以下方法添加到 `WebPart1` 类。 此代码执行以下任务：

   - 创建一个谓词，该谓词显示在呈现的 Web 部件的 Web 部件谓词菜单中。

   - 处理在用户选择谓词菜单中的谓词时所引发的事件。 此代码筛选数据网格中显示的员工列表。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet5":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet5":::

## <a name="test-the-web-part"></a>测试 Web 部件

运行该项目时，SharePoint 网站将打开。 Web 部件会自动添加到 SharePoint 中的 Web 部件库。 可以将 Web 部件添加到任何 Web 部件页面。

1. 将以下 XML 粘贴到记事本文件中。 此 XML 文件包含将在 Web 部件中显示的示例数据。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
        <employees xmlns="http://schemas.microsoft.com/vsto/samples">
           <employee>
               <name>David Hamilton</name>
               <hireDate>2001-05-11</hireDate>
               <title>Sales Associate</title>
           </employee>
           <employee>
               <name>Karina Leal</name>
               <hireDate>1999-04-01</hireDate>
               <title>Manager</title>
           </employee>
           <employee>
               <name>Nancy Davolio</name>
               <hireDate>1992-05-01</hireDate>
               <title>Sales Associate</title>
           </employee>
           <employee>
               <name>Steven Buchanan</name>
               <hireDate>1955-03-04</hireDate>
               <title>Manager</title>
           </employee>
           <employee>
               <name>Suyama Michael</name>
               <hireDate>1963-07-02</hireDate>
               <title>Sales Associate</title>
           </employee>
        </employees>
    ```

2. 在记事本的菜单栏上，选择“文件” > “另存为” 。

3. 在“另存为”对话框的“保存类型”列表中，选择“所有文件”  。

4. 在“文件名”框中，输入“data.xml” 。

5. 通过使用“浏览文件夹”按钮选择任意文件夹，然后选择“保存”按钮 。

6. 在 Visual Studio 中，选择“F5”键。

     SharePoint 网站随即打开。

7. 在“网站操作”菜单上，选择“更多选项” 。

8. 在“创建”页上，选择“Web 部件页面”类型，然后选择“创建”按钮  。

9. 在“新建 Web 部件页面”页上，将该页命名为“SampleWebPartPage.aspx”，然后选择“创建”按钮  。

     Web 部件页面随即打开。

10. 选择 Web 部件页面上的任何区域。

11. 在该页顶部选择“插入”选项卡，然后选择“Web 部件”按钮 。

12. 在“类别”窗格中，依次选择“自定义”文件夹、“WebPart1”Web 部件，然后选择“添加”按钮   。

     该 Web 部件随即显示在页面上。

## <a name="test-the-custom-property"></a>测试自定义属性

若要填充 Web 部件中显示的数据网格，请指定包含有关每个员工的数据的 XML 文件的路径。

1. 选择显示在 Web 部件右侧的箭头，然后从显示的菜单中选择“编辑 Web 部件”。

     页面右侧将显示一个包含 Web 部件属性的窗格。

2. 在此窗格中，展开“杂项”节点，输入先前创建的 XML 文件的路径，选择“应用”按钮，然后选择“确定”按钮  。

     验证 Web 部件中是否显示员工列表。

## <a name="test-the-web-part-verb"></a>测试 Web 部件谓词

通过选择显示在 Web 部件谓词菜单中的项来显示和隐藏不是经理的员工。

1. 选择显示在 Web 部件右侧的箭头，然后从显示的菜单中选择“仅显示经理”。

     只有作为经理的员工才会显示在 Web 部件中。

2. 再次选择此箭头，然后从显示的菜单中选择“显示所有员工”。

     所有员工都显示在 Web 部件中。

## <a name="see-also"></a>另请参阅

[为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
[如何：创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)
[如何：使用设计器创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)
[演练：使用设计器为 SharePoint 创建 Web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
