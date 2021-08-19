---
title: 演练：创建 Web 部件以用于SharePoint |Microsoft Docs
description: 为 SharePoint。 Web 部件允许用户使用浏览器直接更改SharePoint页面的内容、外观和行为。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122123276"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint"></a>演练：为 SharePoint 创建 Web 部件

Web 部件用户可以使用浏览器直接修改SharePoint页面的内容、外观和行为。 本演练演示如何使用 2010 年 1 月中的 **Web** 部件项模板Visual Studio Web 部件。

Web 部件在数据网格中显示员工。 用户指定包含员工数据的文件的位置。 用户还可以筛选数据网格，以便只有作为经理的员工才出现在列表中。

本演练演示以下任务：

- 使用 Web 部件项模板Visual Studio **Web** 部件。

- 创建 Web 部件的用户可设置的属性。 此属性指定员工数据文件的位置。

- 通过将控件添加到 Web 部件控件集合来呈现 Web 部件中的内容。

- 创建一个新的菜单项（称为谓词）出现在呈现的 Web 部件谓词菜单中。 谓词允许用户修改 Web 部件中显示的数据。

- 在 SharePoint 中测试 Web 部件。

    > [!NOTE]
    > 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>必备条件

- 支持的 Microsoft Windows 和 SharePoint 版本。

- Visual Studio 2017 或 Azure DevOps Services。

## <a name="create-an-empty-sharepoint-project"></a>创建空SharePoint项目

首先，创建一个空SharePoint项目。 稍后，你将使用 Web 部件项模板将 Web **部件** 添加到项目。

1. 首先 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 使用" **以管理员方式运行"** 选项。

2. 在男性栏上，选择"**文件**  >  **""新建**  >  **Project"。**

3. 在 **"新建Project"** 对话框中，展开SharePoint语言下的"2010"节点，然后选择 **"2010"** 节点。 

4. 在"**模板"窗格中**，选择 **"SharePoint 2010** Project"，然后选择"确定 **"** 按钮。

     将显示 **SharePoint自定义向导**。 使用此向导可以选择用于调试项目的站点和解决方案的信任级别。

5. 选择"**部署为场解决方案"** 选项按钮，然后选择"完成"按钮以接受默认本地SharePoint站点。

## <a name="add-a-web-part-to-the-project"></a>向项目添加 Web 部件

向 **项目添加 Web** 部件项。 Web **部件项** 添加 Web 部件代码文件。 稍后，你将向 Web 部件代码文件添加代码，以呈现 Web 部件的内容。

1. 在菜单栏上，依次选择“项目” > “添加新项”。

2. 在"**添加新项"对话框** 的"已安装模板"窗格中，展开"SharePoint"**节点**，然后选择 **"2010"** 节点。

3. 在模板SharePoint，选择 **"Web** 部件"模板，然后选择"添加 **"** 按钮。

     Web **部件项** 显示在 **解决方案资源管理器。**

## <a name="rendering-content-in-the-web-part"></a>在 Web 部件中呈现内容

可以通过将哪些控件添加到 Web 部件类的控件集合来指定要显示在 Web 部件中的控件。

1. 在 **解决方案资源管理器** 中，在 C# (Visual Basic) 或 *WebPart1.cs* (中打开 *WebPart1.vb* ) 。

     Web 部件代码文件将在代码编辑器中打开。

2. 将以下指令添加到 Web 部件代码文件的顶部。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet1":::

3. 将以下代码添加到 `WebPart1` 类。 此代码声明以下字段：

   - 一个数据网格，用于显示 Web 部件中的员工。

   - 用于筛选数据网格的控件上显示的文本。

   - 一个标签，如果数据网格无法显示数据，则显示错误。

   - 一个包含员工数据文件路径的字符串。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet2":::

4. 将以下代码添加到 `WebPart1` 类。 此代码将名为 的自定义属性 `DataFilePath` 添加到 Web 部件。 自定义属性是可在用户SharePoint设置的属性。 此属性获取和设置用于填充数据网格的 XML 数据文件的位置。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet3":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet3":::

5. 将 `CreateChildControls` 方法替换为以下代码。 此代码执行以下任务：

   - 添加在上一步中声明的数据网格和标签。

   - 将数据网格绑定到包含员工数据的 XML 文件。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet4":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet4":::

6. 将以下方法添加到 `WebPart1` 类。 此代码执行以下任务：

   - 创建一个谓词，该谓词显示在呈现的 Web 部分的"Web 部件谓词"菜单中。

   - 处理在用户选择谓词菜单中的谓词时所引发的事件。 此代码筛选数据网格中显示的员工列表。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet5":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet5":::

## <a name="test-the-web-part"></a>测试 Web 部件

运行项目时，将打开SharePoint站点。 Web 部件会自动添加到 Web 部件库中的 SharePoint。 可以将 Web 部件添加到任何 Web 部件页。

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

2. 在记事本菜单栏上，选择"**文件**  >  **另存为"。**

3. 在"**另存为**"对话框的"**另存为类型"列表中**，选择"**所有文件"。**

4. 在"**文件名"框中**，输入 **"data.xml"。**

5. 使用"浏览文件夹"按钮 **选择** 任何文件夹，然后选择"保存 **"** 按钮。

6. 在Visual Studio中，选择 **F5** 键。

     随即SharePoint站点。

7. 在"**站点操作"菜单** 上，选择"**更多选项"。**

8. 在" **创建** "页中，选择 **"Web 部件页** "类型，然后选择"创建 **"** 按钮。

9. 在" **新建 Web 部件页"** 页中，将页面名称为 **SampleWebPartPage.aspx**，然后选择"创建 **"** 按钮。

     将显示"Web 部件"页。

10. 选择"Web 部件"页上的任何区域。

11. 在页面顶部，选择"插入 **"** 选项卡，然后选择 **"Web 部件"** 按钮。

12. 在" **类别"** 窗格中，选择" **自定义** "文件夹，选择 **"WebPart1** Web 部件"，然后选择"添加 **"** 按钮。

     Web 部件显示在页面上。

## <a name="test-the-custom-property"></a>测试自定义属性

若要填充 Web 部件中显示的数据网格，请指定包含每个雇员数据的 XML 文件的路径。

1. 选择 Web 部件右侧出现的箭头，然后从出现的菜单中选择"编辑 **Web** 部件"。

     页面右侧将显示一个包含 Web 部件属性的窗格。

2. 在窗格中，展开"**杂项**"节点，输入之前创建的 XML 文件的路径，选择"应用"按钮，然后选择"确定 **"** 按钮。

     验证"Web 部件"中是否显示员工列表。

## <a name="test-the-web-part-verb"></a>测试 Web 部件谓词

通过选择显示在"Web 部件谓词"菜单中的项来显示和隐藏不是经理的员工。

1. 选择 Web 部件右侧出现的箭头，然后从出现的菜单中选择"仅显示经理"。

     只有作为经理的员工才出现在 Web 部件中。

2. 再次选择箭头，然后从出现的 **菜单中** 选择"显示所有员工"。

     所有员工都显示在 Web 部件中。

## <a name="see-also"></a>请参阅

[创建 web 部件SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md) 
[如何：创建SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md) 
[如何：使用设计器SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md) 
[演练：使用设计器](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)为SharePoint Web 部件
