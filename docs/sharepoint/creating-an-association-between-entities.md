---
title: 创建实体之间的关联|Microsoft Docs
description: 在业务数据连接和 BDC (模型中) 关联。 了解关联方法和关联类型。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.BDC.Association_Dialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associations between entities
- BDC [SharePoint development in Visual Studio], associations between entities
- Business Data Connectivity service [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associate external content types
- Business Data Connectivity service [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], associate external content types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: dcae4af6cb6ef0592f587718afe995a364686351
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600672"
---
# <a name="create-an-association-between-entities"></a>创建实体之间的关联
  可以通过创建关联，在 BDC (BDC) 中定义实体之间的关系。 Visual Studio生成方法，这些方法向模型的使用者提供有关每个关联的信息。 SharePoint Web 部件、列表或自定义应用程序可以使用这些方法在用户界面 (UI) 中显示数据关系。

## <a name="create-an-association"></a>创建关联
 通过选择"Visual Studio 工具箱 **"中的"** 关联"控件创建关联，选择 (名为源实体) 的第一个实体，然后选择第二个实体 (称为目标实体) 。 可以在关联编辑器 中定义 **关联的详细信息**。 有关详细信息，请参阅 [如何：创建实体之间的关联](../sharepoint/how-to-create-an-association-between-entities.md)。

## <a name="association-methods"></a>关联方法
 业务数据SharePoint等应用程序通过调用实体的服务类中的方法来使用关联。 通过在关联编辑器 中选择方法，可以将方法添加到实体 **的服务类**。

 默认情况下，关联 **编辑器** 将关联导航方法添加到源和目标实体。 源实体中的关联导航方法使使用者能够检索目标实体的列表。 目标实体中的关联导航方法使使用者能够检索与目标实体相关的源实体。

 必须将代码添加到其中每个方法，以返回相应的信息。 还可以添加其他类型的方法以支持更高级的方案。 有关这些方法中每个方法的信息，请参阅 [支持的操作](/previous-versions/office/developer/sharepoint-2010/ee557363(v=office.14))。

## <a name="types-of-associations"></a>关联类型
 可以在 BDC 设计器中创建两种类型的关联：基于外键的关联和外键无键关联。

### <a name="foreign-key-based-association"></a>基于外键的关联
 可以通过将源实体中的标识符与目标实体中定义的类型描述符关联来创建基于外键的关联。 此关系使模型的使用者能够为用户提供增强的 UI。 例如，Outlook窗体，使用户能够创建可在下拉列表中显示客户的销售订单;或中销售订单SharePoint，使用户能够为客户打开个人资料页。

 若要创建基于外键的关联，请关联共享相同名称和类型的标识符和类型描述符。 例如，您可以在实体和实体之间创建基于外键 `Contact` 的 `SalesOrder` 关联。 `SalesOrder`实体将类型描述符作为 Finder 或特定 Finder 方法的返回参数的 `ContactID` 一部分返回。 这两个类型描述符都显示在关联 **编辑器 中**。 若要在实体和实体之间创建基于外键的关系 `Contact` `SalesOrder` ，请选择 `ContactID` 每个字段旁边的标识符。

 将代码添加到返回目标实体集合的源实体的 Association Navigator 方法。 以下示例返回联系人的销售订单。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet7":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet7":::

 将代码添加到返回源实体的目标实体的 Association Navigator 方法。 以下示例返回与销售订单相关的联系人。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderservice.cs" id="Snippet8":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderservice.vb" id="Snippet8":::

### <a name="foreign-keyless-association"></a>外键无键关联
 可以创建关联，而无需将标识符映射到字段类型描述符。 当源实体与目标实体没有直接关系时，创建此类关联。 例如， `SalesOrderDetail` 表没有映射到表中的主键的外 `Contact` 键。

 如果要在表中显示与 相关的信息，可以在实体和实体之间创建外键 `SalesOrderDetail` `Contact` `Contact` 无键 `SalesOrderDetail` 关联。

 在实体的关联导航方法中，通过联接表或调用存储过程返回 `Contact` `SalesOrderDetail` 实体。

 下面的示例通过联接表返回所有销售订单的详细信息。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet9":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet9":::

 在实体的关联导航 `SalesOrderDetail` 方法中，返回相关的 `Contact` 。 下面的示例演示这一操作。
                                                                            
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderdetailservice.cs" id="Snippet10":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderdetailservice.vb" id="Snippet10":::

## <a name="see-also"></a>另请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：创建实体之间的关联](../sharepoint/how-to-create-an-association-between-entities.md)
