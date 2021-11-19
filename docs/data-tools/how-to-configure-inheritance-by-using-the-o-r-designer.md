---
title: 使用 O-R 设计器配置继承
description: 了解如何使用支持单表继承的对象关系设计器（O/R 设计器）配置继承。 已创建的继承的数据类。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: e594af12-e777-434a-bc08-7dd2dac84cdc
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: bfec5df4ed32178616f1086b2cd52216cb25c9c0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601144"
---
# <a name="how-to-configure-inheritance-by-using-the-or-designer"></a>如何：通过 O/R 设计器配置继承
对象关系设计器（O/R 设计器）支持通常在关系系统中实现的单表继承概念 。 在单表继承中，一个数据库表同时包含父信息和子信息的字段。 使用关系数据时，一个鉴别器列包含的值确定任意记录属于哪个类。

例如，假设有一个 `Persons` 表包含公司的所有员工。 一些人是员工，一些人是经理。 `Persons` 表包含一个名为 `EmployeeType` 的列，其中值 1 表示经理，值 2 表示员工；这个列就是鉴别器列。 在此应用场景中，可以创建一个员工子类，并仅使用 `EmployeeType` 值为 2 的记录来填充该类。 还可以从每个类中移除不适用的列。

创建一个使用继承（并对应于关系数据）的对象模型可能有些不易理解。 下面的过程概括说明使用 O/R 设计器配置继承所需的步骤。 如果不参考现有的表和列，将很难执行这些一般性的步骤，因此我们提供了一个使用数据的演练。 若要了解关于如何使用 O/R 设计器配置继承的详细分步指导，请参阅[演练：使用单表继承创建 LINQ to SQL 类（O/R 设计器）](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)。

## <a name="to-create-inherited-data-classes"></a>创建继承的数据类

1. 通过将“LINQ to SQL 类”项添加到现有 Visual Basic 或 C# 项目中来打开 O/R 设计器 。

2. 将要用作基类的表拖到 O/R 设计器上。

3. 将该表的第二个副本拖到 O/R 设计器上并重命名该副本。 这是派生类，即子类。

4. 在“工具箱”的“对象关系设计器”选项卡中单击“继承”，然后单击子类（重命名的表）并将其连接到基类。

    > [!NOTE]
    > 单击“工具箱”中的“继承”项，释放鼠标按钮，单击在步骤 3 中创建的该类的第二个副本，然后单击在步骤 2 中创建的第一个类。 继承连线中的箭头将指向第一个类。

5. 在每个类中，删除任何不希望显示和没有用于关联的对象属性。 如果试图删除用于关联的对象属性，则会收到一个错误：[无法删除属性 \<property name>，因为它正在参与关联 \<association name>](../data-tools/the-property-property-name-cannot-be-deleted-because-it-is-participating-in-the-association-association-name.md)。

    > [!NOTE]
    > 由于派生类继承其基类中定义的属性，在每个类中不能定义相同的列。 （列实现为属性。）通过设置基类属性中的继承修饰符，可以在派生类中创建列。 有关详细信息，请参阅[继承基础知识 (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)。

6. 在 O/R 设计器中选择继承连线。

7. 在“属性”窗口中，将“鉴别器属性”设置为用于区分类中记录的列名称 。

8. 将“派生类鉴别器值”属性设置为数据库中将记录指定为继承类型的值。 （这是存储在鉴别器列中的值，用于指定继承的类。）

9. 将“基类鉴别器值”属性设置为将记录指定为基类型的值。 （这是存储在鉴别器列中的值，用于指定基类。）

10. （可选）还可以设置“继承默认值”属性，以便在继承层次结构中指定类型，当加载与任何定义的继承代码都不匹配的行时将使用该类型。 换句话说，如果记录在其鉴别器列中的值与“派生类鉴别器值”或“基类鉴别器值”属性中的值都不匹配，则该记录将加载到指定为“继承默认值”的类型中  。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [演练：创建 LINQ to SQL 类（O-R 设计器）](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [演练：使用单表继承创建 LINQ to SQL 类（O/R 设计器）](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)
- [继承的基础知识 (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)
- [继承](/dotnet/csharp/programming-guide/classes-and-structs/inheritance)
