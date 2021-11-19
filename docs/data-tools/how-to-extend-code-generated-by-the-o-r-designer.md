---
title: 如何：扩展由 O-R 设计器生成的代码
description: 查看如何扩展对象关系设计器（O/R 设计器）生成的代码。 向实体类中添加代码。 向 DataContext 中添加代码。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d6d1122e-2f55-4607-8d8b-48c3c22600fb
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 7bc1c926108efb6223788caa695bdb4028645252
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601132"
---
# <a name="how-to-extend-code-generated-by-the-or-designer"></a>如何：扩展由 O/R 设计器生成的代码
在更改设计器图面上的实体类和其他对象时，将重新生成由 O/R 设计器生成的代码。 当设计器重新生成代码时，你添加到生成的代码中的任何代码一般都会被重新声称的代码覆盖。 O/R 设计器提供了一种生成分部类文件的功能，你可以将代码添加到分部类文件中而不会被覆盖。 将你自己的代码添加到 O/R 设计器生成的代码中的一个示例是在 LINQ to SQL（实体）类中添加数据验证。 有关详细信息，请参阅[如何将验证添加到实体类](../data-tools/how-to-add-validation-to-entity-classes.md)。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-code-to-an-entity-class"></a>向实体类中添加代码

### <a name="to-create-a-partial-class-and-add-code-to-an-entity-class"></a>创建分部类并向实体类中添加代码

1. 在 O/R 设计器中打开或创建一个新的 LINQ to SQL 类文件（.dbml 文件） 。 （在“解决方案资源管理器”或“数据库资源管理器”中双击 .dbml 文件。  ）

2. 在 O/R 设计器中，右键单击要为其添加验证的类，然后单击“查看代码”。

     将打开代码编辑器，其中显示所选实体类的分部类。

3. 在该实体类的分部类声明中添加您的代码。

## <a name="add-code-to-a-datacontext"></a>向 DataContext 中添加代码

### <a name="to-create-a-partial-class-and-add-code-to-a-datacontext"></a>创建分部类并向 DataContext 中添加代码

1. 在 O/R 设计器中打开或创建一个新的 LINQ to SQL 类文件（.dbml 文件） 。 （在“解决方案资源管理器”或“数据库资源管理器”中双击 .dbml 文件。  ）

2. 在 O/R 设计器中右击设计器中的空白区域，然后单击“查看代码” 。

     将打开代码编辑器，其中显示 DataContext 的分部类。

3. 在 DataContext 的分部类声明中添加您的代码。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [演练：创建 LINQ to SQL 类（O-R 设计器）](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
