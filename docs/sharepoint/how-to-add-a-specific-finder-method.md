---
title: 如何：添加特定的 Finder 方法 | Microsoft Docs
description: 通过添加 Finder 方法获取实体实例。 当用户在业务数据 Web 部件或外部列表中选取实体时，BDC 服务将调用此方法。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], Specific Finder
- BDC [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], get an entity
- Business Data Connectivity service [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], Specific Finder
- Business Data Connectivity service [SharePoint development in Visual Studio], get an entity
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: be79b205e8b31cf25e6d287784a7f5b144943282
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665022"
---
# <a name="how-to-add-a-specific-finder-method"></a>如何：添加特定的 Finder 方法
  可以创建特定的 Finder 方法来返回单个实体实例。 当用户选择业务数据 Web 部件或外部列表中的实体时，Business Data Connectivity (BDC) service 将执行特定的 Finder 方法。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-a-specific-finder-method"></a>创建特定的 Finder 方法

1. 在 BDC 设计器上，选择一个实体。

    若要了解如何在 Visual Studio 中向“BDC 设计器”添加实体，请参阅[如何：向模型添加实体](../sharepoint/how-to-add-an-entity-to-a-model.md)。

2. 在菜单栏上，依次选择“视图” > “其他窗口”、“BDC 方法详细信息”  。

    “BDC 方法详细信息”窗口将打开。 有关该窗口的详细信息，请参阅 [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在“添加方法”列表中，选择“创建特定的 Finder 方法” 。

    Visual Studio 将以下元素添加到模型中。 这些元素显示在“BDC 方法详细信息”窗口中。

   - 方法。

   - 方法的输入参数。

   - 方法的返回参数。

   - 每个参数的类型描述符。

   - 方法的方法实例。

     有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

4. 打开 Visual Studio 的“属性”窗口。

5. 将返回参数的类型描述符配置为实体类型描述符。 若要了解如何创建实体类型描述符，请参阅[如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

   > [!NOTE]
   > 如果向实体添加了 Finder 方法，则无需执行此步骤。 Visual Studio 将使用在 Finder 方法中定义的类型描述符。

   > [!NOTE]
   > 如果实体类型的标识符字段表示数据库表中自动生成的字段，请将标识符字段的只读属性设置为 True 。

6. 在“方法详细信息”窗口中，选择该方法的方法实例。

7. 在“属性”窗口中，将“返回参数名称”属性设置为该方法的返回参数的名称 。 有关方法实例属性的详细信息，请参阅 [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14))。

8. 在解决方案资源管理器中，打开为实体生成的服务代码文件的快捷菜单，然后选择“查看代码” 。

    实体服务代码文件将在代码编辑器中打开。 有关该实体服务代码文件的详细信息，请参阅[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

9. 向特定的 Finder 方法添加代码。 此代码执行以下任务：

   - 从数据源检索记录。

   - 将实体返回到 BDC 服务。

     以下示例返回 SQL Server AdventureWorks 示例数据库中的联系人。

     > [!NOTE]
     > 将 `ServerName` 字段的值替换为你的服务器名称。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet3":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet3":::

## <a name="see-also"></a>另请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
