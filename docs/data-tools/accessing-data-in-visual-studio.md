---
title: 在 Visual Studio 中处理数据
description: 在 Visual Studio 中处理数据。 通过本地计算机、LAN、公有云或私有云创建连接到其他数据库产品或服务中的数据的应用。
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
ms.openlocfilehash: 053fd7e5607103a9a3b0ece521556bcbe34bb446
ms.sourcegitcommit: 11a02f6a01fe73349084663a0b39909969ce6931
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2022
ms.locfileid: "140812378"
---
# <a name="work-with-data-in-visual-studio"></a>在 Visual Studio 中处理数据

在 Visual Studio 中，你可以创建连接到几乎任何数据库产品或服务中的数据的应用程序，无论数据采用何种格式、位于何处（本地计算机、局域网或公有/私有/混合云），均可连接。

对于采用 JavaScript、Python、PHP、Ruby 或 C++ 的应用程序，通过获取库和编写代码，可以像执行其他任何操作一样连接到数据。 对于 .NET 应用程序，Visual Studio 提供可用于浏览数据源、创建对象模型以便在内存中存储和操作数据以及将数据绑定到用户界面的工具。 Microsoft Azure 提供适用于 .NET、Java、Node.js、PHP、Python、Ruby 和移动应用的 SDK 以及 Visual Studio 中用于连接到 Azure 存储的工具。

::: moniker range="vs-2017"
以下列表仅显示了可从 Visual Studio 中使用的多个数据库和存储系统的一小部分。 [Microsoft Azure](https://azure.microsoft.com/) 产品/服务是数据服务，其中包括对基础数据存储的所有预配和管理。 利用 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) 中的 Azure 开发工作负载，你可以直接从 Visual Studio 使用 Azure 数据存储。
::: moniker-end
::: moniker range=">=vs-2019"
以下列表仅显示了可从 Visual Studio 中使用的多个数据库和存储系统的一小部分。 [Microsoft Azure](https://azure.microsoft.com/) 产品/服务是数据服务，其中包括对基础数据存储的所有预配和管理。 使用 **Visual Studio** 中的 Azure [开发工作负载，](https://visualstudio.microsoft.com/downloads)可以直接从 Visual Studio。
::: moniker-end

![Azure 开发工作负载](media/azure-development-workload.png)

此处列出的大部分其他 SQL 和 NoSQL 数据库产品可以托管在本地计算机、本地网络或虚拟机上的 Microsoft Azure 中。 如果在 Microsoft Azure 虚拟机中托管数据库，则需要负责管理数据库本身。

**Microsoft Azure**

- SQL 数据库
- Azure Cosmos DB
- 存储（Blob、表、队列、文件）
- SQL 数据仓库
- SQL Server Stretch Database
- StorSimple
- 等等。

**SQL**

- SQL Server 2005 - 2016（包括 Express 和 LocalDB）
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
- OrientDB|
- RavenDB
- VelocityDB
- 等等。

::: moniker range="vs-2017"

许多数据库供应商和第三方通过 NuGet 包支持 Visual Studio 集成。 可在 nuget.org 上或通过 Visual Studio 中的 NuGet 包管理器浏览产品/服务（“工具” > “NuGet 包管理器” > “管理解决方案 NuGet 包”  ）。 其他数据库产品作为扩展与 Visual Studio 集成。 你可以在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) 中，也可以通过导航到“工具” > “扩展和更新”，然后在对话框的左窗格中选择“联机”来浏览这些产品/服务  。 有关详细信息，请参阅[适用于 Visual Studio 的兼容数据库系统](../data-tools/installing-database-systems-tools-and-samples.md)。

::: moniker-end

::: moniker range=">=vs-2019"

许多数据库供应商和第三方通过 NuGet 包支持 Visual Studio 集成。 可在 nuget.org 上或通过 Visual Studio 中的 NuGet 包管理器浏览产品/服务（“工具” > “NuGet 包管理器” > “管理解决方案 NuGet 包”  ）。 其他数据库产品作为扩展与 Visual Studio 集成。 你可以在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) 中，也可以通过导航到“扩展” > “管理扩展”，然后在对话框的左窗格中选择“联机”来浏览这些产品/服务  。 有关详细信息，请参阅[适用于 Visual Studio 的兼容数据库系统](../data-tools/installing-database-systems-tools-and-samples.md)。

