---
title: LINQ to SQL 类之间的关系
description: 使用对象关系设计器（O/R 设计器）中的关联编辑器对话框创建 LINQ to SQL 实体类之间的关联。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 56133e65-81f3-44c3-bc28-ffdd0671a0d2
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: e7f686e86f0bb4743e8cbb45e29d0ebcb2b22e5e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601136"
---
# <a name="how-to-create-an-association-between-linq-to-sql-classes-or-designer"></a>如何：在 LINQ to SQL 类之间创建关联（O/R 设计器）
[!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] 中实体类之间的关联类似于数据库中表之间的关系。 可以使用“关联编辑器”对话框创建实体类之间的关联。

使用“关联编辑器”对话框创建关联时，必须选择父类和子类。 父类是包含主键的实体类；子类是包含外键的实体类。 例如，如果创建映射到 `Northwind Customers` 和 `Orders` 表的实体类，则 `Customer` 类将是父类，而 `Order` 类将是子类。

> [!NOTE]
> 将表从服务器资源管理器或数据库资源管理器拖动到对象关系设计器（O/R 设计器）时，，会基于数据库中的现有外键关系自动创建关联。

## <a name="association-properties"></a>关联属性
创建关联后，在 O/R 设计器中选择该关联时，“属性”窗口中将有一些可配置属性。 （关联是相关类之间的线。）下表提供了关联属性的说明。

|属性|说明|
|--------------|-----------------|
|**基数**|控制关联是一对多关系还是一对一关系。|
|**子属性**|指定是否在父类上创建一个属性，作为关联关系外键一方上的子记录的集合或对这些子记录的引用。 例如，在 `Customer` 和 `Order` 之间的关联中，如果“子属性”设置为“True”，则将在父类上创建一个名为 `Orders` 的属性 。|
|**Parent 属性**|子类上引用关联父类的属性。 例如，在 `Customer` 和 `Order` 之间的关联中，在 `Order` 类上创建一个名为 `Customer` 的属性，用来引用与订单关联的客户。|
|**参与的属性**|显示关联属性，并提供一个省略号按钮 (...)，该按钮可重新打开“关联编辑器”对话框。|
|**唯一**|指定外目标列是否具有唯一性约束。|

## <a name="to-create-an-association-between-entity-classes"></a>创建实体类之间的关联

1. 右击表示关联中的父类的实体类，指向“添加”，然后单击“关联”。

2. 验证在“关联编辑器”对话框中是否选择了正确的“父类”。

3. 选择组合框中的“子类”。

4. 选择实现类之间的关联的“关联属性”。 通常，这种关联对应于数据库中定义的外键关系。 例如，在 `Customers` 和 `Orders` 关联中，“关联属性”是每个类的 `CustomerID`。

5. 单击“确定”创建关联。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [演练：创建 LINQ to SQL 类](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [DataContext 方法（O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)
- [如何：表示主键](/dotnet/framework/data/adonet/sql/linq/how-to-represent-primary-keys)
