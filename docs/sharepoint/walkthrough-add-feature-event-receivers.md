---
title: 演练：添加功能事件接收器 | Microsoft Docs
description: 在本演练中，添加功能事件接收器，这是安装、激活、停用或删除 SharePoint 功能时执行的方法。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, advanced packaging tools
- SharePoint development in Visual Studio, event receivers
- SharePoint development in Visual Studio, feature event receivers
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 58e4210244c09271741a89e2343bfaf06a6d2c20
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671843"
---
# <a name="walkthrough-add-feature-event-receivers"></a>演练：添加功能事件接收器
功能事件接收器是在 SharePoint 中发生以下与功能相关的事件之一时执行的方法：

- 功能已安装。

- 功能已激活。

- 功能已停用。

- 功能已删除。

本演练演示如何将事件接收器添加到 SharePoint 项目中的功能。 它演示以下任务：

- 使用功能事件接收器创建空项目。

- 处理 FeatureDeactivating 方法。

- 使用 SharePoint 项目对象模型向公告列表添加公告。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 Microsoft Windows 和 SharePoint 版本。

- Visual Studio。

## <a name="create-a-feature-event-receiver-project"></a>创建功能事件接收器项目
 首先，创建一个包含功能事件接收器的项目。

#### <a name="to-create-a-project-with-a-feature-event-receiver"></a>创建一个包含功能事件接收器的项目

1. 在菜单栏上，选择“文件”>“新建”>“项目”，打开“新建项目”对话框 >  >  。

2. 展开“Visual C#”或“Visual Basic”下的“SharePoint”节点，然后选择“2010”节点   。

3. 在“模板”窗格中，选择“SharePoint 2010 项目”模板 。

     将此项目类型用于功能事件接收器，因为它们没有项目模板。

4. 在“名称”框中，输入“FeatureEvtTest”，然后选择“确定”按钮以显示“SharePoint 自定义向导”   。

5. 在“指定用于调试的网站和安全级别”页中，输入要向其添加新自定义字段项的 SharePoint 网站的 URL，或使用默认位置 (http://\<*system name*>/)。

6. 在“此 SharePoint 解决方案的信任级别是什么?”部分中，选择“部署为场解决方案”选项按钮 。

     有关沙盒解决方案与场解决方案的详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 选择“完成”按钮，然后可以看到名为“Feature1”的功能出现在“功能”节点下 。

## <a name="add-an-event-receiver-to-the-feature"></a>向功能添加事件接收器
 接下来，将事件接收器添加到该功能，并添加在停用该功能时执行的代码。

#### <a name="to-add-an-event-receiver-to-the-feature"></a>向功能添加事件接收器

1. 打开“功能”节点的快捷菜单，然后选择“添加功能”以创建功能。

2. 在“功能”节点下，打开 Feature1 的快捷菜单，然后选择“添加事件接收器”以向该功能添加事件接收器  。

     这将在 Feature1 下添加一个代码文件。 在本例中，它被命名为 Feature1.EventReceiver.cs 或 Feature1.EventReceiver.vb，这取决于你的项目的开发语言 。

3. 如果你的项目是用 [!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)] 编写的，请在事件接收器的顶部添加以下代码（如果它还没有在那里）：

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/featureevttest2/features/feature1/feature1.eventreceiver.cs" id="Snippet1":::

4. 事件接收器类包含若干作为事件的注释掉的方法。 将 FeatureDeactivating 方法替换为以下内容：

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/featureevt2vb/features/feature1/feature1.eventreceiver.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/featureevttest2/features/feature1/feature1.eventreceiver.cs" id="Snippet2":::

## <a name="test-the-feature-event-receiver"></a>测试功能事件接收器
 接下来，停用该功能，测试 FeatureDeactivating 方法是否将公告输出到 SharePoint 公告列表。

#### <a name="to-test-the-feature-event-receiver"></a>测试功能事件接收器

1. 将项目的“活动部署配置”属性的值设置为“无激活” 。

     设置此属性可防止该功能在 SharePoint 中激活，并使你能够调试功能事件接收器。 有关详细信息，请参阅[调试 SharePoint 解决方案](../sharepoint/debugging-sharepoint-solutions.md)。

2. 按 F5 运行项目并将其部署到 SharePoint。

3. 在 SharePoint 网页顶部，打开“站点操作”菜单，然后选择“站点设置” 。

4. 在“站点设置”页的“站点操作”部分下，选择“管理站点功能”链接  。

5. 在“功能”页上，选择“FeatureEvtTest Feature1”功能旁边的“激活”按钮  。

6. 在“功能”页上，选择“FeatureEvtTest Feature1”功能旁边的“停用”按钮，然后选择“停用此功能”确认链接来停用该功能   。

7. 选择“主页”按钮。

     请注意，停用功能后，“公告”列表中会出现公告。

## <a name="see-also"></a>另请参阅

- [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)