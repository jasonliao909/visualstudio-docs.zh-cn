---
title: 如何：将参数添加到方法|Microsoft Docs
description: 了解如何使用 BDC (方法将参数) 业务数据连接，从而将信息传递到方法中或从方法返回信息。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], adding a method to a parameter
- Business Data Connectivity service [SharePoint development in Visual Studio], parameter
- BDC [SharePoint development in Visual Studio], adding a method to a parameter
- BDC [SharePoint development in Visual Studio], parameter
- Business Data Connectivity service [SharePoint development in Visual Studio], method parameters
- BDC [SharePoint development in Visual Studio], method parameters
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 5868dfe761030ed46d71b45cbe646959f8824ece
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600636"
---
# <a name="how-to-add-a-parameter-to-a-method"></a>如何：向方法添加参数
  使用 参数将信息传递到 方法中，或者从 方法返回信息。 所有方法都必须至少具有一个参数。 若要详细了解如何设计参数以支持要创建的方法类型，请参阅 [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

 向方法添加参数时，Visual Studio将 Parameter 元素添加到项目中模型文件的 XML。 有关 Parameter 元素的属性详细信息，请参阅 [Parameter](/previous-versions/office/developer/sharepoint-2010/ee557705(v=office.14))。

### <a name="to-add-a-parameter-to-a-method"></a>向方法添加参数

1. 向实体添加方法。

2. 在菜单栏上，选择"**查看其他** Windows  >    >  **BDC 方法详细信息"。**

     **"BDC 方法详细信息"窗口** 随即打开。 有关详细信息，请参阅 [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在 **"BDC 方法详细信息"** 窗口中，展开方法的节点，然后展开 **"参数"** 节点。

4. 在"**添加参数"列表中**，选择"**创建参数"。**

     新参数显示在"参数 **"节点** 下。

5. 在菜单栏上，选择"查看  >  **属性窗口"。**

6. 在" **属性** "窗口中，将 **Name** 属性设置为任何有意义的名称。 例如，如果方法将返回客户，你可以将方法命名 **GetCustomers**。

7. 在 **"BDC 方法详细信息**"窗口中，打开针对参数方向显示的列表，然后选择"In、InOut、Out"或"**返回"。**

     有关为要创建的类型方法选择哪个方向的信息，请参阅 [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

8. 修改参数的类型描述符。 有关详细信息，请参阅 [如何：定义](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)参数 的类型描述符。

## <a name="see-also"></a>另请参阅
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：向模型添加实体](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
