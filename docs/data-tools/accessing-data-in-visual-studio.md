---
title: 在 Visual Studio 中处理数据
description: 使用 Visual Studio 中的数据。 通过本地计算机、Lan 或公有云或私有云创建连接到其他数据库产品或服务中的数据的应用。
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
ms.openlocfilehash: 24051678c5d17344684c806abde7940bc619b10e
ms.sourcegitcommit: 3cfe24a74b611440b831d9591e067874c51a3bfb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2021
ms.locfileid: "130087470"
---
# <a name="work-with-data-in-visual-studio"></a>在 Visual Studio 中处理数据

在 Visual Studio 中，你可以创建应用程序，这些应用程序在任何格式、任何位置、本地计算机上、在本地计算机上或在公有云、私有云或混合云中以任何格式连接到数据。

对于 JavaScript、Python、PHP、Ruby 或 c + + 中的应用程序，你可以通过获取库和编写代码来连接到你执行任何其他操作等数据。 对于 .net 应用程序，Visual Studio 提供可用于浏览数据源、创建对象模型以便在内存中存储和处理数据以及将数据绑定到用户界面的工具。 Microsoft Azure 提供适用于 .net、Java、Node.js、PHP、Python、Ruby 和移动应用的 sdk 以及用于连接到 Azure 存储的 Visual Studio 中的工具。

::: moniker range="vs-2017"
以下列表仅显示了可从 Visual Studio 中使用的多个数据库和存储系统中的几个。 [Microsoft Azure](https://azure.microsoft.com/)产品是数据服务，其中包括基础数据存储的所有预配和管理。 利用 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)中的 **azure 开发** 工作负载，你可以直接从 Visual Studio 使用 azure 数据存储。
::: moniker-end
::: moniker range=">=vs-2019"
以下列表仅显示了可从 Visual Studio 中使用的多个数据库和存储系统中的几个。 [Microsoft Azure](https://azure.microsoft.com/)产品是数据服务，其中包括基础数据存储的所有预配和管理。 利用 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)中的 **azure 开发** 工作负载，你可以直接从 Visual Studio 使用 azure 数据存储。
::: moniker-end

![Azure 开发工作负载](media/azure-development-workload.png)

此处列出的大部分其他 SQL 和 NoSQL 数据库产品可以托管在本地计算机、本地网络或虚拟机上的 Microsoft Azure 中。 如果在 Microsoft Azure 虚拟机中托管数据库，则需要负责管理数据库本身。

**Microsoft Azure**

- SQL 数据库
- Azure Cosmos DB
- 存储 (blob、表、队列和文件) 
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
- OrientDB |
- RavenDB
- VelocityDB
- 等等。

::: moniker range="vs-2017"

许多数据库供应商和第三方通过 NuGet 包支持 Visual Studio 集成。 您可以在 nuget.org 上或通过 NuGet 程序包管理器 Visual Studio (**工具**  >  **NuGet 程序包管理器**  >  **管理解决方案 NuGet 的) 包** 中了解产品/服务。 其他数据库产品与 Visual Studio 作为扩展集成。 你可以在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/)中浏览这些产品/服务，也可以导航到 "**工具**" "  >  **扩展和更新**"，然后在对话框的左窗格中选择 "**联机**"。 有关详细信息，请参阅[Visual Studio 的兼容数据库系统](../data-tools/installing-database-systems-tools-and-samples.md)。

::: moniker-end

::: moniker range=">=vs-2019"

许多数据库供应商和第三方通过 NuGet 包支持 Visual Studio 集成。 您可以在 nuget.org 上或通过 NuGet 程序包管理器 Visual Studio (**工具**  >  **NuGet 程序包管理器**  >  **管理解决方案 NuGet 的) 包** 中了解产品/服务。 其他数据库产品与 Visual Studio 作为扩展集成。 你可以在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/)中浏览这些产品/服务，或者导航到 "**扩展**" "  >  **管理扩展**"，然后在对话框的左窗格中选择 "**联机**"。 有关详细信息，请参阅[Visual Studio 的兼容数据库系统](../data-tools/installing-database-systems-tools-and-samples.md)。

