---
title: 无法删除后备方法
description: 此相关方法是以下默认插入、更新或删除方法的支持方法
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 62afa6da-97cf-48b9-8de3-33e4d72a0377
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 94e9f1f91aa5c879e0e3ed0034e0d1f554901513
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866367"
---
# <a name="this-related-method-is-the-backing-method-for-the-following-default-insert-update-or-delete-methods"></a>此相关方法是以下默认插入、更新或删除方法的支持方法

此相关方法是以下默认 `Insert` 、或方法的后备方法 `Update` `Delete` 。 如果删除这些方法，则备份方法也将被删除。 是否要继续?

所选 `DataContext` 方法当前用作 `Insert` `Update` `Delete` **O/R 设计器** 上某个实体类的、或方法之一。 删除所选方法会导致使用此方法的实体类恢复为在更新过程中执行插入、更新或删除操作的默认运行时行为。

## <a name="selected-method-options"></a>选择的方法选项

- 若要删除所选方法，使实体类使用运行时更新，请单击 **"是"**。

   将删除所选方法，并使用默认的 LINQ to SQL 运行时行为将使用此方法替代更新行为的任何类还原为。

- 若要关闭该消息框，使所选方法保持不变，请单击 " **否**"。

   消息框关闭，不进行任何更改。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)