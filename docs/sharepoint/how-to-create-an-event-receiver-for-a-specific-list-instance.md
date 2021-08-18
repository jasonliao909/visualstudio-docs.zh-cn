---
title: 如何：为特定列表实例实例创建事件接收器|Microsoft Docs
titleSuffix: ''
description: 为特定列表实例创建事件接收器。 列表实例事件接收器响应列表定义的任何实例中发生的事件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
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
ms.openlocfilehash: cfc18bab08a141e5c7173d622e0bc55d1a2f0fbc
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122130996"
---
# <a name="how-to-create-an-event-receiver-for-a-specific-list-instance"></a>如何：为特定列表实例创建事件接收器
  列表实例事件接收器响应列表定义的任何实例中发生的事件。 尽管事件接收器模板不启用特定列表实例的目标，但你可以修改范围为列表定义的事件接收器，以响应特定列表实例中的事件。

 若要以特定列表实例为目标，Elements.xml接收器的 URL 中，将 替换为 并添加 `ListTemplateId` 列表实例的 `ListUrl` URL。

## <a name="create-a-list-instance-event-receiver"></a>创建列表实例事件接收器
 以下步骤显示如何修改列表项事件接收器，以仅响应自定义 announcements-list 实例中发生的事件。

#### <a name="to-modify-an-event-receiver-to-respond-to-a-specific-list-instance"></a>修改事件接收器以响应特定列表实例

1. 在浏览器中打开 SharePoint 网站。

2. 在导航窗格中，" **列表"** 链接。

3. 在" **所有站点内容"** 页中，选择" **创建"** 链接。

4. 在"**创建**"对话框中，选择"公告类型"，将公告命名 **TestAnnouncements**，然后选择"创建 **"** 按钮。

5. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，创建事件接收器项目。

6. 在"**你想要哪种类型的事件接收者？"列表中**，选择"**列出项事件"。**

    > [!NOTE]
    > 还可以选择范围为列表定义的任何类型的事件接收器，例如"**列出电子邮件** 事件"或"**列出工作流事件"。**

7. 在"**什么项应为事件源？"列表中**，选择"**公告"。**

8. 在 **"处理以下事件"列表中**，选中"正在添加项"复选框，然后选择"完成 **"** 按钮。

9. 在 **解决方案资源管理器** 中，在 EventReceiver1 下打开 *Elements.xml。*

     事件接收器当前使用以下行来引用公告列表定义：

    ```xml
    <Receivers ListTemplateId="104">
    ```

     将此行更改为以下文本：

    ```xml
    <Receivers ListUrl="Lists/TestAnnouncements">
    ```

     这会指示事件接收器仅响应刚刚创建的新 **TestAnnouncements** 公告列表中发生的事件。 可以更改 属性 `ListURL` 以引用该服务器上任何SharePoint实例。

10. 打开事件接收器的代码文件，在 ItemAdding 方法中放入断点。

11. 选择 **F5** 键以生成并运行解决方案。

12. 在SharePoint中，选择导航窗格中的 **"TestAnnouncements"** 链接。

13. 选择" **添加新公告"** 链接。

14. 输入公告的标题，然后选择"保存 **"** 按钮。

     请注意，将新项添加到自定义公告列表时，将命中断点。

15. 选择要 **恢复的 F5** 键。

16. 在导航窗格中，选择" **列表"** 链接，然后选择" **公告"** 链接。

17. 添加新公告。

     请注意，事件接收器不会触发新公告，因为接收方配置为仅响应自定义公告列表实例 **TestAnnouncements 中的事件**。

## <a name="see-also"></a>请参阅
- [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
