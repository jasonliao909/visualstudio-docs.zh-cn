---
title: 使用设计器为SharePoint Web 部件
description: 在此演练中，使用 SharePoint Visual Web 部件项目模板以可视Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], designer
- Web Parts [SharePoint development in Visual Studio], creating
- Web Parts [SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 2a00ea5c8720c02b9dbdbd8a6fad7fa7657efeb5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122130788"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint-by-using-a-designer"></a>演练：使用设计器为 SharePoint 创建 Web 部件

如果为 web 站点SharePoint Web 部件，则用户可以使用浏览器直接修改该站点中页面的内容、外观和行为。 本演练演示如何使用 SharePoint **Visual Web 部件** 项目模板以可视Visual Studio。

你将创建的 Web 部件显示每月日历视图，以及站点上每个日历列表的复选框。 用户可以通过选中复选框来指定要包括在每月日历视图中的日历列表。

本演练演示以下任务：

- 使用 Visual Web 部件项目模板 **创建 Web** 部件。
- 使用 Visual Studio 中的 Visual Web 开发人员设计器设计 Web 部件。
- 添加代码以处理 Web 部件上的控件事件。
- 在 SharePoint 中测试 Web 部件。

    > [!NOTE]
    > 你的计算机可能会显示用户界面某些元素的不同名称或位置，Visual Studio说明中的内容。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件

您需要满足以下条件才能完成本演练：

- 支持的 Windows 和 SharePoint。

## <a name="create-a-web-part-project"></a>创建 Web 部件项目

首先，使用 Visual Web 部件项目模板 **创建 Web** 部件项目。

1. 首先 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 使用" **以管理员方式运行"** 选项。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。
::: moniker range="=vs-2017"

3. 在 **"新建Project"** 对话框中的 **"Visual C#"** 或"Visual Basic"下，展开"Office/SharePoint"，然后选择"SharePoint **解决方案"** 类别。  

4. 在模板列表中，选择"SharePoint **2013 - Visual Web 部件**"模板，然后选择"确定 **"** 按钮。

     将显示 **SharePoint自定义向导**。 使用此向导，可以指定用于调试项目的站点和解决方案的信任级别。
::: moniker-end
::: moniker range=">=vs-2019"
3. 在"**创建新Project"对话框中**，SharePoint已安装Project特定版本的SharePoint"空版本*"。 例如，如果安装了 2019 SharePoint，请选择"SharePoint **2019 - 空** Project模板。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

4. 在" **名称"** 框中，输入 **"TestProject1"，** 然后选择"创建 **"** 按钮。

::: moniker-end
5. 在"**此解决方案的信任级别SharePoint？"** 部分中，选择"部署 **为场解决方案"** 选项按钮。

6. 选择"**完成**"按钮以接受默认本地SharePoint站点。

## <a name="designing-the-web-part"></a>设计 Web 部件

通过将"工具箱"中的控件添加到 Visual  Web 开发人员设计器的图面来设计 Web 部件。

1. 在 Visual Web 开发人员设计器上，选择"设计 **"** 选项卡以切换到设计视图。

2. 在菜单栏上，选择"查看 **工具箱**  >  **"。**

3. 在" **工具箱** "的"标准" **节点中，** 选择 **CheckBoxList** 控件，然后执行以下步骤之一：

    - 打开 **CheckBoxList** 控件的快捷菜单，选择 **"复制**"，打开设计器中第一行的快捷菜单，然后选择"粘贴 **"。**

    - 从" **工具箱"拖动 CheckBoxList** **控件**，并将该控件连接到设计器的第一行。

4. 重复上一步，但将"按钮"移动到设计器的下一行。

5. 在设计器中，选择 **"Button1"** 按钮。

6. 在菜单栏上，选择"查看  >  **属性窗口"。**

     此时将打开“属性”窗口。

7. 在按钮 **的"文本**"属性中，输入"**更新"。**

## <a name="handling-the-events-of-controls-on-the-web-part"></a>处理 Web 部件上的控件事件

添加使用户能够将日历添加到主日历视图的代码。

1. 执行下面的某一组步骤：

   - 在设计器中，双击"更新 **"** 按钮。

   - 在" **更新"** 按钮的" **属性"** 窗口中，选择" **事件"** 按钮。 在" **单击** "属性中 **Button1_Click，** 然后选择 Enter 键。

     用户控件代码文件将在代码编辑器中打开， `Button1_Click` 并且事件处理程序随即出现。 稍后，你将向此事件处理程序添加代码。

2. 将以下 语句添加到用户控件代码文件的顶部。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet1":::

3. 将以下代码行添加到 `VisualWebPart1` 类。 此代码声明每月日历视图控件。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet2":::

4. 将 `Page_Load` 类的 `VisualWebPart1` 方法替换为以下代码。 此代码执行以下任务：

   - 将每月日历视图添加到用户控件。

   - 为站点上的每个日历列表添加一个复选框。

   - 为日历视图中显示的每种类型的项指定模板。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet3":::

5. 将 `Button1_Click` 类的 `VisualWebPart1` 方法替换为以下代码。 此代码将每个选定日历中的项添加到主日历视图。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet4":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet4":::

## <a name="test-the-web-part"></a>测试 Web 部件

运行项目时，将打开SharePoint站点。 Web 部件会自动添加到 Web 部件库中的 SharePoint。 若要测试此项目，需要执行以下任务：

- 将事件添加到两个单独的日历列表的每一个。
- 将 Web 部件添加到 Web 部件页。
- 指定要包括在每月日历视图中的列表。

### <a name="to-add-events-to-calendar-lists-on-the-site"></a>将事件添加到站点上的日历列表

1. 在Visual Studio中，选择 **F5** 键。

     "SharePoint"站点随即打开，快速启动 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 栏显示在页面上。

2. 在快速启动栏的 **"列表"下**，选择" **日历"** 链接。

     将显示 **"日历** "页。

     如果"日历"链接未显示在快速启动栏上，请选择" **站点内容"** 链接。 如果"站点内容"页未显示" **日历"** 项，请创建一个。

3. 在"日历"页上，选择一天，然后选择所选日期 **中的"** 添加"链接以添加事件。

4. 在" **标题** "框中，在默认日历中输入" **事件**"，然后选择"保存 **"** 按钮。

5. 选择" **站点内容"** 链接，然后选择" **添加应用"磁贴** 。

6. 在" **创建** "页上，选择 **"日历** 类型"，为日历命名，然后选择"创建 **"** 按钮。

7. 将事件添加到新日历，在自定义日历中将事件命名，然后选择"保存 **"** 按钮。

### <a name="to-add-the-web-part-to-a-web-part-page"></a>将 Web 部件添加到 Web 部件页

1. 在" **站点内容"** 页上，打开 **"网站页"** 文件夹。

2. 在功能区上，选择" **文件"** 选项卡，打开" **新建文档"** 菜单，然后选择 **"Web 部件页"** 命令。

3. 在" **新建 Web 部件页"** 页上，将页面名称为 **SampleWebPartPage.aspx**，然后选择"创建 **"** 按钮。

     将显示 Web 部件页。

4. 在 Web 部件页的顶部区域中，选择"插入 **"** 选项卡，然后选择 **"Web 部件"** 按钮。

5. 选择" **自定义** "文件夹，选择 **"VisualWebPart1"Web** 部件，然后选择"添加 **"** 按钮。

     Web 部件显示在页面上。 以下控件显示在 Web 部件上：

    - 每月日历视图。

    - " **更新"** 按钮。

    - " **日历** "复选框。

    - " **自定义日历"** 复选框。

### <a name="to-specify-lists-to-include-in-the-monthly-calendar-view"></a>指定要包括在每月日历视图中的列表

在 Web 部件中，指定要包括在每月日历视图中的日历，然后选择"更新 **"** 按钮。

指定的所有日历中的事件将显示在每月日历视图中。

## <a name="see-also"></a>请参阅

[创建 web 部件SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md) 
[如何：创建SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md) 
[演练：创建 web 部件以用于SharePoint](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
