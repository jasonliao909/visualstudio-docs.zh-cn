---
title: 演练：创建 SharePoint 应用程序页 | Microsoft Docs
description: 在此演练中，创建应用程序页（ASP.NET 的专用窗体），然后使用本地 SharePoint 站点对其进行调试。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665004"
---
# <a name="walkthrough-create-a-sharepoint-application-page"></a>演练：创建 SharePoint 应用程序页

应用程序页是 ASP.NET 页的专用窗体。 应用程序页包含与 SharePoint 母版页合并的内容。 有关详细信息，请参阅[为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

本演练演示如何创建应用程序页，然后使用本地 SharePoint 站点对其进行调试。 此页显示每位用户在服务器场的所有站点中创建或修改的所有项。

本演练演示以下任务：

- 创建 SharePoint 项目。
- 将应用程序页添加到 SharePoint 项目。
- 将 ASP.NET 控件添加到应用程序页。
- 在 ASP.NET 控件后面添加代码。
- 测试应用程序。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件

- 支持的 Windows 和 SharePoint 版本。

## <a name="create-a-sharepoint-project"></a>创建 SharePoint 项目

首先，创建空的 SharePoint 项目。 然后，向此项目添加“应用程序页”项。

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在“新建项目”对话框中，展开要使用的语言下的“Office/SharePoint”节点，然后选择“SharePoint 解决方案”节点  。

3. 在“Visual Studio 安装的模板”窗格中，选择“SharePoint 2010 - 空项目”模板 。 将项目命名为 MySharePointProject，然后选择“确定”按钮 

     SharePoint 自定义向导随即出现。 使用此向导可以选择用于调试项目的站点和解决方案的信任级别。

4. 选择“部署为场解决方案”选项按钮，然后选择“完成”按钮，以接受默认本地 SharePoint 站点 。

## <a name="create-an-application-page"></a>创建应用程序页

若要创建应用程序页，请向该项目添加“应用程序页”项。

1. 在解决方案资源管理器中，选择 MySharePointProject 项目 。

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 在“添加新项”对话框中，选择“应用程序页(仅限场解决方案)”模板 。

4. 将页面命名为 SearchItems，然后选择“添加”按钮 。

     Visual Web 开发人员设计器在源视图中显示应用程序页，可在其中查看页面的 HTML 元素。 设计器显示多个 <xref:System.Web.UI.WebControls.Content> 控件的标记。 每个控件映射到默认应用程序母版页中定义的 <xref:System.Web.UI.WebControls.ContentPlaceHolder> 控件。

## <a name="design-the-layout-of-the-application-page"></a>设计应用程序页的布局

使用“应用程序页”项，可以使用设计器将 ASP.NET 控件添加到应用程序页。 此设计器与 Visual Web 开发人员中使用的设计器相同。 将标签、单选按钮列表和表添加到设计器的源视图中，然后设置属性，就像设计任何标准 ASP.NET 时所操作的一样。

1. 在菜单栏上，依次选择“视图” > “工具箱” 。

2. 在工具箱的标准节点中，执行以下步骤之一：

    - 打开“标签”项的快捷菜单，选择“复制”，打开设计器中 PlaceHolderMain 内容控件下行的快捷菜单，然后选择“粘贴”   。

    - 将“标签”项从“工具箱”拖动到 PlaceHolderMain 内容控件的正文上  。

3. 重复上一步，将“DropDownList”项和“表”项添加到 PlaceHolderMain 内容控件  。

4. 在设计器上，将标签控件的 `Text` 特性的值更改为“显示所有项”。

5. 在设计器上，将 `<asp:DropDownList>` 元素替换为以下 XML。

    ```xml
    <asp:DropDownList ID="DropDownList1" runat="server" AutoPostBack="true"
     OnSelectedIndexChanged="DropDownList1_SelectedIndexChanged">
        <asp:ListItem Text="Created by me" Value="Author"></asp:ListItem>
        <asp:ListItem Text="Modified by me" Value="Editor"></asp:ListItem>
    </asp:DropDownList>
    ```

## <a name="handle-the-events-of-controls-on-the-page"></a>处理页面上的控件的事件

处理应用程序页中的控件，就和处理任何 ASP.NET 进行的操作一样。 此过程将处理下拉列表的 `SelectedIndexChanged` 事件。

1. 在“视图”菜单上，选择“代码” 。

     应用程序页代码文件会在代码编辑器中打开。

2. 将以下方法添加到 `SearchItems` 类。 此代码通过调用在本演练中后面创建的方法来处理 <xref:System.Web.UI.WebControls.DropDownList> 的 <xref:System.Web.UI.WebControls.ListControl.SelectedIndexChanged> 事件。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb" id="Snippet5":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs" id="Snippet5":::

3. 将以下语句添加到应用程序代码文件的顶部。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs" id="Snippet1":::

4. 将以下方法添加到 `SearchItems` 类。 此方法会循环访问服务器场上的所有站点，并搜索当前用户创建或修改的项。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs" id="Snippet2":::

5. 将以下方法添加到 `SearchItems` 类。 此方法显示表中当前用户创建或修改的项。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs" id="Snippet3":::

## <a name="test-the-application-page"></a>测试应用程序页

运行项目时，SharePoint 站点将打开，并会显示应用程序页。

1. 在解决方案资源管理器中，打开应用程序页的快捷菜单，然后选择“设为启动项” 。

2. 选择 F5。

     SharePoint 网站随即打开。

3. 在应用程序页上，选择“修改者是我”选项。

     应用程序页将刷新并显示在服务器场的所有站点中修改的所有项。

4. 在应用程序页上，选择列表中的“创建者是我”。

     应用程序页会刷新并显示在服务器场的所有站点中修改的所有项。

## <a name="next-steps"></a>后续步骤

有关 SharePoint 应用程序页的详细信息，请参阅[为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

可以使用以下主题中的 Visual Web 设计器了解如何设计 SharePoint 页面内容：

- [为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)。

- [为 Web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)。

## <a name="see-also"></a>另请参阅

[如何：创建应用程序页](../sharepoint/how-to-create-an-application-page.md)
[应用程序 _layouts 页类型](/previous-versions/office/aa979604(v=office.14))
