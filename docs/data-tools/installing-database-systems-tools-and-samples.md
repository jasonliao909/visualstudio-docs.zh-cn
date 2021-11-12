---
title: 数据库兼容性
description: 查看 Visual Studio 的兼容数据库系统，例如 Microsoft SQL Server、Oracle、MySQL、PostgreSQL、SQLite 和 Firebird。
ms.custom: SEO-VS-2020
ms.date: 09/06/2017
ms.topic: conceptual
helpviewer_keywords:
- database systems
- database compatibility
- databases for Visual Studio
ms.assetid: 821de34b-eaa9-40af-b9aa-b8305de16899
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 6ccbf0866022e6e602938d2a5f86f8374eb73c89
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601128"
---
# <a name="compatible-database-systems-for-visual-studio"></a>适用于 Visual Studio 的兼容数据库系统

若要在 Visual Studio 中开发与数据连接的应用程序，通常在本地开发计算机上安装数据库系统，然后在应用程序和数据库准备就绪时将其部署到生产环境。 Visual Studio 会在你的计算机上安装 SQL Server Express LocalDB 作为“数据存储和处理”工作负载的一部分。 此 LocalDB 实例适用于快速轻松地开发与数据连接的应用程序。

为了使数据库系统可从 .NET 应用程序访问并在 Visual Studio 数据工具窗口中可见，它必须具有 ADO.NET 数据提供程序。 如果计划在 .NET 应用程序中使用实体数据模型，提供程序必须专门支持实体框架。 许多提供程序通过 NuGet 包管理器或通过 Visual Studio Marketplace 提供。

如果使用的是 Azure 存储 API，请于开发期间在本地计算机上安装 Azure 存储储拟器以避免产生费用，直到准备好部署到生产环境为止。 有关详细信息，请参阅[使用 Azure 存储模拟器进行开发和测试](/azure/storage/common/storage-use-emulator)。

下面的列表包含一些可在 Visual Studio 项目中使用的更常用的数据库系统。 表格并不详尽。 若要通过列表了解提供可实现与 Visual Studio 工具的深度集成的 ADO.NET 数据提供程序的第三方供应商，请参阅 [ADO.NET 数据提供程序](/dotnet/framework/data/adonet/data-providers)。

## <a name="microsoft-sql-server"></a>Microsoft SQL Server

SQL Server 是 Microsoft 旗舰数据库产品/服务。 SQL Server 2016 提供了突破性的性能、高级安全性和丰富的集成报告和分析。 它随附在为不同用途设计的各种版本中：从高度可缩放的高性能业务分析，到在单台计算机上的使用。 SQL Server Express 是一个功能齐全的 SQL Server 版本，专为重新分发和嵌入而定制。  LocalDB 是一个简化的 SQL Server Express 版本，无需进行配置并在应用程序的进程中运行。 可从 [SQL Server Express 下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)下载任一或全部两款产品。 本部分中的许多 SQL 示例都使用 SQL Server LocalDB。 SQL Server Management Studio (SSMS) 是独立的数据库管理应用程序，其功能比 Visual Studio SQL Server 对象资源管理器中提供的功能要多。 可从上述链接获取 SSMS。

## <a name="oracle"></a>Oracle

可从 [Oracle 技术网络](https://www.oracle.com/database/technologies/oracle-database-software-downloads.html)页下载 Oracle 数据库的付费版本或免费版本。 对于实体框架和 Tableadapter 的设计时支持，将需要[适用于 Visual Studio 的 Oracle 开发人员工具](https://www.oracle.com/database/technologies/developer-tools/visual-studio/)。 其他官方 Oracle 产品（包括 Oracle 即时客户端）通过 NuGet 包管理器提供。 可按照 [Oracle 联机文档](https://docs.oracle.com/cd/E11882_01/server.112/e10831/toc.htm)中的说明下载 Oracle 示例架构。

## <a name="mysql"></a>MySQL

MySQL 是一种常用的开源数据库系统，广泛用于企业和网站。 可在 [ MySQL on Windows](https://www.mysql.com/why-mysql/windows/) 下载 MySQL、MySQL for Visual Studio 和相关产品。 第三方为 MySQL 提供了各种 Visual Studio 扩展和独立管理应用程序。 可在 NuGet 包管理器中浏览产品/服务（“工具” > “NuGet 包管理器” > “管理解决方案 NuGet 包”  ）。

## <a name="postgresql"></a>PostgreSQL

PostgreSQL 是一个免费的开源对象关系数据库系统。 若要在 Windows 上安装它，可从[PostgreSQL 下载页](https://www.postgresql.org/download/windows/)下载。 还可从源代码生成 PostgreSQL。 PostgreSQL 核心系统包含 C 语言接口。 许多第三方提供了从 .NET 应用程序使用 PostgreSQL 的 NuGet 包。 可在 NuGet 包管理器中浏览产品/服务（“工具” > “NuGet 包管理器” > “管理解决方案 NuGet 包”  ）。 或许，最常用的包由 [npgsql.org](http://www.npgsql.org) 提供。

## <a name="sqlite"></a>SQLite

SQLite 是一款嵌入式 SQL 数据库引擎，它在应用程序自己的进程中运行。 可从 [ SQLite 下载页](https://www.sqlite.org/download.html)下载它。 还有许多用于 SQLite 的第三方 NuGet 包可供使用。 可在 NuGet 包管理器中浏览产品/服务（“工具” > “NuGet 包管理器” > “管理解决方案 NuGet 包”  ）。

## <a name="firebird"></a>Firebird

Firebird 是一个开源 SQL 数据库系统。 可从 [ Firebird 下载页](http://firebirdsql.org/en/downloads/)下载它。 ADO.NET 数据提供程序通过 NuGet 包管理器提供。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
- [如何确定 SQL Server 及其组件的版本和版本类别](https://support.microsoft.com/help/321185/how-to-determine-the-version-edition-and-update-level-of-sql-server-an)
