---
title: 演练：创建基本站点定义项目 | Microsoft Docs
description: 本 SharePoint 演练演示如何创建一个基本的站点定义，该定义包含一个具有一些控件的可视 Web 部件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, site definitions
- site definitions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 2d8de9b5da1a9bff70b8332b9b6804295996af5e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664142"
---
# <a name="walkthrough-create-a-basic-site-definition-project"></a>演练：创建基本站点定义项目
  本演练演示如何创建一个基本的站点定义，该定义包含一个具有一些控件的可视 Web 部件。 为了清楚起见，你创建的可视 Web 部件只有几个控件。 不过，你可以创建更复杂的 SharePoint 站点定义，其中包括更多的功能。

 本演练演示了下列任务：

- 通过使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 项目模板创建一个站点定义。

- 通过使用 SharePoint 中的站点定义创建一个 SharePoint 站点。

- 在解决方案中添加一个可视 Web 部件。

- 在站点的 default.aspx 页面上添加新的可视 Web 部件，以对其进行自定义。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 Microsoft Windows 和 SharePoint 版本。 有关详细信息，请参阅“开发 SharePoint 解决方案的要求”。

- Visual Studio。

## <a name="create-a-site-definition-solution"></a>创建站点定义解决方案
 首先，在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中创建站点定义项目。

#### <a name="to-create-a-site-definition-project"></a>创建站点定义项目

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。 如果 IDE 设置为使用 Visual Basic 开发设置，请在菜单栏上选择“文件” > “新建项目” 。

    此时将出现“新建项目”  对话框。

2. 展开“Visual C#”节点或“Visual Basic”节点，再展开“SharePoint”节点，然后选择“2010”节点   。

3. 在“模板”列表中，选择“SharePoint 2010 项目” 模板。

4. 在“名称”框中，输入“TestSiteDef”，然后选择“确定”按钮。

    “SharePoint 自定义向导”随即出现。

5. 在“指定用于调试的站点和安全级别”页上，输入要在其中调试站点定义的 SharePoint 站点的 URL，或者使用默认位置 (http://System Name/)。

6. 在“此 SharePoint 解决方案的信任级别是什么?”部分中，选择“部署为场解决方案”选项按钮。

    所有站点定义项目都必须部署为场解决方案。 有关沙盒解决方案与场解决方案的详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 选择 **“完成”** 按钮。

    项目将出现在“解决方案资源管理器”中。

8. 在解决方案资源管理器中，选择项目节点，然后在菜单栏上选择“项目” > “添加新项”  。

9. 展开“Visual C#”或“Visual Basic”下的“SharePoint”节点，然后选择“2010”节点   。

10. 在“模板”窗格中，选择“站点定义”模板，保留“名称”为“SiteDefinition1”，然后选择“添加”按钮    。

## <a name="create-a-visual-web-part"></a>创建可视 Web 部件
 接下来，创建要显示在站点定义主页上的可视 Web 部件。

#### <a name="to-create-a-visual-web-part"></a>创建可视 Web 部件

1. 在“解决方案资源管理器”中，选择“显示所有文件”按钮。

2. 选择“SiteDefinition1”项目节点，然后在菜单栏上选择“项目” > “添加新项”  。

     此时会显示“添加新项”对话框。

3. 展开“Visual C#”节点或“Visual Basic”节点，再展开“SharePoint”节点，然后选择“2010”节点   。

4. 在模板列表中，选择“可视 Web 部件”模板，保留默认名称“VisualWebPart1”，然后选择“添加”按钮 。

     VisualWebPart1.ascx 文件随即打开。

5. 在“VisualWebPart1.ascx”的底部，添加以下标记以向窗体添加三个控件：文本框、按钮和标签：

    ```aspx-csharp
    <table>
      <tr>
        <td>
          <asp:TextBox runat="server" ID="tbName"></asp:TextBox>
        </td>
        <td>
          <asp:Button runat="server" ID="btnSubmit" Text = "Change Label Text" OnClick="btnSubmit_Click"></asp:Button>
        </td>
        <td>
          <asp:Label runat="server" ID="lblName"></asp:Label>
        </td>
      </tr>
    </table>
    ```

6. 在“VisualWebPart1.ascx”下，打开“VisualWebPart1.ascx.cs”文件 ([!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)]) 或“VisualWebPart1.ascx.vb”文件 ([!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)])，然后添加以下代码：

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/testsitedefvb/sitedefinition/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/testsitedef/sitedefinition/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet1":::

     此代码为 Web 部件的按钮单击添加功能。

## <a name="add-the-visual-web-part-to-the-default-aspx-page"></a>将可视 Web 部件添加到默认 ASPX 页
 接下来，将可视 Web 部件添加到站点定义的默认 ASPX 页。

#### <a name="to-add-a-visual-web-part-to-the-default-aspx-page"></a>将可视 Web 部件添加到默认 ASPX 页

1. 打开 default.aspx 页，然后在 `WebPartPages` 标记下添加以下行：

    ```aspx-csharp
    <%@ Register Tagprefix="MyWebPartControls" Namespace="TestSiteDef.VisualWebPart1" Assembly="$SharePoint.Project.AssemblyFullName$" %>
    ```

     此行将名称 MyWebPartControls 与 Web 部件及其代码关联。 Namespace 参数与 VisualWebPart1.ascx 代码文件中使用的命名空间匹配。

2. 在 `</asp:Content>` 元素之后，将整个 `ContentPlaceHolderId="PlaceHolderMain"` 部分及其内容替换为以下代码：

    ```aspx-csharp
    <asp:Content ID="Content1" ContentPlaceHolderId="PlaceHolderMain" runat="server">
        <MyWebPartControls:VisualWebPart1 runat="server" />
    </asp:Content>
    ```

     此代码会创建一个对前面创建的可视 Web 部件的引用。

3. 在解决方案资源管理器中，打开“SiteDefinition1”节点的快捷菜单，然后选择“设为启动项”  。

## <a name="deploy-and-run-the-site-definition-solution"></a>部署并运行站点定义解决方案
 接下来，将项目部署到 SharePoint，然后运行该项目。

#### <a name="to-deploy-and-run-the-site-definition"></a>部署并运行网站定义

- 在菜单栏上，选择“生成” > “部署 TestSiteDef”。

- 选择 F5。

     Visual Studio 编译代码、添加其功能、将所有文件打包到 SharePoint 解决方案 (WSP) 文件中，并将 WSP 文件部署到 SharePoint Server。 然后，SharePoint 安装文件，然后激活功能。

## <a name="create-a-site-based-on-the-site-definition"></a>基于站点定义创建站点
 接下来，使用新的站点定义来创建站点。

#### <a name="to-create-a-site-by-using-the-site-definition"></a>使用新的站点定义来创建站点

1. 在 SharePoint 站点上，将显示“新建SharePoint 站点”页。

2. 在“标题和说明”部分中，输入“我的新站点”作为站点的标题和说明 。

3. 在“网站地址”部分，在“URL 名称”框中输入“mynewsite”。  

4. 在“模板”部分中，选择“SharePoint 自定义项”选项卡 。

5. 在“选择模板”列表中，选择“SiteDefinition1” 。

6. 将其他设置保留为默认值，然后选择“创建”按钮。

     新站点随即显示。

## <a name="test-the-new-site"></a>测试新站点
 接下来，测试新站点以验证它是否正常工作。

#### <a name="to-test-the-new-site"></a>测试新站点

- 在默认 ASPX 页上，输入一些文本，然后选择文本框旁边的“更改标签文本”按钮。

     该文本显示在按钮右侧标签中。

## <a name="see-also"></a>另请参阅
- [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
