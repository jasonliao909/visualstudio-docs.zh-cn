---
title: 如何：定义方法实例 | Microsoft Docs
description: 了解如何在业务数据连接 (BDC) 模型中为方法定义方法实例。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], method instance
- BDC [SharePoint development in Visual Studio], method instance
- BDC [SharePoint development in Visual Studio], method
- Business Data Connectivity service [SharePoint development in Visual Studio], method
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 1b01a254283befcd790b0e2ecbb0a35084c5b944
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663838"
---
# <a name="how-to-define-a-method-instance"></a>如何：定义方法实例
  必须为模型中的每个方法至少定义一个方法实例。

 使用“BDC 方法详细信息”窗口添加方法实例。 当你添加方法实例时，Visual Studio 会将 `<MethodInstance>` 元素添加到你的项目中模型文件的 XML。 有关 `<MethodInstance>` 元素特性的详细信息，请参阅 [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14))。

### <a name="to-define-a-method-instance"></a>定义方法实例

1. 在“BDC 方法详细信息”窗口中，展开方法的节点，然后展开“实例”节点。

2. 在“添加方法实例”列表中，选择“创建 Finder 实例”。

     新的方法实例将显示在“实例”节点下。

3. 在菜单栏上，选择“视图” > “属性窗口”。

4. 在“属性”窗口中，设置方法实例的属性。 有关每个属性的详细信息，请参阅 [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14))。

## <a name="see-also"></a>另请参阅
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：将实体添加到模型](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