::: moniker-end

> [!NOTE]
> 对 SQL Server 2005 的延长支持已于 2016 年 4 月 12 日结束。 不保证 Visual Studio 2015 及更高版本中的数据工具将继续与 SQL Server 2005 一起使用。 有关详细信息，请参阅[SQL Server 2005 的支持终止公告](https://www.microsoft.com/sql-server/sql-server-2005)。

## <a name="net-languages"></a>.NET 语言

所有 .net 数据访问（包括在 .net Core 中）都基于 ADO.NET，这是一组类，用于定义用于访问任何类型数据源（关系数据源和非关系数据源）的接口。 Visual Studio 具有多个工具和设计器，这些工具和设计器可与 ADO.NET 结合使用，以帮助你连接到数据库、操作数据以及向用户提供数据。 本部分中的文档介绍了如何使用这些工具。 您还可以对 ADO.NET 命令对象直接编程。 有关直接调用 ADO.NET api 的详细信息，请参阅[ADO.NET](/dotnet/framework/data/adonet/index)。

有关与 ASP.NET 相关的数据访问文档，请参阅使用 ASP.NET 网站上的[数据](https://www.asp.net/web-forms/overview/presenting-and-managing-data)。 有关将实体框架与 ASP.NET MVC 配合使用的教程，请参阅[使用 mvc 5 入门与实体框架 6 Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)。

通用 Windows 平台 (UWP) c # 中的应用或 Visual Basic 可以使用用于 .NET 的 Microsoft Azure SDK 访问 Azure 存储和其他 Azure 服务。 Windows。HttpClient 类启用与任何 RESTful 服务的通信。 有关详细信息，请参阅[如何使用 Windows 连接到 HTTP 服务器。Http.sys](/previous-versions/windows/apps/dn469430(v=win.10))。

对于本地计算机上的数据存储，推荐的方法是使用 SQLite，此方法在应用程序的进程中运行。 如果需要 (ORM) 层的对象关系映射，则可以使用实体框架。 有关详细信息，请参阅 Windows 开发人员中心的[数据访问权限](/windows/uwp/data-access/index)。

如果要连接到 Azure 服务，请确保下载最新的 [AZURE SDK 工具](https://azure.microsoft.com/downloads/)。

### <a name="data-providers"></a>数据提供程序

对于要在 ADO.NET 中使用的数据库，该数据库必须具有自定义 *ADO.NET 数据提供程序*，否则必须公开 ODBC 或 OLE DB 接口。 Microsoft 提供 SQL Server 产品以及 ODBC 和 OLE DB 提供程序的[ADO.NET 数据提供程序列表](/dotnet/framework/data/adonet/ado-net-overview)。

::: moniker range=">=vs-2022"
> [!NOTE]
> 如果使用 Visual Studio 2022 连接到 OLEDB 或 ODBC 数据访问接口，则需要注意 Visual Studio 2022 现在是64位进程。
>
> 这意味着，Visual Studio 中的某些数据工具将无法使用32位数据提供程序连接到 OLEDB 或 ODBC 数据库。 这包括 Microsoft Access 32 位 OLEDB 数据访问接口以及其他第三方32位提供程序。
>
>如果需要维护连接到 OLEDB 或 ODBC 的32位应用程序，仍可以 Visual Studio 2022 生成并运行该应用程序。 但是，如果需要使用任何 Visual Studio 数据工具（如服务器资源管理器、数据源向导或数据集设计器），则需要使用仍为32位进程的 Visual Studio 的早期版本。 32位进程 Visual Studio 的最后版本 Visual Studio 2019。
>
>如果计划将项目转换为64位进程，则需要更新 OLEDB 和 ODBC 数据连接才能使用64位数据访问接口。
>
>如果你的应用程序使用 Microsoft Access 数据库，并可以将项目转换为64位，则建议你使用64位 Microsoft Access 数据库引擎（也称为访问连接引擎 (ACE) ）。 有关详细信息，请参阅 [适用于 Jet 和 ODBC 驱动程序的 OLE DB 提供程序是32位版本](/office/troubleshoot/access/jet-odbc-driver-available-32-bit-version) 。
>
>如果你使用的是第三方数据提供程序，我们建议与你的供应商联系，以了解在将项目转换为64位之前，它们是否提供了64位提供程序。

::: moniker-end

### <a name="data-modeling"></a>数据建模

在 .NET 中，你有三种方法可以在从数据源中检索数据后在内存中对数据进行建模和操作：

[实体框架](../data-tools/entity-data-model-tools-in-visual-studio.md) 首选的 Microsoft ORM 技术。 您可以使用它来针对关系数据编程，作为第一类 .NET 对象。 对于新应用程序，它应该是需要模型时的默认首选项。 它需要底层 ADO.NET 提供程序的自定义支持。

[LINQ to SQL](../data-tools/linq-to-sql-tools-in-visual-studio2.md)早期代对象关系映射器。 它适用于不太复杂的方案，但不再处于活动状态。

[数据集](../data-tools/dataset-tools-in-visual-studio.md) 最早的三个建模技术。 它主要设计用于快速开发 "窗体超过数据" 应用程序，在这些应用程序中，您不会处理大量数据或执行复杂的查询或转换。 DataSet 对象由数据表和 DataRow 对象组成，它们在逻辑上类似于 SQL 数据库对象，而不仅仅是 .net 对象。 对于基于 SQL 数据源的相对简单的应用程序，数据集可能仍是一个不错的选择。

不需要使用其中的任何一种技术。 在某些情况下，尤其是在性能至关重要的情况下，只需使用 DataReader 对象从数据库中读取数据，并将需要的值复制到集合对象（如 List） \<T> 。

## <a name="native-c"></a>本机 C++

在大多数情况下，连接到 SQL Server 的 c + + 应用程序应使用[Microsoft® ODBC 驱动程序13.1 进行 SQL Server](https://www.microsoft.com/download/details.aspx?id=53339) 。 如果服务器已链接，则 OLE DB 是必需的，并且你使用[SQL Server Native Client](/sql/relational-databases/native-client/sql-server-native-client)。 您可以直接使用 [ODBC](/sql/odbc/microsoft-open-database-connectivity-odbc?view=sql-server-2017&preserve-view=true) 或 OLE DB 驱动程序来访问其他数据库。 ODBC 是当前的标准数据库接口，但大多数数据库系统都提供无法通过 ODBC 接口访问的自定义功能。 OLE DB 是一种旧的 COM 数据访问技术，仍受支持，但不建议用于新应用程序。 有关详细信息，请参阅 [Visual C++ 中的数据访问](/cpp/data/data-access-in-cpp)。

使用 REST 服务的 c + + 程序可使用 [c + + REST SDK](https://github.com/Microsoft/cpprestsdk)。

使用 Microsoft Azure 存储的 c + + 程序可以使用[Microsoft Azure 存储客户端](https://www.nuget.org/packages/Microsoft.Azure.Storage.CPP)。

数据建模 &mdash; Visual Studio 不提供 c + + 的 ORM 层。 [ODB](https://www.codesynthesis.com/products/odb/) 是适用于 c + + 的常用开源 ORM。

若要详细了解如何从 c + + 应用程序连接到数据库，请参阅[Visual Studio data tools for c + +](../data-tools/visual-studio-data-tools-for-cpp.md)。 有关旧 Visual C++ 数据访问技术的详细信息，请参阅 [数据访问](/cpp/data/data-access-in-cpp)。

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
