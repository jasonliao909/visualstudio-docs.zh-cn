---
title: 演练：部署Project 任务列表定义|Microsoft Docs
description: 在此演练中，使用Visual Studio创建、自定义、调试和部署SharePoint跟踪项目任务。
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
ms.translationtype: MT
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

1. 打开"**新建Project"** 对话框，展开"SharePoint"**节点**，然后选择 **"2010"** 节点。

2. 在"**模板"** 窗格中，选择SharePoint **2010** Project模板，将项目命名 **为 ProjectTaskList**，然后选择"确定 **"** 按钮。

     将显示 **SharePoint自定义向导**。

3. 指定用于SharePoint本地解决方案站点，选择"部署 **为** 场解决方案"选项按钮，然后选择"完成 **"** 按钮。

4. 打开项目的快捷菜单，然后选择"**添加新**  >  **项"。**

5. 在" **模板"窗格中** ，选择" **列表"** 模板，然后选择"添加 **"** 按钮。

     将显示 **SharePoint自定义向导**。

6. 在"**要为列表显示什么名称？"** 框中，输入 **"Project 任务列表"。**

7. 选择"**基于选项** 的现有列表类型创建不可自定义的列表"按钮，然后在列表列表中选择"任务"，然后选择"完成 **"** 按钮。

     列表、特性和包显示在 **解决方案资源管理器。**

## <a name="add-an-event-receiver"></a>添加事件接收器

在任务列表中，可以添加自动设置任务的截止日期和说明的事件接收器。 以下过程将一个简单的事件处理程序作为事件接收器添加到列表实例。

1. 打开项目节点的快捷菜单，选择"**添加"，** 然后选择"**新建项"。**

2. 在模板列表SharePoint，选择"事件接收器"模板，然后将它命名为 **"ProjectTaskListEventReceiver"。**

     将显示 **SharePoint自定义向导**。

3. 在"**选择事件接收器设置"** 页上，在"你想要的事件接收者类型"列表中选择"列出项事件"作为 **事件接收器** 类型。

4. 在"**什么项应为事件源"列表中**，选择"任务 **"。**

5. 在要处理的事件列表中，选中"已添加项"旁边的复选框，然后选择"完成 **"** 按钮。

     新的事件接收器节点将添加到项目，其代码文件名为 **ProjectTaskListEventReceiver**。

6. 将代码添加到 `ItemAdded` **ProjectTaskListEventReceiver** 代码文件中的方法。 每次添加新任务时，会向任务添加默认截止日期和说明。 默认截止日期为 2009 年 7 月 1 日。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projecttasklist1/projecttasklisteventreceiver/projecttasklisteventreceiver.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projecttasklist/projecttasklisteventreceiver/projecttasklisteventreceiver.cs" id="Snippet1":::

## <a name="customize-the-project-task-list-feature"></a>自定义项目任务列表功能

创建一个SharePoint解决方案时，Visual Studio自动为默认项目项创建功能。 可以使用功能设计器自定义SharePoint站点的项目任务列表设置。

1. 在 **解决方案资源管理器** 中，展开"**功能"。**

2. 打开 **Feature1 的快捷菜单**，然后选择"视图设计器"。 

3. 在"**标题"** 框中，**输入"Project 任务列表功能"。**

4. 在"**作用域"** 列表中，选择 **"Web"。**

5. 在" **属性** "窗口中，输入 **1.0.0.0** 作为 **Version 属性的值** 。

## <a name="customize-the-project-task-list-package"></a>自定义项目任务列表包

创建项目SharePoint，Visual Studio将包含默认项目项的功能添加到包。 可以使用包设计器自定义SharePoint站点的项目任务列表设置。

1. 在 **"SolutionExplorer"** 中，打开"包"的快捷 **菜单，然后选择****"视图设计器"。**

2. 在" **名称"** 框中，输入 **ProjectTaskListPackage**。

3. 选中" **重置 Web 服务器** "复选框。

## <a name="build-and-test-the-project-task-list"></a>生成并测试项目任务列表

运行项目时，将打开SharePoint站点。 但是，必须手动导航到任务列表的位置。

1. 选择 **F5** 键以生成和部署项目任务列表。

     随即SharePoint站点。

2. 选择" **主页"** 选项卡。

3. 在左侧边栏中，**选择Project 任务列表链接**。

     将显示Project 任务列表页。

4. 在" **列表工具"** 选项卡中，选择" **项"** 选项卡。

5. 在" **项"** 组中，选择" **新建项"** 按钮。

6. 在" **标题"** 文本框中，输入 **Task1**。

7. 选择"保存 **"** 按钮。

     刷新站点后 **，Task1** 任务将显示为到期日期 2009/7/1。

8. 选择 **"Task1"。**

     此时会显示任务的详细视图，说明显示"这是一项关键任务"。

## <a name="deploy-the-project-task-list"></a>部署项目任务列表

生成并测试项目任务列表后，可以将其部署到本地 *系统* 或 *远程系统*。 本地系统是开发解决方案的同一台计算机，而远程系统是一台不同的计算机。

### <a name="to-deploy-the-project-task-list-to-the-local-system"></a>将项目任务列表部署到本地系统

在"Visual Studio栏上，选择"**生成**  >  **部署解决方案"。**

Visual Studio IIS 应用程序池，收回解决方案的任何现有版本，将解决方案包 (*.wsp*) 文件复制到 SharePoint，然后激活其功能。 现在可以在 SharePoint 中使用此解决方案。 有关部署配置步骤详细信息，请参阅[如何：](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)编辑SharePoint配置。

### <a name="to-deploy-the-project-task-list-to-a-remote-system"></a>将项目任务列表部署到远程系统

1. 在菜单Visual Studio栏上，选择"生成 **发布**  >  **"。**

2. 在" **发布"** 对话框中，选择" **发布到文件系统"** 选项按钮。

     可以通过选择省略号按钮"省略号图标"，然后导航到其他位置，在![](../sharepoint/media/ellipsisicon.gif "“省略号”图标")"发布"对话框中更改目标位置。

3. 选择 **“发布”** 按钮。

     为 *解决方案创建 .wsp* 文件。

4. 将 *.wsp 文件* 复制到远程SharePoint系统。

5. 使用 PowerShell `Add-SPUserSolution` 命令在远程客户端安装SharePoint包。  (场解决方案，请使用 `Add-SPSolution` command.) 

     例如，`Add-SPUserSolution C:\MyProjects\ProjectTaskList\ProjectTaskList\bin\Debug\ProjectTaskList.wsp`。

6. 使用 PowerShell `Install-SPUserSolution` 命令部署解决方案。  (场解决方案，请使用 `Install-SPSolution` command.) 

     例如，`Install-SPUserSolution -Identity ProjectTaskList.wsp -Site http://NewSiteName`。

     有关远程部署的更多信息，请参阅[2010](http://www.dotnetmafia.com/blogs/dotnettipoftheday/archive/2009/12/02/adding-and-deploying-solutions-with-powershell-in-sharepoint-2010.aspx)年 10 月中的 Using [Solutions](/previous-versions/office/developer/sharepoint-2010/ee534972(v=office.14)) and Adding and Deploying Solutions with PowerShell（使用解决方案和通过 PowerShell SharePoint部署解决方案）。

## <a name="next-steps"></a>后续步骤

可以从以下主题详细了解如何自定义和SharePoint解决方案：

- [演练：创建 SharePoint 的网站栏、内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)

- [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)

- [Windows PowerShell Server 2010 SharePoint](/powershell/module/sharepoint-server)

## <a name="see-also"></a>另请参阅
[打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
