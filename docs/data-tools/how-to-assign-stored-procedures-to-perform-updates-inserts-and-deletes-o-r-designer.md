---
title: 在 LINQ to SQL 中使用存储过程来更新数据
description: 使用 LINQ to SQL 对象关系设计器 (O/R 设计器) 中的存储过程来执行数据的更新、插入和删除。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: e88224ab-ff61-4a3a-b6b8-6f3694546cac
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 51cdb3f5af6f77d67cdcd9342e39aca6a5dcf24730cb9565ce5b0404b24e1543
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121347163"
---
# <a name="how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-or-designer"></a>如何：分配存储流程来执行更新、插入和删除操作（O/R 设计器）

存储过程可添加到 **O/R 设计器** 并作为典型方法执行 <xref:System.Data.Linq.DataContext> 。 在将更改从实体类保存到数据库时，它们还可以用于替代默认 LINQ to SQL 运行时行为，该行为执行插入、更新和删除操作 (例如，在调用 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 方法) 时。

> [!NOTE]
> 如果存储过程的返回值需要发送回客户端（例如在存储过程中计算出的值），则在存储过程中创建输出参数。 如果无法使用输出参数，则编写分部方法实现，而不是依靠 O/R 设计器生成的重写。 在成功完成 INSERT 或 UPDATE 操作后，需要将映射到数据库生成的值的成员设置为相应的值。 有关详细信息，请参阅 [开发人员在重写默认行为中的责任](/dotnet/framework/data/adonet/sql/linq/responsibilities-of-the-developer-in-overriding-default-behavior)。

> [!NOTE]
> LINQ to SQL 会自动处理数据库生成的值，以使标识 (自动增量) 、rowguidcol (数据库生成的 GUID) 和时间戳列。 在其他列类型中，数据库生成的值将意外导致 Null 值。 若要返回数据库生成的值，应手动将设置 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> 为 **true** ，并将设置 <xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A> 为以下值之一： [AutoSync](<xref:System.Data.Linq.Mapping.AutoSync.Always>)、 [AutoSync](<xref:System.Data.Linq.Mapping.AutoSync.OnInsert>)或 [AutoSync。](<xref:System.Data.Linq.Mapping.AutoSync.OnUpdate>)

## <a name="configure-the-update-behavior-of-an-entity-class"></a>配置实体类的更新行为

默认情况下，用于更新数据库的逻辑 (插入、更新和删除) 对 LINQ to SQL 实体类中的数据所做的更改由 LINQ to SQL 运行时提供。 该运行时创建默认的 INSERT、UPDATE 和 DELETE 命令，这些命令基于表的架构（列和主键信息）。 当不需要默认行为时，可以通过分配特定的存储过程，以执行操作表中数据所必需的插入、更新和删除操作来配置更新行为。 在不生成默认行为时（例如，实体类映射到视图时），也可以这样做。 最后，在数据库要求通过存储过程访问表时，您可以重写默认的更新行为。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-assign-stored-procedures-to-override-the-default-behavior-of-an-entity-class"></a>指定存储过程以重写实体类的默认行为

1. 在设计器中打开“LINQ to SQL”文件。 （在“解决方案资源管理器”中双击“.dbml”文件。）

2. 在“服务器资源管理器”或“数据库资源管理器”中，展开“存储过程”，找到要为实体类的 Insert、Update 和/或 Delete 命令使用的存储过程。

3. 将该存储过程拖到 **O/R 设计器** 上。

     该存储过程将作为 <xref:System.Data.Linq.DataContext> 方法添加到方法窗格中。 有关详细信息，请参阅 [DataContext 方法 (O/R Designer) ](../data-tools/datacontext-methods-o-r-designer.md)。

4. 选择要使用存储过程对其执行更新的实体类。

5. 在“属性”窗口中选择要替代的命令（“插入”、“更新”或“删除”）。

6. 单击“使用运行时”旁边的省略号 (...) 以打开“配置行为”对话框。

7. 选择“自定义”。

8. 在“自定义”列表中选择所需的存储过程。

9. 检查“方法自变量”和“类属性”列表以验证“方法自变量”是否映射到相应的“类属性”。 将 () 的原始方法参数映射 `Original_<ArgumentName>` 到 `<PropertyName> (Original)` 和命令 () 的原始 `Update` 属性 `Delete` 。

    > [!NOTE]
    > 默认情况下，名称匹配时方法自变量映射到类属性。 如果更改的属性名称在表和实体类之间不再匹配，而设计器无法确定正确的映射，您可能需要选择等效的类属性进行映射。

10. 单击“**确定**”或“**应用**”。

    > [!NOTE]
    > 只要在每次更改后单击 " **应用** "，就可以继续为每个类和行为组合配置行为。 如果在单击 " **应用**" 之前更改类或行为，则会出现一个警告对话框，并提供应用更改的机会。

若要恢复为使用默认运行时更新逻辑，请单击“属性”窗口中“插入”、“更新”或“删除”命令旁边的省略号，然后在“配置行为”对话框中选择“使用运行时”。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [DataContext 方法](../data-tools/datacontext-methods-o-r-designer.md)
- [LINQ to SQL (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/index)
- [ (.NET Framework 的插入、更新和删除操作) ](/dotnet/framework/data/adonet/sql/linq/insert-update-and-delete-operations)
