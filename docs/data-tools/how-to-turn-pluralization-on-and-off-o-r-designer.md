---
title: 如何：启用和禁用复数形式（O-R 设计器）
description: 了解如何在对象关系设计器（O/R 设计器）中启用和禁用复数形式。 默认设置将复数名称转换为单数名称。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 9b693bc3-303a-40a9-97ee-9cef5ca3ae81
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: f51d48f2d4af4ed723dbe0dcd720ee460e1feb1b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601130"
---
# <a name="how-to-turn-pluralization-on-and-off-or-designer"></a>如何：启用和禁用复数形式（O/R 设计器）
默认情况下，将名称以 s 或 ies 结尾的数据库对象从“服务器资源管理器”或“数据库资源管理器”拖放到 [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)上时，生成的实体类的名称从复数形式变为单数形式 。 这样可以更准确地表示实例化的实体类映射到单个数据记录的事实。 例如，将 `Customers` 表添加到 O/R 设计器将生成名为 `Customer` 的实体类，因为该类将仅为一个客户保存数据。

> [!NOTE]
> 默认情况下，复数形式仅在 Visual Studio 的英语版本中启用。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-turn-pluralization-on-and-off"></a>打开和关闭复数形式

1. 在 **“工具”** 菜单上，单击 **“选项”** 。

2. 在“选项”对话框中展开“数据库工具”。

    > [!NOTE]
    > 如果“数据库工具”节点不可见，请选择“显示所有设置”。

3. 单击“O/R 设计器”。

4. 将“名称的复数形式”设置为“启用 = False”，可将 O/R 设计器设置为不更改类名称   。

5. 将“名称的复数形式”设置为“启用 = True”，可向添加到 O/R 设计器的对象的类名称应用复数规则   。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
