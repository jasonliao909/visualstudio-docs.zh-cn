---
title: 不支持的数据类型
description: 一个或多个选定项包含设计器不支持的数据类型。 查看有关此Visual Studio O/R 设计器消息的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 71dcd4f9-2946-42c5-9ce4-99c819ea2785
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 55402288d52f6f4b5eeac41efbb15d9f164ff5cd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122075146"
---
# <a name="one-or-more-selected-items-contain-a-data-type-that-is-not-supported-by-the-designer"></a>一个或多个所选项包含设计器不支持的数据类型

从 服务器资源管理器 或 数据库资源管理器拖动到 **O/R** 设计器上的一个或多个项包含 **O/R** 设计器不支持的数据类型，例如 [CLR](/dotnet/framework/data/adonet/sql/clr-user-defined-types)用户定义类型 。 

## <a name="to-correct-this-error"></a>更正此错误

1. 创建一个基于所需的表的视图，且其中不包括不支持的数据类型。

2. 将视图 **从服务器资源管理器或****数据库资源管理器设计器** 上。

## <a name="see-also"></a>请参阅

- [LINQ to SQL工具Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