::: moniker-end

> [!NOTE]
> 对 SQL Server 2005 的延长支持已于 2016 年 4 月 12 日结束。 不保证 Visual Studio 2015 及更高版本中的数据工具将继续与 SQL Server 2005 一起使用。 有关详细信息，请参阅 [SQL Server 2005 的支持终止公告](https://www.microsoft.com/sql-server/sql-server-2005)。

## <a name="net-languages"></a>.NET 语言

所有 .NET 数据访问（包括在 .NET Core 中）均基于 ADO.NET，这组类定义用于访问任何类型数据源（关系数据源和非关系数据源）的接口。 Visual Studio 具有多个工具和设计器，这些工具和设计器可与 ADO.NET 结合使用，以帮助你连接到数据库、操作数据以及向用户提供数据。 本部分中的文档介绍了如何使用这些工具。 你还可以直接根据 ADO.NET 命令对象编程。 有关直接调用 ADO.NET API 的详细信息，请参阅 [ADO.NET](/dotnet/framework/data/adonet/index)。

有关与 ASP.NET 相关的数据访问文档，请参阅在 ASP.NET 站点上[处理数据](https://www.asp.net/web-forms/overview/presenting-and-managing-data)。 有关将实体框架与 ASP.NET MVC 配合使用的教程，请参阅[使用 MVC 5 的 Entity Framework 6 Code First 入门](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)。

C# 或 Visual Basic 中的通用 Windows 平台 (UWP) 可以使用用于 .NET 的 Microsoft Azure SDK 访问 Azure 存储和其他 Azure 服务。 Windows.Web.HttpClient 类支持与任何 RESTful 服务进行通信。 有关详细信息，请参阅[如何使用 Windows.Web.Http 连接到 HTTP 服务器](/previous-versions/windows/apps/dn469430(v=win.10))。

对于本地计算机上的数据存储，推荐的方法是使用 SQLite，它与应用在同一进程中运行。 如果需要对象关系映射 (ORM) 层，则可以使用实体框架。 有关详细信息，请参阅 Windows 开发人员中心中的[数据访问](/windows/uwp/data-access/index)。

如果要连接到 Azure 服务，请确保下载最新的 [Azure SDK 工具](https://azure.microsoft.com/downloads/)。

### <a name="data-providers"></a>数据提供程序

对于要在 ADO.NET 中使用的数据库，必须具有自定义 ADO.NET 数据提供程序，否则必须公开 ODBC 或 OLE DB 接口。 Microsoft 提供适用于 SQL Server 产品的 [ADO.NET 数据提供程序列表](/dotnet/framework/data/adonet/ado-net-overview)以及 ODBC 和 OLE DB 提供程序。

::: moniker range=">=vs-2019"
> [!NOTE]
>如果使用 Visual Studio 连接到使用 OLEDB 或 ODBC 数据提供程序的数据库，则需要注意低于 Visual Studio 2022 的 Visual Studio 版本都是 32 位进程。 这意味着，Visual Studio 中的某些数据工具只能使用 32 位数据提供程序连接到 OLEDB 或 ODBC 数据库。 其中包括 Microsoft Access 32 位 OLEDB 数据提供程序以及其他第三方 32 位提供程序。
>
>如果使用 Visual Studio 2022 连接到数据库，则需要注意 Visual Studio 2022 是 64 位进程。 这意味着，Visual Studio 中的某些数据工具将无法使用 32 位数据提供程序连接到 OLEDB 或 ODBC 数据库。
>
>如果需要维护连接到 OLEDB 或 ODBC 数据库的 32 位应用程序，仍可以使用 Visual Studio 2022 生成并运行该应用程序。 但是，如果需要使用任何 Visual Studio 数据工具（如服务器资源管理器、数据源向导或数据集设计器），则需要使用仍为 32 位进程的 Visual Studio 的早期版本。 32 位进程的 Visual Studio 的上一版本为 Visual Studio 2019。
>
>如果计划将项目转换为 64 位进程，则建议使用 64 位 Microsoft Access 数据库引擎，也称为访问连接引擎 (ACE)。 有关详细信息，请参阅[仅适用于 Jet 和 ODBC 驱动程序的 OLE DB 提供程序为 32 位版本](/office/troubleshoot/access/jet-odbc-driver-available-32-bit-version)。

::: moniker-end

### <a name="data-modeling"></a>数据建模

在 .NET 中，从数据源检索数据后，你有三种选择来根据内存中的数据进行建模和操作：

[实体框架](../data-tools/entity-data-model-tools-in-visual-studio.md) 首选的 Microsoft ORM 技术。 可以使用它来根据关系数据编程，作为第一类 .NET 对象。 对于新应用程序，它应该是需要模型时的默认首选项。 它需要底层 ADO.NET 提供程序的自定义支持。

[LINQ to SQL](../data-tools/linq-to-sql-tools-in-visual-studio2.md) 早期版本的对象关系映射器。 它适用于不太复杂的方案，但不再处于积极开发状态。

[数据集](../data-tools/dataset-tools-in-visual-studio.md) 这三种建模技术中最早使用的一种。 它主要设计用于快速开发“数据表单”应用程序，在这些应用程序中，你不需要处理大量数据或执行复杂的查询或转换。 DataSet 对象由 DataTable 和 DataRow 对象组成，它们在逻辑上与 SQL 数据库对象的相似程度远远超过 .NET 对象。 对于基于 SQL 数据源的相对简单的应用程序，数据集可能仍是一个不错的选择。

不需要使用其中的任何一种技术。 在某些情况下，尤其是在性能至关重要的情况下，只需使用 DataReader 对象从数据库中读取数据，并将需要的值复制到集合对象（如 List\<T>）。

## <a name="native-c"></a>本机 C++

在大多数情况下，连接到 SQL Server 的 C++ 应用程序应使用 [Microsoft® ODBC Driver 13.1 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339)。 如果服务器已链接，则 OLE DB 是必需的，为此你要使用 [SQL Server Native Client](/sql/relational-databases/native-client/sql-server-native-client)。 可以直接使用 [ODBC](/sql/odbc/microsoft-open-database-connectivity-odbc?view=sql-server-2017&preserve-view=true) 或 OLE DB 驱动程序来访问其他数据库。 ODBC 是当前的标准数据库接口，但大多数数据库系统都提供无法通过 ODBC 接口访问的自定义功能。 OLE DB 是一种旧的 COM 数据访问技术，虽然仍受支持，但不建议用于新的应用程序。 有关详细信息，请参阅 [Visual C++ 中的数据访问](/cpp/data/data-access-in-cpp)。

使用 REST 服务的 C++ 程序可以使用 [C++ REST SDK](https://github.com/Microsoft/cpprestsdk)。

使用 Microsoft Azure 存储的 C++ 程序可以使用 [Microsoft Azure 存储客户端](https://www.nuget.org/packages/Microsoft.Azure.Storage.CPP)。

数据建模&mdash;Visual Studio 不提供适用于 C++ 的 ORM 层。 [ODB](https://www.codesynthesis.com/products/odb/) 是一种适用于 C++ 的常用开源 ORM。

若要详细了解如何从 C++ 应用连接到数据库，请参阅[适用于 C++ 的 Visual Studio 数据工具](../data-tools/visual-studio-data-tools-for-cpp.md)。 有关旧 Visual C++ 数据访问技术的详细信息，请参阅[数据访问](/cpp/data/data-access-in-cpp)。

## <a name="javascript"></a>JavaScript

[Visual Studio 中的 JavaScript](/scripting/javascript/javascript-language-reference) 是一种用于构建跨平台应用、UWP 应用、云服务、网站和 Web 应用的一等语言。 你可以使用 Visual Studio 中的 Bower、Grunt、Gulp、npm 和 NuGet 来安装你最喜爱的 JavaScript 库和数据库产品。 通过从 [Azure 网站](https://azure.microsoft.com/)下载 SDK 连接到 Azure 存储和服务。 Edge.js 是将服务器端 JavaScript (Node.js) 连接到 ADO.NET 数据源的库。

## <a name="python"></a>Python

[在 Visual Studio 中安装 Python 支持](../python/overview-of-python-tools-for-visual-studio.md)，以创建 Python 应用程序。 Azure 文档包含几个有关连接到数据的教程，包括以下内容：

- [Azure 上的 Django 和 SQL 数据库](/azure/app-service/app-service-web-get-started-python)
- [Azure 上的 Django 和 MySQL](/azure/app-service-web/web-sites-python-ptvs-django-mysql)
- 处理 [Blob](/azure/storage/blobs/storage-quickstart-blobs-python)、[文件](/azure/storage/files/storage-python-how-to-use-file-storage)、[队列](/azure/storage/queues/storage-python-how-to-use-queue-storage)和[表 (Cosmo DB)](/azure/cosmos-db/table-storage-how-to-use-python)。

## <a name="related-topics"></a>相关主题

[Microsoft AI 平台](https://azure.microsoft.com/overview/ai-platform/?v=17.42w)&mdash;介绍了 Microsoft 智能云，包括 Cortana 分析套件和对物联网的支持。

[Microsoft Azure 存储](/azure/storage/)&mdash;描述了 Azure 存储，并介绍如何使用 Azure Blob、表、队列和文件来创建应用程序。

[Azure SQL 数据库](/azure/sql-database/)&mdash;描述了如何连接到作为服务的关系数据库，即 Azure SQL 数据库。

[SQL Server Data Tools](/sql/ssdt/download-sql-server-data-tools-ssdt)&mdash;描述了简化数据连接的应用程序和数据库的设计、探索、测试和部署的工具。

[ADO.NET](/dotnet/framework/data/adonet/index)&mdash;描述了 ADO.NET 体系结构，并介绍如何使用 ADO.NET 类管理应用程序数据并与数据源和 XML 进行交互。

[ADO.NET Entity Framework](/ef/ef6/)&mdash;描述了如何创建允许开发人员根据概念模型而不是直接根据关系数据库进行编程的数据应用程序。

[WCF Data Services 4.5](/dotnet/framework/data/wcf/index)&mdash;描述了如何使用 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 在实现 [Open Data Protocol (OData)](https://www.odata.org/) 的 Web 或 Intranet 上部署数据服务。

[Office 解决方案中的数据](../vsto/data-in-office-solutions.md)&mdash;包含指向一些主题的链接，这些主题说明如何在 Office 解决方案中处理数据。 其中包括有关面向架构的编程、数据缓存和服务器端数据访问的信息。

[LINQ（语言集成查询）](/dotnet/csharp/linq/)&mdash;描述了 C# 和 Visual Basic 中内置的查询功能，以及用于查询关系数据库、XML 文档、数据集和内存中集合的通用模型。

[Visual Studio 中的 XML 工具](../xml-tools/xml-tools-in-visual-studio.md)&mdash;讨论了如何使用 XML 数据、调试 XSLT、.NET XML 功能和 XML 查询体系结构。

[XML 文档和数据](/dotnet/standard/data/xml/index)&mdash;概述了在 .NET 中处理 XML 文档和数据的一组全面、集成的类。
