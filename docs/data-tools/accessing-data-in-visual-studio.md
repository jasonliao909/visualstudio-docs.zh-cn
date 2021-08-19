---
title: 在 Visual Studio 中处理数据
description: 使用数据Visual Studio。 创建通过本地计算机、LAN 或公有云或私有云连接到其他数据库产品或服务中数据的应用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data [Visual Studio]
- data access [Visual Studio]
- data [C#]
- ADO.NET, data access
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 0b6f79c38b599a66a9609bd88399f075f54f59dd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122154974"
---
# <a name="work-with-data-in-visual-studio"></a>在 Visual Studio 中处理数据

在 Visual Studio 中，可以创建连接到几乎任何数据库产品或服务、任何格式、任何位置（本地计算机、本地区域网络或公有云、私有云或混合云）的数据的应用程序。

对于 JavaScript、Python、PHP、Ruby 或 C++ 中的应用程序，通过获取库和编写代码，可以像连接任何其他操作一样连接到数据。 对于 .NET 应用程序，Visual Studio提供的工具可用于浏览数据源、创建对象模型以存储和操作内存中的数据，以及将数据绑定到用户界面。 Microsoft Azure .NET、Java、Node.js、PHP、Python、Ruby 和移动应用的 SDK，以及 Visual Studio 中用于连接到 Azure 存储 的工具。

::: moniker range="vs-2017"
以下列表只显示了许多数据库和存储系统中的一些，可以从 Visual Studio。 服务[Microsoft Azure](https://azure.microsoft.com/)包括基础数据存储的所有预配和管理的数据服务。 使用[2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) Visual Studio中的 Azure 开发工作负载，可以直接从 Visual Studio。 
::: moniker-end
::: moniker range=">=vs-2019"
以下列表只显示了许多数据库和存储系统中的一些，可以从 Visual Studio。 服务[Microsoft Azure](https://azure.microsoft.com/)包括基础数据存储的所有预配和管理的数据服务。 使用[2019](https://visualstudio.microsoft.com/downloads) Visual Studio 中的 Azure 开发工作负载，可以直接从 Visual Studio。 
::: moniker-end

![Azure 开发工作负载](media/azure-development-workload.png)

此处列出的大多数其他 SQL 和 NoSQL 数据库产品可以托管在本地计算机上、本地网络上或Microsoft Azure虚拟机上。 如果在虚拟机中托管Microsoft Azure，则你负责管理数据库本身。

**Microsoft Azure**

- SQL 数据库
- Azure Cosmos DB
- 存储 (Blob、表、队列、文件) 
- SQL 数据仓库
- SQL Server Stretch Database
- StorSimple
- 等等。

**SQL**

- SQL Server 2005-2016 (包括 Express 和 LocalDB) 
- Firebird
- MariaDB
- MySQL
- Oracle
- PostgreSQL
- SQLite
- 等等。

**NoSQL**

- Apache Cassandra
- CouchDB
- MongoDB
- NDatabase
- 方向DB|
- RavenDB
- VelocityDB
- 等等。

::: moniker range="vs-2017"

许多数据库供应商和第三方支持Visual Studio包进行NuGet集成。 可以浏览 nuget.org 上的产品/服务，NuGet 程序包管理器在 Visual Studio (Tools NuGet 程序包管理器 Manage   >    >  **NuGet Packages for Solution) 。** 其他数据库产品与 Visual Studio作为扩展集成。 可以在 Visual Studio Marketplace 中浏览这些产品/服务，[或者导航到"工具扩展和更新"，](https://marketplace.visualstudio.com/)然后在对话框的左窗格中选择"联机  >  "。  有关详细信息，请参阅兼容的[数据库系统Visual Studio。](../data-tools/installing-database-systems-tools-and-samples.md)

::: moniker-end

::: moniker range=">=vs-2019"

许多数据库供应商和第三方支持Visual Studio包进行NuGet集成。 可以浏览 nuget.org 上的产品/服务，NuGet 程序包管理器在 Visual Studio (Tools NuGet 程序包管理器 Manage   >    >  **NuGet Packages for Solution) 。** 其他数据库产品与 Visual Studio作为扩展集成。 可以在 Visual Studio Marketplace 中浏览这些产品/服务，或者导航[到"扩展""管理扩展](https://marketplace.visualstudio.com/)"，然后在对话框的左窗格中选择"联机  >  "。  有关详细信息，请参阅兼容的[数据库系统Visual Studio。](../data-tools/installing-database-systems-tools-and-samples.md)

::: moniker-end

> [!NOTE]
> 对 SQL Server 2005 的延长支持已于 2016 年 4 月 12 日结束。 无法保证 2015 Visual Studio及更高版本的数据工具将继续在 2005 SQL Server使用。 有关详细信息，请参阅[2005](https://www.microsoft.com/sql-server/sql-server-2005)年 5 月的支持终止SQL Server公告。

## <a name="net-languages"></a>.NET 语言

所有 .NET 数据访问（包括在 .NET Core 中）都基于 ADO.NET，ADO.NET 是一组类，用于定义用于访问任何类型的数据源（关系数据源和非关系数据源）的接口。 Visual Studio具有多个工具和设计器，它们 ADO.NET 帮助连接到数据库、操作数据以及向用户呈现数据。 本部分中的文档介绍如何使用这些工具。 还可以直接针对命令 ADO.NET 编程。 有关直接调用 ADO.NET API 的信息[，请参阅](/dotnet/framework/data/adonet/index)ADO.NET。

有关与数据相关的数据访问 ASP.NET，[请参阅在](https://www.asp.net/web-forms/overview/presenting-and-managing-data)ASP.NET 站点上使用数据。 有关将 实体框架 ASP.NET MVC 的教程，入门[MVC 5 实体框架 Code First 6 的教程](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)。

通用 Windows 平台 (C#) UWP Visual Basic 应用可以使用 用于 .NET 的 Microsoft Azure SDK 访问 Azure 存储 和其他 Azure 服务。 Windows。Web.HttpClient 类允许与任何 RESTful 服务通信。 有关详细信息，请参阅如何使用 Windows[连接到 HTTP 服务器。Web.Http](/previous-versions/windows/apps/dn469430(v=win.10))。

对于本地计算机上数据存储，建议的方法是使用 SQLite，该 SQLite 与应用在同一进程中运行。 如果需要在 ORM 层 (对象) 映射，可以使用实体框架。 有关详细信息，[请参阅开发人员中心](/windows/uwp/data-access/index)Windows数据访问。

如果要连接到 Azure 服务，请务必下载最新的 [Azure SDK 工具](https://azure.microsoft.com/downloads/)。

### <a name="data-providers"></a>数据提供程序

若要在数据库中使用 ADO.NET，该数据库必须具有自定义 ADO.NET 数据提供程序 *，* 否则必须公开 ODBC 或 OLE DB接口。 Microsoft 提供了[适用于 ADO.NET](/dotnet/framework/data/adonet/ado-net-overview)产品SQL Server ODBC 和 OLE DB 提供程序的列表。

### <a name="data-modeling"></a>数据建模

在 .NET 中，在从数据源检索数据后，有三个选项用于对内存中的数据进行建模和操作：

[实体框架](../data-tools/entity-data-model-tools-in-visual-studio.md) 首选 Microsoft ORM 技术。 可以使用它以第一类 .NET 对象对关系数据进行编程。 对于新应用程序，它应该是需要模型时的默认第一个选择。 它需要基础提供程序的自定义 ADO.NET 支持。

[LINQ to SQL](../data-tools/linq-to-sql-tools-in-visual-studio2.md)早期生成的对象关系映射器。 它适用于不太复杂的方案，但不再用于主动开发。

[数据集](../data-tools/dataset-tools-in-visual-studio.md) 三种建模技术中最早的一种。 它主要用于快速开发"基于数据的表单"应用程序，其中不会处理大量数据或执行复杂的查询或转换。 DataSet 对象由 DataTable 和 DataRow 对象组成，这些对象在逻辑上SQL数据库对象比 .NET 对象要多。 对于基于数据源的SQL应用程序，数据集可能仍是一个不错的选择。

无需使用上述任何技术。 在某些情况下，尤其是在性能至关重要的情况下，只需使用 DataReader 对象从数据库读取，将所需的值复制到集合对象（如列表 \<T> ）中。

## <a name="native-c"></a>本机 C++

在大多数情况下，连接到 SQL Server 的 C++ 应用程序® [Microsoft SQL Server ODBC Driver 13.1。](https://www.microsoft.com/download/details.aspx?id=53339) 如果服务器已链接，OLE DB是必需的，并且对于使用[SQL Server Native Client。](/sql/relational-databases/native-client/sql-server-native-client) 可以使用 [ODBC](/sql/odbc/microsoft-open-database-connectivity-odbc?view=sql-server-2017&preserve-view=true) 访问其他数据库，也可以OLE DB驱动程序。 ODBC 是当前的标准数据库接口，但大多数数据库系统都提供无法通过 ODBC 接口访问的自定义功能。 OLE DB是一种旧版 COM 数据访问技术，仍受支持，但不建议用于新应用程序。 有关详细信息，请参阅 [Visual C++ 中的数据访问](/cpp/data/data-access-in-cpp)。

使用 REST 服务的 C++ 程序可以使用 [C++ REST SDK](https://github.com/Microsoft/cpprestsdk)。

使用客户端 的 C++ Microsoft Azure 存储可以使用[Microsoft Azure 存储 客户端](https://www.nuget.org/packages/Microsoft.Azure.Storage.CPP)。

数据建模 &mdash; Visual Studio不提供 C++ 的 ORM 层。 [ODB](https://www.codesynthesis.com/products/odb/) 是适用于 C++ 的常用开源 ORM。

若要详细了解如何从 C++ 应用连接到数据库，请参阅[Visual Studio C++ 的数据工具](../data-tools/visual-studio-data-tools-for-cpp.md)。 有关旧 Visual C++ 数据访问技术的详细信息，请参阅 [数据访问](/cpp/data/data-access-in-cpp)。

## <a name="javascript"></a>JavaScript

[Visual Studio 中的 JavaScript](/scripting/javascript/javascript-language-reference)是一种用于构建跨平台应用、UWP 应用、云服务、网站和 web 应用的一流语言。 您可以使用 Visual Studio 中的 Bower、Grunt、Gulp、npm 和 NuGet 来安装您最喜爱的 JavaScript 库和数据库产品。 通过从[azure 网站](https://azure.microsoft.com/)下载 sdk 连接到 azure 存储和服务。 Edge.js 是将服务器端 JavaScript (Node.js) 连接到 ADO.NET 数据源的库。

## <a name="python"></a>Python

[在 Visual Studio 中安装 python 支持](../python/overview-of-python-tools-for-visual-studio.md)以创建 python 应用程序。 Azure 文档包含几个有关连接到数据的教程，其中包括：

- [Azure 上的 Django 和 SQL 数据库](/azure/app-service/app-service-web-get-started-python)
- [Azure 上的 Django 和 MySQL](/azure/app-service-web/web-sites-python-ptvs-django-mysql)
- [ (COSMO DB) ](/azure/cosmos-db/table-storage-how-to-use-python)使用[blob](/azure/storage/blobs/storage-quickstart-blobs-python)、[文件](/azure/storage/files/storage-python-how-to-use-file-storage)、[队列](/azure/storage/queues/storage-python-how-to-use-queue-storage)和表。

## <a name="related-topics"></a>相关主题

[MICROSOFT AI 平台](https://azure.microsoft.com/overview/ai-platform/?v=17.42w) &mdash;介绍 Microsoft 智能云，包括 Cortana 分析套件和对物联网的支持。

[Microsoft Azure 存储](/azure/storage/) &mdash;介绍 Azure 存储，以及如何使用 Azure blob、表、队列和文件创建应用程序。

[Azure SQL 数据库](/azure/sql-database/) &mdash;描述如何连接到作为服务的关系数据库 Azure SQL 数据库。

[SQL Server Data Tools](/sql/ssdt/download-sql-server-data-tools-ssdt) &mdash;介绍简化数据连接的应用程序和数据库的设计、探索、测试和部署的工具。

[ADO.NET](/dotnet/framework/data/adonet/index) &mdash;介绍 ADO.NET 的体系结构，以及如何使用 ADO.NET 类管理应用程序数据以及与数据源和 XML 进行交互。

[ADO.NET 实体框架](/ef/ef6/) &mdash;介绍如何创建允许开发人员针对概念模型而不是直接针对关系数据库进行编程的数据应用程序。

[WCF Data Services 4.5](/dotnet/framework/data/wcf/index) &mdash;描述如何使用 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 在实现[Open Data Protocol (OData) ](https://www.odata.org/)的 web 或 intranet 上部署数据服务。

[Office 解决方案](../vsto/data-in-office-solutions.md) &mdash; 中的数据包含指向一些主题的链接，这些主题说明如何在 Office 解决方案中处理数据。 这包括有关面向架构的编程、数据缓存和服务器端数据访问的信息。

[LINQ (语言集成查询) ](/dotnet/csharp/linq/) &mdash;介绍 c # 和 Visual Basic 中内置的查询功能，以及用于查询关系数据库、XML 文档、数据集和内存中集合的通用模型。

Visual Studio 中的[XML 工具](../xml-tools/xml-tools-in-visual-studio.md) &mdash;讨论如何使用 XML 数据、调试 XSLT、.NET XML 功能和 XML 查询的体系结构。

[XML 文档和数据](/dotnet/standard/data/xml/index) &mdash;概述了一组全面的集成类，这些类可用于 .NET 中的 XML 文档和数据。