---
title: 不支持的数据库提供程序
description: 所选连接使用不支持的数据库提供程序。 查看此 Visual Studio 对象关系设计器（O/R 设计器）消息的相关信息。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601077"
---
# <a name="the-selected-connection-uses-an-unsupported-database-provider"></a>所选连接使用不支持的数据库提供程序

在将未使用适用于 SQL Server 的 .NET Framework 数据提供程序的项从“服务器资源管理器”或“数据库资源管理器”拖动到 [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)上时，会出现此消息 。

O/R 设计器仅支持使用适用于 SQL Server 的 .NET Framework 提供程序的数据连接。 只有指向 Microsoft SQL Server 或 Microsoft SQL Server 数据库文件的连接才有效。

此错误的更正方法：仅当项来自于使用适用于 SQL Server 的 .NET Framework 数据提供程序的数据连接时，才将其添加到 O/R 设计器中。

## <a name="see-also"></a>另请参阅

- <xref:System.Data.SqlClient>
- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
