---
title: 演练：部署项目任务列表定义 | Microsoft Docs
description: 本演练使用 Visual Studio 创建、自定义、调试和部署 SharePoint 列表以跟踪项目任务。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 88b4be482cc0ad99829a065b8bc423258b69de49
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665268"
---
# <a name="walkthrough-deploy-a-project-task-list-definition"></a>演练：部署项目任务列表定义

本演练演示如何使用 [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] 创建、自定义、调试和部署 SharePoint 列表以跟踪项目任务。

[!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件

- 支持的 Microsoft Windows 和 SharePoint 版本。

- Visual Studio 2017 或 Azure DevOps Services。

## <a name="create-a-sharepoint-list"></a>创建 SharePoint 列表

创建 SharePoint 列表项目，并将该列表定义与任务相关联。

1. 打开“新建项目”对话框，再展开“SharePoint”节点，然后选择“2010”节点  。

2. 在“模板”窗格中，选择“SharePoint 2010 项目”模板，将此项目命名为 ProjectTaskList，然后选择“确定”按钮   。

     “SharePoint 自定义向导”随即出现。

3. 指定用于调试的本地 SharePoint 网站，选择“部署为场解决方案”选项按钮，然后选择“完成”按钮 。

4. 打开项目的快捷菜单，然后选择“添加” > “新建项” 。

5. 在“模板”窗格中，选择“列表”模板，然后选择“添加”按钮  。

     “SharePoint 自定义向导”随即出现。

6. 在“你希望列表的显示名称是什么?”框中，输入“项目任务列表” 。

7. 选择“基于现有列表类型创建不可自定义的列表”选项按钮，然后在其列表中依次选择“任务”、“完成”按钮  。

     列表、功能和包显示在“解决方案资源管理器”中。

## <a name="add-an-event-receiver"></a>添加事件接收器

在任务列表中，可以添加自动设置任务的截止日期和说明的事件接收器。 下面的过程可将一个简单的事件处理程序作为事件接收器添加到列表实例中。

1. 打开项目节点的快捷菜单，选择“添加”，然后选择“新建项” 。

2. 在 SharePoint 模板列表中，选择“事件接收器”模板，然后将其命名为 ProjectTaskListEventReceiver 。

     “SharePoint 自定义向导”随即出现。

3. 在“选择事件接收器设置”页上，在“需要哪种类型的事件接收器”列表中选择“列表项事件”作为事件接收器类型  。

4. 在“哪个项应为事件源”列表中，选择“任务” 。

5. 在要处理的事件列表中，选择“已添加项”旁边的复选框，然后选择“完成”按钮 。

     新的事件接收器节点将通过名为 ProjectTaskListEventReceiver 的代码文件添加到项目中。

6. 向 ProjectTaskListEventReceiver 代码文件中的 `ItemAdded` 方法添加代码。 每次添加新任务时，都会向任务添加默认的截止日期和描述。 默认截止日期为 2009 年 7 月 1 日。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projecttasklist1/projecttasklisteventreceiver/projecttasklisteventreceiver.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projecttasklist/projecttasklisteventreceiver/projecttasklisteventreceiver.cs" id="Snippet1":::

## <a name="customize-the-project-task-list-feature"></a>自定义项目任务列表功能

创建 SharePoint 解决方案时，Visual Studio 会自动为默认项目项创建功能。 你可使用功能设计器自定义 SharePoint 网站的项目任务列表设置。

1. 在“解决方案资源管理器”中，展开“功能” 。

2. 打开“Feature1”的快捷菜单，然后选择“查看设计器” 。

3. 在“标题”框中，输入“项目任务列表功能” 。

4. 在“范围”列表中，选择“Web” 。

5. 在“属性”窗口中，输入 1.0.0.0 作为“版本”属性的值  。

## <a name="customize-the-project-task-list-package"></a>自定义项目任务列表包

创建 SharePoint 项目时，Visual Studio 会自动将包含默认项目项的功能添加到包中。 你可使用包设计器自定义 SharePoint 网站的项目任务列表设置。

1. 在解决方案资源管理器中，打开“包”的快捷菜单，然后选择“查看设计器”  。

2. 在“名称”框中，输入 ProjectTaskListPackage 。

3. 选择“重置 Web 服务器”复选框。

## <a name="build-and-test-the-project-task-list"></a>生成并测试项目任务列表

运行该项目时，SharePoint 网站将打开。 但你必须手动导航到任务列表的位置。

1. 选择 F5 键以生成并部署项目任务列表。

     SharePoint 网站随即打开。

2. 选择“主页”选项卡。

3. 在左侧栏中，选择“项目任务列表”链接。

     “项目任务列表”页随即显示。

4. 在“列表工具”选项卡中，选择“项”选项卡 。

5. 在“项”组中，选择“新建项”按钮 。

6. 在“标题”文本框中，输入 Task1 。

7. 选择“保存”按钮。

     刷新网站后，Task1 任务将会出现，其截止日期为 2009/7/1。

8. 选择“Task1”。

     此时将显示任务的详细视图，并且其描述显示“这是一项关键任务。”

## <a name="deploy-the-project-task-list"></a>部署项目任务列表

生成并测试项目任务列表后，可以将其部署到“本地系统”或“远程系统” 。 本地系统是在其上开发解决方案的计算机，而远程系统是另一台计算机。

### <a name="to-deploy-the-project-task-list-to-the-local-system"></a>将项目任务列表部署到本地系统

在 Visual Studio 菜单栏上，依次选择“生成” > “部署解决方案” 。

Visual Studio 回收 IIS 应用程序池，收回解决方案的任何现有版本，将解决方案包 (.wsp) 文件复制到 SharePoint，然后激活其功能。 现在即可在 SharePoint 中使用该解决方案。 有关部署配置步骤的详细信息，请参阅[操作指南：编辑 SharePoint 部署配置](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)。

### <a name="to-deploy-the-project-task-list-to-a-remote-system"></a>将项目任务列表部署到远程系统

1. 在 Visual Studio 菜单栏上，依次选择“生成” > “发布” 。

2. 在“发布”对话框中，选择“发布到文件系统”选项按钮 。

     若要更改目标位置，可在“发布”对话框中选择省略号按钮 ![省略号图标](../sharepoint/media/ellipsisicon.gif "“省略号”图标")，然后导航到另一位置。

3. 选择 **“发布”** 按钮。

     将为此解决方案创建 .wsp 文件。

4. 将 .wsp 文件复制到远程 SharePoint 系统。

5. 使用 PowerShell `Add-SPUserSolution` 命令在远程 SharePoint 安装上安装包。 （对于场解决方案，请使用 `Add-SPSolution` 命令。）

     例如，`Add-SPUserSolution C:\MyProjects\ProjectTaskList\ProjectTaskList\bin\Debug\ProjectTaskList.wsp`。

6. 使用 PowerShell `Install-SPUserSolution` 命令来部署解决方案。 （对于场解决方案，请使用 `Install-SPSolution` 命令。）

     例如，`Install-SPUserSolution -Identity ProjectTaskList.wsp -Site http://NewSiteName`。

     有关远程部署的详细信息，请参阅[使用解决方案](/previous-versions/office/developer/sharepoint-2010/ee534972(v=office.14))和[使用 PowerShell 在 SharePoint 2010 中添加和部署解决方案](http://www.dotnetmafia.com/blogs/dotnettipoftheday/archive/2009/12/02/adding-and-deploying-solutions-with-powershell-in-sharepoint-2010.aspx)。

## <a name="next-steps"></a>后续步骤

若要详细了解如何自定义和部署 SharePoint 解决方案，请参阅以下主题：

- [演练：创建 SharePoint 的网站栏、内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)

- [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)

- [适用于 SharePoint Server 2010 的 Windows PowerShell](/powershell/module/sharepoint-server)

## <a name="see-also"></a>另请参阅
[打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
