---
title: 不支持的数据库提供程序
description: 所选连接使用不受支持的数据库提供程序。 查看有关此Visual Studio 对象关系设计器 (O/R 设计器) 消息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 4d25dfa1-8fa4-4529-9b90-973bc2ec2993
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: b4956314b994d66e972a9e65a30ee5eb8d8aac13
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122121950"
---
# <a name="the-selected-connection-uses-an-unsupported-database-provider"></a>所选连接使用不支持的数据库提供程序

将不使用 .NET Framework Data Provider for SQL Server 的项从 服务器资源管理器 或 数据库资源管理器 拖动到 Visual Studio 中的LINQ to SQL 工具时，会出现[此消息](../data-tools/linq-to-sql-tools-in-visual-studio2.md)。

**O/R 设计器** 仅支持使用 .NET Framework Provider for SQL Server。 只有指向 Microsoft SQL Server 或 Microsoft SQL Server 数据库文件的连接才有效。

若要更正此错误，请仅将使用 .NET Framework Data Provider for SQL Server的数据连接中的项添加到 **O/R 设计器**。

## <a name="see-also"></a>请参阅

- <xref:System.Data.SqlClient>
- [LINQ to SQL工具Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
