---
title: 使用设计器为 SharePoint 创建 Web 部件
description: 在本演练中，使用 Visual Studio 中的 SharePoint 可视 Web 部件项目模板以可视方式创建 Web 部件。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665272"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint-by-using-a-designer"></a>演练：使用设计器为 SharePoint 创建 Web 部件

如果为 SharePoint 站点创建 Web 部件，用户可以使用浏览器直接修改该站点中页面的内容、外观和行为。 本演练演示如何使用 Visual Studio 中的 SharePoint 可视 Web 部件项目模板以可视化方式创建 Web 部件。

你将创建的 Web 部件将显示月历视图，以及站点上每个日历列表的复选框。 用户可以通过选中复选框来指定要包含在月历视图中的日历列表。

本演练演示以下任务：

- 使用可视 Web 部件项目模板创建 Web 部件。
- 使用 Visual Studio 中的可视 Web 开发人员设计器设计 Web 部件。
- 添加代码以处理 Web 部件上的控件的事件。
- 在 SharePoint 中测试 Web 部件。

    > [!NOTE]
    > 以下说明中的 Visual Studio 用户界面的某些元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件

您需要满足以下条件才能完成本演练：

- 支持的 Windows 和 SharePoint 版本。

## <a name="create-a-web-part-project"></a>创建 Web 部件项目

首先，使用可视 Web 部件项目模板创建 Web 部件。

1. 使用“以管理员身份运行”选项启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。
::: moniker range="=vs-2017"

3. 在“新建项目”对话框中，展开 Visual C# 或 Visual Basic 下的“Office/SharePoint”，然后选择“SharePoint 解决方案”类别。

4. 在模板列表中，选择“SharePoint 2013 - 可视 Web 项目”模板，然后选择“确定”按钮。

     “SharePoint 自定义向导”随即出现。 使用此向导，可以指定用于调试项目的站点和解决方案的信任级别。
::: moniker-end
::: moniker range=">=vs-2019"
3. 在“创建新项目”对话框中，为已安装的 SharePoint 的特定版本选择“SharePoint 空项目”。 例如，如果安装了 SharePoint 2019，请选择“SharePoint 2019 - 空项目”模板。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

4. 在“名称”框中，输入“TestProject1”，然后选择“创建”按钮。

::: moniker-end
5. 在“此 SharePoint 解决方案的信任级别是什么?”部分中，选择“部署为场解决方案”选项按钮。

6. 选择“完成”按钮以接受默认的本地 SharePoint 站点。

## <a name="designing-the-web-part"></a>设计 Web 部件

通过将“工具箱”中的控件添加到可视 Web 开发人员设计器的图面来设计 Web 部件。

1. 在可视 Web 开发人员设计器中，选择“设计”选项卡以切换到“设计”视图。

2. 在菜单栏上，依次选择“视图” > “工具箱” 。

3. 在“工具箱”的“标准”节点中，选择“CheckBoxList”控件，然后执行以下步骤之一：

    - 打开“CheckBoxList”控件的快捷菜单，选择“复制”，打开设计器中第一行的快捷菜单，然后选择“粘贴”。

    - 从“工具箱”中拖动“CheckBoxList”控件，并将该控件连接到设计器中的第一行。

4. 重复前面的步骤，但将按钮移动到设计器的下一行。

5. 在设计器中，选择“Button1”按钮。

6. 在菜单栏上，选择“视图” > “属性窗口”。

     此时将打开“属性”窗口。

7. 在按钮的“文本”属性中，输入“更新”。

## <a name="handling-the-events-of-controls-on-the-web-part"></a>处理 Web 部件上的控件的事件

添加使用户能够将日历添加到母版日历视图中的代码。

1. 执行下面的某一组步骤：

   - 在设计器中，双击“更新”按钮。

   - 在“更新”按钮的“属性”窗口中，选择“事件”按钮。 在“单击”属性中，输入 Button1_Click，然后选择 Enter 键。

     用户控件代码文件将在代码编辑器中打开，并且将显示 `Button1_Click` 事件处理程序。 稍后，你将向此事件处理程序中添加代码。

2. 将下面的语句添加到用户控件代码文件的顶部。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet1":::

3. 将以下代码行添加到 `VisualWebPart1` 类。 此代码声明月历视图控件。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet2":::

4. 将 `VisualWebPart1` 类的 `Page_Load` 方法替换为以下代码。 此代码执行以下任务：

   - 向用户控件添加月历视图。

   - 为站点上的每个日历列表添加一个复选框。

   - 为日历视图中显示的每种类型的项指定模板。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet3":::

5. 将 `VisualWebPart1` 类的 `Button1_Click` 方法替换为以下代码。 此代码将每个选定日历中的项添加到母版日历视图中。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet4":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet4":::

## <a name="test-the-web-part"></a>测试 Web 部件

运行该项目时，SharePoint 站点将打开。 Web 部件会自动添加到 SharePoint 中的 Web 部件库。 若要测试此项目，你将执行以下任务：

- 向两个单独日历列表中的每个列表添加一个事件。
- 将 Web 部件添加到 Web 部件页。
- 指定要包含在月历视图中的列表。

### <a name="to-add-events-to-calendar-lists-on-the-site"></a>向站点上的日历列表添加事件

1. 在 Visual Studio 中，选择“F5”键。

     此时将打开 SharePoint 站点，[!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 快速启动栏将显示在该页上。

2. 在快速启动栏上的“列表”下，选择“日历”链接。

     “日历”页面随即出现。

     如果快速启动栏上未显示“日历”链接，请选择“网站内容”链接。 如果“网站内容”页不显示“日历”项，请创建一个。

3. 在“日历”页上，选择一天，然后选择所选日期中的“添加”链接以添加一个事件。

4. 在“标题”框中，输入“默认日历中的事件”，然后选择“保存”按钮  。

5. 选择“网站内容”链接，然后选择“添加应用”磁贴。

6. 在“创建”页上，选择“日历”类型，为日历命名，然后选择“创建”按钮。

7. 向新日历添加事件，将事件命名为“自定义日历中的事件”，然后选择“保存”按钮。

### <a name="to-add-the-web-part-to-a-web-part-page"></a>将 Web 部件添加到 Web 部件页

1. 在“网站内容”页上，打开“网站页面”文件夹。

2. 在功能区上，选择“文件”选项卡，打开“新建文档”菜单，然后选择“Web 部件页面”命令。

3. 在“新建 Web 部件页面”页上，将该页命名为“SampleWebPartPage.aspx”，然后选择“创建”按钮  。

     Web 部件页面随即出现。

4. 在该 Web 部件页面顶部选择“插入”选项卡，然后选择“Web 部件”按钮 。

5. 依次选择“自定义”文件夹、“VisualWebPart1”Web 部件，然后选择“添加”按钮  。

     该 Web 部件随即显示在页面上。 以下控件显示在 Web 部件上：

    - 月历视图。

    - “更新”按钮。

    - “日历”复选框。

    - “自定义日历”复选框。

### <a name="to-specify-lists-to-include-in-the-monthly-calendar-view"></a>指定要包含在月历视图中的列表

在 Web 部件中，指定要包含在月历视图中的日历，然后选择“更新”按钮。

指定的所有日历中的事件均显示在月历视图中。

## <a name="see-also"></a>另请参阅

[为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
[如何：创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)
[演练：为 SharePoint 创建 Web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
