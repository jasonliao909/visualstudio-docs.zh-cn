---
title: 演练：创建应用程序SharePoint页|Microsoft Docs
description: 在此演练中，使用 (页面的专用 ASP.NET 创建应用程序) ，然后使用本地 SharePoint 站点对其进行调试。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application pages [SharePoint development in Visual Studio], developing
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 7aa99f3d9fb333d9d7b1177eae39a5f5800cb4e1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122148852"
---
# <a name="walkthrough-create-a-sharepoint-application-page"></a>演练：创建 SharePoint 应用程序页

应用程序页是应用程序页的专用 ASP.NET 形式。 应用程序页包含与主页面SharePoint的内容。 有关详细信息，请参阅[为应用程序创建SharePoint。](../sharepoint/creating-application-pages-for-sharepoint.md)

本演练演示如何创建应用程序页，然后使用本地站点调试SharePoint页面。 此页显示每个用户在服务器场的所有站点中创建或修改的所有项。

本演练演示以下任务：

- 创建SharePoint项目。
- 将应用程序页添加到SharePoint项目。
- 将 ASP.NET 添加到应用程序页。
- 在控件后面添加 ASP.NET 代码。
- 测试应用程序页。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>必备条件

- 支持的 Windows 和 SharePoint 版本。

## <a name="create-a-sharepoint-project"></a>创建SharePoint项目

首先，创建 **一个空SharePoint Project。** 稍后，你将向 **此项目添加应用程序** 页项。

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 打开 **"Project"** 对话框，展开 **Office/SharePoint** 语言下的"SharePoint解决方案 **"** 节点。

3. 在 **"Visual Studio模板**"窗格中，选择"SharePoint **2010 - 空** Project模板。 将项目 **"MySharePointProject"** 命名，然后选择"确定 **"** 按钮。

     将显示 **SharePoint自定义向导**。 使用此向导可以选择用于调试项目的站点和解决方案的信任级别。

4. 选择"**部署为场解决方案"** 选项按钮，然后选择"完成"按钮以接受默认本地SharePoint站点。

## <a name="create-an-application-page"></a>创建应用程序页

若要创建应用程序页，请向 **项目添加应用程序** 页项。

1. 在 **解决方案资源管理器** 中，选择 **"MySharePointProject"** 项目。

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 在" **添加新项"对话框中** ，选择"应用程序页 **" ("仅场解决方案"** 模板。

4. 将页面 **"SearchItems"命名**，然后选择" **添加"** 按钮。

     Visual Web 开发人员设计器在" **源"视图中** 显示应用程序页，可在其中查看页面的 HTML 元素。 设计器显示多个控件的 <xref:System.Web.UI.WebControls.Content> 标记。 每个控件映射到 <xref:System.Web.UI.WebControls.ContentPlaceHolder> 默认应用程序母版页中定义的控件。

## <a name="design-the-layout-of-the-application-page"></a>设计应用程序页的布局

使用"应用程序页"项，可以使用设计器将 ASP.NET 控件添加到应用程序页。 此设计器与 Visual Web 开发人员中使用的设计器相同。 将标签、单选按钮列表和表添加到设计器的"源"视图中，然后设置属性，就像设计任何标准 ASP.NET 一样。

1. 在菜单栏上，选择"查看 **工具箱**  >  **"。**

2. 在"工具箱 **"的"** 标准"节点中，执行以下步骤之一：

    - 打开"标签"项的快捷菜单，选择"复制"，打开设计器中 **PlaceHolderMain** 内容控件下行的快捷菜单，然后选择"粘贴 **"。**

    - 将 **"标签"** 项从 **"工具箱** "拖动到 **PlaceHolderMain** 内容控件的正文上。

3. 重复上一步，将 **DropDownList** 项和 **表** 项添加到 **PlaceHolderMain** 内容控件。

4. 在设计器上，将标签控件的 属性的值更改为 `Text` **"显示所有项"。**

5. 在设计器上，将 `<asp:DropDownList>` 元素替换为以下 XML。

    ```xml
    <asp:DropDownList ID="DropDownList1" runat="server" AutoPostBack="true"
     OnSelectedIndexChanged="DropDownList1_SelectedIndexChanged">
        <asp:ListItem Text="Created by me" Value="Author"></asp:ListItem>
        <asp:ListItem Text="Modified by me" Value="Editor"></asp:ListItem>
    </asp:DropDownList>
    ```

## <a name="handle-the-events-of-controls-on-the-page"></a>处理页面上控件的事件

处理应用程序页中的控件，就像处理任何 ASP.NET 一样。 此过程将处理 `SelectedIndexChanged` 下拉列表的 事件。

1. 在"视图 **"菜单** 上，选择"代码 **"。**

     应用程序页代码文件将在代码编辑器中打开。

2. 将以下方法添加到 `SearchItems` 类。 此代码通过调用稍后将在此演练中创建的方法来处理 <xref:System.Web.UI.WebControls.ListControl.SelectedIndexChanged> <xref:System.Web.UI.WebControls.DropDownList> 的 事件。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb" id="Snippet5":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs" id="Snippet5":::

3. 将以下语句添加到应用程序页代码文件的顶部。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs" id="Snippet1":::

4. 将以下方法添加到 `SearchItems` 类。 此方法会访问服务器场上的所有站点，并搜索当前用户创建或修改的项。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs" id="Snippet2":::

5. 将以下方法添加到 `SearchItems` 类。 此方法显示表中当前用户创建或修改的项。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs" id="Snippet3":::

## <a name="test-the-application-page"></a>测试应用程序页

运行项目时，将打开SharePoint站点，并出现应用程序页。

1. 在 **解决方案资源管理器** 中，打开应用程序页的快捷菜单，然后选择"**设置为启动项"。**

2. 选择 F5。

     随即SharePoint站点。

3. 在应用程序页上，选择" **修改者"** 选项。

     应用程序页将刷新并显示在服务器场的所有站点中修改的所有项。

4. 在应用程序页上，选择 **列表中的"由我** 创建"。

     应用程序页将刷新并显示在服务器场的所有站点中创建的所有项。

## <a name="next-steps"></a>后续步骤

有关应用程序页SharePoint，请参阅[为应用程序创建SharePoint。](../sharepoint/creating-application-pages-for-sharepoint.md)

可以使用以下主题中的 Visual Web 设计器SharePoint设计页面内容：

- [为 SharePoint。](../sharepoint/creating-web-parts-for-sharepoint.md)

- [为 Web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)。

## <a name="see-also"></a>请参阅

[如何：创建应用程序页](../sharepoint/how-to-create-an-application-page.md) 
[应用程序_layouts页类型](/previous-versions/office/aa979604(v=office.14))
