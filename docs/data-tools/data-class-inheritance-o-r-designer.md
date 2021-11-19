---
title: 数据类继承（O-R 设计器）
description: 在对象关系设计器（O/R 设计器，Visual Studio 中的一种 LINQ to SQL 类工具）中使用数据类继承。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: af32653c-f4e6-4217-8c5a-e32b322b4918
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 82c1c07ec9fb7e19a2d4e126358d124d88c79ff1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601174"
---
# <a name="data-class-inheritance-or-designer"></a>数据类继承（O/R 设计器）

像其他对象一样，LINQ to SQL 类可以使用继承，并可从其他类派生。 在代码中，可以通过声明一个类继承自另一个类来指定对象间的继承关系。 在数据库中，可通过多种方式创建继承关系。 对象关系设计器（O/R 设计器）支持通常在关系系统中实现的单表继承概念 。

在单表继承中，一个数据库表同时包含基类和派生类的列。 使用关系数据时，一个鉴别器列包含的值确定任意给定的记录属于哪个类。 例如，假设有一个 `Persons` 表包含公司的所有员工。 一些人是员工，一些人是经理。 `Persons` 表包含一个名为 `Type` 的列，该列用值 1 表示经理，用值 2 表示员工。 `Type` 列是鉴别器列。 在此应用场景中，可以创建一个员工子类，并仅使用 `Type` 值为 2 的记录来填充该类。

使用 [!INCLUDE[vs_ordesigner_short](../data-tools/includes/vs_ordesigner_short_md.md)] 配置实体类中的继承时，将包含继承数据的单表两次拖动到设计器上：一次拖动对应继承层次结构中的一个类。 将表添加到设计器后，从“对象关系设计器”工具箱中用“继承”项连接这些表，然后在“属性”窗口中设置四个继承属性。

## <a name="inheritance-properties"></a>继承属性

下表列出了这些继承属性及其说明：

|属性|说明|
|--------------|-----------------|
|**鉴别器属性**|决定当前记录所属的类的属性，该属性映射到列。|
|**基类鉴别器值**|决定记录所属的基类的值，该值位于指定为鉴别器属性的列中。|
|**派生类鉴别器值**|决定记录所属的派生类的值，该值位于指定为鉴别器属性的属性中。|
|**继承默认值**|当指定为“鉴别器属性”的属性的值与“基类鉴别器值”或“派生类鉴别器值”不匹配时填充的类  。|

创建一个使用继承并对应于关系数据的对象模型可能有些不易理解。 本主题提供了有关配置继承时所需的基本概念及各个属性的信息。 下列主题对如何使用 O/R 设计器配置继承进行了更清楚的阐释。

|主题|说明|
|-----------|-----------------|
|[如何：通过 O/R 设计器配置继承](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)|描述如何使用 O/R 设计器配置使用单表继承的实体类。|
|[演练：使用单表继承创建 LINQ to SQL 类（O/R 设计器）](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)|提供有关如何使用 O/R 设计器配置使用单表继承的实体类的分步说明。|

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [演练：创建 LINQ to SQL 类（O-R 设计器）](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [演练：使用单表继承创建 LINQ to SQL 类（O/R 设计器）](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)
- [入门](/dotnet/framework/data/adonet/sql/linq/getting-started)
