---
title: 创建实体之间的关联 | Microsoft Docs
description: 在业务数据连接 (BDC) 模型中创建实体之间的关联。 了解关联方法和关联类型。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600672"
---
# <a name="create-an-association-between-entities"></a>创建实体之间的关联
  你可以通过创建关联来定义业务数据连接 (BDC) 模型中实体之间的关系。 Visual Studio 生成了一些方法，这些方法为模型的使用者提供有关每个关联的信息。 SharePoint Web 部件、列表或自定义应用程序可以使用这些方法在用户界面 (UI) 中显示数据关系。

## <a name="create-an-association"></a>创建关联
 要创建关联，请选择 Visual Studio“工具箱”中的“关联”控件，选择第一个实体（称为源实体），然后选择第二个实体（称为目标实体）。  可以在“关联编辑器”中定义关联的详细信息。 有关详细信息，请参阅[如何：创建实体之间的关联](../sharepoint/how-to-create-an-association-between-entities.md)。

## <a name="association-methods"></a>关联方法
 诸如 SharePoint 业务数据 Web 部件等应用程序通过调用实体的服务类中的方法来使用关联。 通过在“关联编辑器”中选择方法，可以将方法添加到实体的服务类。

 默认情况下，“关联编辑器”会将关联导航方法添加到源实体和目标实体。 源实体中的关联导航方法使使用者能够检索目标实体的列表。 目标实体中的关联导航方法使使用者能够检索与目标实体相关的源实体的列表。

 必须将代码添加到其中每个方法，以返回相应的信息。 还可以添加其他类型的方法以支持更高级的方案。 有关这些方法的详细信息，请参阅[支持的操作](/previous-versions/office/developer/sharepoint-2010/ee557363(v=office.14))。

## <a name="types-of-associations"></a>关联类型
 可以在 BDC 设计器中创建两种类型的关联：基于外键的关联和无外键关联。

### <a name="foreign-key-based-association"></a>基于外键的关联
 可以通过将源实体中的标识符与目标实体中定义的类型描述符进行关联，来创建基于外键的关联。 此关系使模型的使用者能够为用户提供增强的 UI。 例如，Outlook 中的一个窗体，使用户能够创建一个可在下拉列表中显示客户的销售订单；或者 SharePoint 中的一个销售订单列表，使用户能够为客户打开个人资料页。

 为了创建基于外键的关联，需要将共享相同名称和类型的标识符和类型描述符关联起来。 例如，可以在 `Contact` 实体和 `SalesOrder` 实体之间创建一个基于外键的关联。 `SalesOrder` 实体将 `ContactID` 类型描述符作为 Finder 或特定 Finder 方法的返回参数的一部分返回。 这两个类型描述符都显示在“关联编辑器”中。 若要在 `Contact` 实体和 `SalesOrder` 实体之间创建一个基于外键的关系，请选择这些字段旁边的 `ContactID` 标识符。

 在源实体的关联导航器方法中，添加可返回目标实体集合的代码。 以下示例返回联系人的销售订单。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet7":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet7":::

 在目标实体的关联导航器方法中，添加可返回源实体的代码。 以下示例返回与销售订单相关的联系人。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderservice.cs" id="Snippet8":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderservice.vb" id="Snippet8":::

### <a name="foreign-keyless-association"></a>无外键关联
 可以创建一个关联，而不将标识符映射到字段类型描述符上。 当源实体与目标实体没有直接关系时，创建这种关联。 例如，`SalesOrderDetail` 表没有映射到 `Contact` 表中主键的外键。

 如果要在与 `Contact` 相关的 `SalesOrderDetail` 表中显示信息，可以在 `Contact` 实体与 `SalesOrderDetail` 实体之间创建一个无外键关联。

 在 `Contact` 实体的关联导航方法中，通过联接表或通过调用存储过程来返回 `SalesOrderDetail` 实体。

 下面的示例通过联接表返回所有销售订单的详细信息。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet9":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet9":::

 在 `SalesOrderDetail` 实体的关联导航方法中，返回相关的 `Contact`。 下面的示例演示这一操作。
                                                                            
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderdetailservice.cs" id="Snippet10":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderdetailservice.vb" id="Snippet10":::

## <a name="see-also"></a>另请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：创建实体之间的关联](../sharepoint/how-to-create-an-association-between-entities.md)
