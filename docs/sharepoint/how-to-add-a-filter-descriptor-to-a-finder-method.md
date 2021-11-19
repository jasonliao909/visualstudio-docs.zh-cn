---
title: 如何：将筛选器描述符添加到 Finder 方法 | Microsoft Docs
description: 了解如何使用 Visual Studio 中的“BDC 方法详细信息”窗口向 Finder 方法添加筛选器描述符。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], filter descriptors
- Business Data Connectivity service [SharePoint development in Visual Studio], add a filter
- BDC [SharePoint development in Visual Studio], add a filter
- BDC [SharePoint development in Visual Studio], filter descriptors
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 62d05e77d808744da1fbb8d639e762f55103b7d4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600638"
---
# <a name="how-to-add-a-filter-descriptor-to-a-finder-method"></a>如何：将筛选器描述符添加到 Finder 方法
  筛选器描述符允许模型的使用者在执行之前将值传递给方法。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

 一种常见的情况是，SharePoint 中的用户想要检索符合某些条件的外部内容类型的实例。 可以通过向 Finder 方法添加筛选器描述符来支持此方案。

### <a name="to-add-a-filter-descriptor-to-a-finder-method"></a>将筛选器描述符添加到 Finder 方法

1. 在“BDC 方法详细信息”窗口中，依次展开 Finder 方法的节点和“参数”节点，然后添加输入参数。 有关详细信息，请参阅[如何：向方法中添加参数](../sharepoint/how-to-add-a-parameter-to-a-method.md)。

2. 在“方法详细信息”窗口中，选择该参数的类型描述符。

3. 在菜单栏上，选择“视图” > “属性窗口”。

4. 在“属性”窗口中，将“类型名称”属性设置为适合筛选器的数据类型。

     例如，筛选器可以使用订单日期来限制该方法返回的销售订单数。 若要支持该筛选器，必须将类型描述符的“类型名称”属性设置为 System.DateTime。

5. 在“方法详细信息”窗口中，扩展“筛选器描述符”节点 。

6. 在“添加筛选器描述符”列表中，选择“创建筛选器描述符”。

     “筛选器描述符”节点下将显示一个新的筛选器描述符。

7. 在菜单栏上，选择“视图” > “属性窗口”。

8. 在“属性”窗口中，选择“类型”属性。

9. 在显示了“类型”属性的列表中，选择所需的筛选模式。

     例如，若要创建一个使用订单日期来限制在 Finder 方法中返回的销售订单数的筛选器，请选择“比较”。 比较筛选器可确保 Finder 方法仅返回满足特定条件的实例。 有关每种筛选模式的详细信息，请参阅 [BDC 支持的筛选器的类型](/previous-versions/office/developer/sharepoint-2010/ee556392(v=office.14))。

10. 在“属性”窗口中，选择“关联的类型描述符”属性。

11. 在为“关联的类型描述符”属性显示的列表中，选择之前在此过程中创建的类型描述符。 这会将筛选器与 Finder 方法的输入参数相关联。

12. 向返回数据的 Finder 方法添加代码。 可以使用输入参数作为选择查询中的条件。

     下面的示例返回了具有指定订单日期的销售订单。

    > [!NOTE]
    > 将 `ServerName` 字段的值替换为你的服务器名称。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderservice.cs" id="Snippet11":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderservice.vb" id="Snippet11":::

## <a name="see-also"></a>另请参阅
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [将业务数据集成到 SharePoint 中](../sharepoint/integrating-business-data-into-sharepoint.md)
