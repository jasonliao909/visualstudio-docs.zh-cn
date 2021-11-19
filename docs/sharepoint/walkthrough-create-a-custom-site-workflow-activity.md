---
title: 演练：创建自定义站点工作流活动|Microsoft Docs
description: 在此演练中，请参阅如何使用 Visual Studio 为站点级工作流创建自定义SharePoint活动。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom workflow activities [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, custom workflow activities
- site workflows [SharePoint development in Visual Studio]
- workflow activities [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, site workflows
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 8a7beaea3b9a7becc2b162304287b4e1b340fceb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664143"
---
# <a name="walkthrough-create-a-custom-site-workflow-activity"></a>演练：创建自定义站点工作流活动
  本演练演示如何使用 为站点级工作流创建自定义活动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。  (级工作流应用于整个站点，而不只是站点上的列表。) 自定义活动会创建备份公告列表，然后将公告列表的内容复制到其中。

 本演练演示了下列任务：

- 创建站点级工作流。

- 创建自定义工作流活动。

- 创建和删除SharePoint列表。

- 将项从一个列表复制到另一个列表。

- 在"快速启动"栏上显示列表。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 和 [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] SharePoint。

- Visual Studio。

## <a name="create-a-site-workflow-custom-activity-project"></a>创建站点工作流自定义活动项目
 首先，创建一个项目来保存和测试自定义工作流活动。

#### <a name="to-create-a-site-workflow-custom-activity-project"></a>创建站点工作流自定义活动项目

1. 在菜单栏上，选择"**文件**  >    >  **""新建Project** 以显示"新建Project对话框。

2. 展开SharePoint  **Visual C#** 或 **Visual Basic节点，** 然后选择 **"2010"** 节点。

3. 在"**模板"窗格中**，选择SharePoint **2010 Project** 模板。

4. 在" **名称"** 框中，输入 **"AnnouncementBackup"，** 然后选择"确定 **"** 按钮。

     将显示 **SharePoint自定义向导**。

5. 在"**指定** 用于调试的站点和安全级别"页上，选择"部署 **为** 场解决方案"选项按钮，然后选择"完成"按钮以接受信任级别和默认站点。

     此步骤将解决方案的信任级别设置为场解决方案，这是工作流项目的唯一可用选项。

6. 在 **解决方案资源管理器** 中，选择项目节点，然后在菜单栏上选择  >  **"Project"添加新项"。**

7. 在 **Visual C#** 或 **Visual Basic** 下，展开 **SharePoint节点，** 然后选择 **"2010"** 节点。

8. 在" **模板"窗格中** ，选择"仅场解决方案 (**顺序** 工作流) 模板，然后选择"添加 **"** 按钮。

     将显示 **SharePoint自定义向导**。

9. 在" **指定调试的工作流** 名称"页上，接受"AnnouncementBackup - Workflow1" (的默认) 。 将工作流模板类型更改为 **"站点工作流"，** 然后选择"下一 **步"** 按钮。

10. 选择" **完成"** 按钮以接受剩余的默认设置。

## <a name="add-a-custom-workflow-activity-class"></a>添加自定义工作流活动类
 接下来，向项目添加一个类，以包含自定义工作流活动的代码。

#### <a name="to-add-a-custom-workflow-activity-class"></a>添加自定义工作流活动类

1. 在菜单栏上，选择  >  **Project"添加新项**"以显示"**添加新项**"对话框。

2. 在"**已安装的模板"** 树视图中，选择"代码"节点，然后在项目项模板列表中选择"类"模板。 使用默认名称 Class1。 选择“添加”按钮。

3. 将 Class1 中所有代码替换为以下内容：

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/announcementbackup/class1.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/announcementbackupvb/class1.vb" id="Snippet1":::

4. 保存项目，然后在菜单栏上选择"生成 **生成**  >  **解决方案"。**

     Class1 在"公告""回退组件"选项卡上的 **"** 工具箱" **中显示为自定义** 操作。

## <a name="add-the-custom-activity-to-the-site-workflow"></a>将自定义活动添加到站点工作流
 接下来，将活动添加到工作流以包含自定义代码。

#### <a name="to-add-a-custom-activity-to-the-site-workflow"></a>将自定义活动添加到站点工作流

1. 在设计视图中的工作流设计器中打开 Workflow1。

2. 从"工具箱"拖动 **Class1，** 以便它出现在活动下，或打开 Class1 的快捷菜单，选择"复制"，打开活动下行的快捷菜单，然后选择 `onWorkflowActivated1`  `onWorkflowActivated1` "粘贴 **"。**

3. 保存项目。

## <a name="test-the-site-workflow-custom-activity"></a>测试站点工作流自定义活动
 接下来，运行项目并启动站点工作流。 自定义活动创建备份公告列表，将当前公告列表中的内容复制到该列表。 该代码还会在创建备份列表之前检查备份列表是否已存在。 如果备份列表已存在，则删除它。 该代码还会添加指向新列表的链接，SharePoint网站的"快速启动"栏上。

#### <a name="to-test-the-site-workflow-custom-activity"></a>测试站点工作流自定义活动

1. 选择 **F5** 键以运行项目，并部署到SharePoint。

2. 在"快速启动"栏上，选择"列表"链接以显示在"快速启动"站点中SharePoint列表。 请注意，只有一个名为"公告" **的公告列表**。

3. 在"站点工作流"SharePoint，选择"**站点工作流"** 链接。

4. 在"启动新工作流"部分下，选择 **"AnnouncementBackup - Workflow1"** 链接。 这会启动站点工作流，并运行自定义操作中的代码。

5. 在"快速启动"栏上，选择" **公告备份"** 链接。 请注意，"公告"列表中包含的所有公告已复制到此新列表。

## <a name="see-also"></a>另请参阅
- [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
