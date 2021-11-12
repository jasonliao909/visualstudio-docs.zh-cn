---
title: 无法删除备份方法
description: 此相关方法是以下默认插入、更新或删除方法的支持方法
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 62afa6da-97cf-48b9-8de3-33e4d72a0377
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 8dcf07340584a3103a854dae3ffa7787cabee448
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601080"
---
# <a name="this-related-method-is-the-backing-method-for-the-following-default-insert-update-or-delete-methods"></a>此相关方法是以下默认插入、更新或删除方法的支持方法

此相关方法是下列默认 `Insert`、`Update` 或 `Delete` 方法的备份方法。 如果删除这些方法，则备份方法也将被删除。 是否要继续?

所选的 `DataContext` 方法当前用作 O/R 设计器上某实体类的 `Insert`、`Update` 或 `Delete` 方法之一。 如果删除所选方法，则使用此方法的实体类在更新过程中执行插入、更新或删除时将还原为默认的运行时行为。

## <a name="selected-method-options"></a>选择的方法选项

- 若要删除所选方法，使实体类使用运行时更新，请单击“是”。

   所选方法将被删除，并且使用此方法重写更新行为的所有类将还原为使用默认 LINQ to SQL 运行时行为。

- 关闭消息框，不对所选方法进行更改，单击“否”。

   消息框关闭，不进行任何更改。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)