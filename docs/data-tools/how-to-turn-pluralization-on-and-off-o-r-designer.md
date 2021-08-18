---
title: 如何：启用和禁用复数形式（O-R 设计器）
description: 了解如何对象关系设计器 (O/R 设计器) 打开和关闭复数形式。 默认设置将复数名称转换为单数形式。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122139668"
---
# <a name="how-to-turn-pluralization-on-and-off-or-designer"></a>如何：启用和禁用复数形式（O/R 设计器）
默认情况下，当您将名称以 s 或从 **服务器资源管理器** 结尾或 **数据库资源管理器** 的数据库对象拖到 [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)时，所生成的实体类的名称将从复数改为单数形式。 这样可以更准确地表示实例化的实体类映射到单个数据记录的事实。 例如，将表添加 `Customers` 到 **O/R 设计器** 会生成一个名为的实体类， `Customer` 因为该类只保存单个客户的数据。

> [!NOTE]
> 默认情况下，复数形式仅在 Visual Studio 的英语版本中启用。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-turn-pluralization-on-and-off"></a>打开和关闭复数形式

1. 在 **“工具”** 菜单上，单击 **“选项”** 。

2. 在“选项”对话框中展开“数据库工具”。

    > [!NOTE]
    > 如果“数据库工具”节点不可见，请选择“显示所有设置”。

3. 单击“O/R 设计器”。

4. 将 "**名称" 的复数形式****设置为 "**  =  **False** "，以设置 **O/R 设计器**，使其不更改类名称。

5. 将 **复数形式的名称** 设置 **为 "**  =  **True** " 可将复数形式规则应用于添加到 **O/R 设计器** 的对象的类名。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
