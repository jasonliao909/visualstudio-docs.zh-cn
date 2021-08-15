---
title: 如何：定义方法实例 |Microsoft Docs
description: 了解如何在业务数据连接 (BDC) 模型中定义方法的方法实例。
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
ms.openlocfilehash: c75c41a68c4c6ba2cebf0b7d16bbf5b5ff064aee8f25d4c2962c9574b5c78ef1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121409613"
---
# <a name="how-to-define-a-method-instance"></a>如何：定义方法实例
  必须为模型中的每个方法定义至少一个方法实例。

 使用 " **BDC 方法详细信息** " 窗口添加方法实例。 添加方法实例时，Visual Studio 会将一个 `<MethodInstance>` 元素添加到项目中的模型文件的 XML 中。 有关元素特性的详细信息 `<MethodInstance>` ，请参阅 [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14))。

### <a name="to-define-a-method-instance"></a>定义方法实例

1. 在 " **BDC 方法详细信息** " 窗口中，展开方法的节点，然后展开 " **实例** " 节点。

2. 在 " **添加方法实例** " 列表中，选择 " **创建 Finder 实例**"。

     " **实例** " 节点下将出现一个新的方法实例。

3. 在菜单栏上，选择 "**查看**  >  **属性窗口**"。

4. 在 " **属性** " 窗口中，设置方法实例的属性。 有关每个属性的详细信息，请参阅 [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14))。

## <a name="see-also"></a>另请参阅
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：向模型添加实体](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [如何：向方法添加参数](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
