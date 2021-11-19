---
title: 如何：创建事件接收器 | Microsoft Docs
description: 创建事件接收器，以便你可以在用户与 SharePoint 项（如列表或列表项）交互时做出响应。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.SPE.EventReceiver
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, event receivers
- event receivers [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 66b62a619b64534f56039e6213b01d4d12bb941a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663846"
---
# <a name="how-to-create-an-event-receiver"></a>如何：创建事件接收器
  通过创建事件接收器，你可以在用户与 SharePoint 项（如列表或列表项）交互时做出响应。 例如，当用户更改日历或删除联系人列表中的名称时，可以触发事件接收器中的代码。 使用以下主题，可以了解如何向列表实例添加事件接收器。

 若要完成这些步骤，必须已安装 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和支持的 Windows 和 SharePoint 版本。 由于此示例需要 SharePoint 项目，因此还必须已完成[演练：创建 SharePoint 的网站栏、内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)主题中的过程。

## <a name="adding-an-event-receiver"></a>添加事件接收器
 在[演练：创建 SharePoint 的网站栏、内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)中创建的项目包括自定义网站栏、自定义列表和内容类型。 在下面的过程中，你将通过将一个简单的事件处理程序（事件接收器）添加到列表实例中来扩展此项目，演示如何处理 SharePoint 项（如列表）中发生的事件。

#### <a name="to-add-an-event-receiver-to-the-list-instance"></a>向列表实例添加事件接收器

1. 打开在[演练：创建 SharePoint 的网站栏、内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)中创建的项目。

2. 在“解决方案资源管理器”中，选择名为“Clinic”的 SharePoint 项目节点。

3. 在菜单栏上，依次选择“项目” > “添加新项”。

4. 在“Visual C#”或“Visual Basic”下，展开“SharePoint”节点，然后选择“2010”项。

5. 在“模板”窗格中，选择“事件接收器”，将其命名为“TestEventReceiver1”，然后选择“确定”按钮。

     “SharePoint 自定义向导”随即出现。

6. 在“需要哪种类型的事件接收器?”列表中，选择“列表项事件”。

7. 在“哪个项应为事件源?”列表中，选择“患者(诊所\患者)”。

8. 在“处理以下事件”列表中，选中“已添加项”旁边的复选框，然后选择“完成”按钮。

     新事件接收器的代码文件包含名为 `ItemAdded` 的单个方法。 下一步，你将向此方法添加代码，以便默认情况下将每个联系人都命名为 Scott Brown。

9. 将现有的 `ItemAdded` 方法替换为以下代码，然后选择 F5 键：

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/CustomField1/TestEventReceiver1/TestEventReceiver1.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/CustomField1_VB/EventReceiver1/EventReceiver1.vb" id="Snippet1":::

     代码将运行，并且 SharePoint 站点将显示在 Web 浏览器中。

10. 在快速启动栏上，选择“患者”链接，然后选择“添加新项”链接。

     此时将打开新项的条目窗体。

11. 在字段中输入数据，然后选择“保存”按钮。

     选择“保存”按钮后，“患者姓名”列将自动更新为名称 Scott Brown。

## <a name="see-also"></a>另请参阅

- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)