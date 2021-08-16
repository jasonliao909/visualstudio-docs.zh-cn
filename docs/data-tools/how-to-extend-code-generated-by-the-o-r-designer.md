---
title: 如何：扩展由 O-R 设计器生成的代码
description: 查看如何扩展由 O/R 设计器对象关系设计器 (生成的) 。 将代码添加到实体类。 将代码添加到 DataContext。
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
ms.openlocfilehash: dac89dae2f54c32e6fb4e2bd40d3ee231e4847e3914bd0e577e489beb214e5f0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121264345"
---
# <a name="how-to-extend-code-generated-by-the-or-designer"></a>如何：扩展由 O/R 设计器生成的代码
对设计器图面上的实体类和其他对象进行更改时，将重新生成 **O/R** 设计器生成的代码。 当设计器重新生成代码时，你添加到生成的代码中的任何代码一般都会被重新声称的代码覆盖。 **O/R 设计器** 提供生成分部类文件的能力，可在其中添加未覆盖的代码。 向 **O/R** 设计器生成的代码添加自己的代码的一个示例是将数据验证添加到 LINQ to SQL (实体) 类。 有关详细信息，请参阅 [如何：向实体类 添加验证](../data-tools/how-to-add-validation-to-entity-classes.md)。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-code-to-an-entity-class"></a>向实体类添加代码

### <a name="to-create-a-partial-class-and-add-code-to-an-entity-class"></a>创建分部类并向实体类中添加代码

1. 在 **O/R** 设计器中LINQ to SQL **.dbml** (中打开) 或创建新的类文件。  (双击 .解决方案资源管理器 或 .数据库资源管理器 **中的****.dbml** ) 

2. 在 O/R 设计器中，右键单击要为其添加验证的类，然后单击“查看代码”。

     将打开代码编辑器，其中显示所选实体类的分部类。

3. 在该实体类的分部类声明中添加您的代码。

## <a name="add-code-to-a-datacontext"></a>向 DataContext 添加代码

### <a name="to-create-a-partial-class-and-add-code-to-a-datacontext"></a>创建分部类并向 DataContext 中添加代码

1. 在 **O/R** 设计器中LINQ to SQL **.dbml** (中打开) 或创建新的类文件。  (双击 .解决方案资源管理器 或 .数据库资源管理器 **中的****.dbml** ) 

2. 在 **O/R 设计器中**，右键单击设计器上的空白区域，然后单击"查看 **代码"。**

     将打开代码编辑器，其中显示 DataContext 的分部类。

3. 在 DataContext 的分部类声明中添加您的代码。

## <a name="see-also"></a>另请参阅

- [LINQ to SQL工具Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [演练：创建 LINQ to SQL 类（O-R 设计器）](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
