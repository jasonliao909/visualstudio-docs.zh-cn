---
title: 添加新连接
description: 使用服务器资源管理器、Cloud Explorer 或 SQL Server 对象资源管理器，在 Visual Studio 中将连接添加到 DB 或服务并浏览 DB 内容和架构。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 6a5e6ea72056fcb7e4a7b4ca15750aa57dea7bf1
ms.sourcegitcommit: 3cfe24a74b611440b831d9591e067874c51a3bfb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2021
ms.locfileid: "130087483"
---
# <a name="add-new-connections"></a>添加新连接

通过使用服务器资源管理器、Cloud Explorer 或 SQL Server 对象资源管理器，可以测试对数据库或服务的连接，还可以浏览数据库内容和架构。   这些窗口的功能在一种程度上会重叠。 基本区别包括：

- 服务器资源管理器

   默认安装在 Visual Studio 中。 可以用来测试连接，查看 SQL Server 数据库、安装了 ADO.NET 提供程序的其他数据库以及一些 Azure 服务。 还显示低级对象，例如系统性能计数器、事件日志和消息队列。 如果数据源没有 ADO.NET 提供程序，则不会显示在此处，但仍可以通过以编程方式连接来从 Visual Studio 使用它。

- Cloud Explorer

   手动安装此窗口作为 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.CloudExplorerForVS) 的 Visual Studio 扩展。 提供用于浏览和连接到 Azure 服务的专用功能。

- SQL Server 对象资源管理器

   与 SQL Server Data Tools 一起安装，并可在“视图”菜单中显示。 如果在此处没有看到安装程序，则在选中 SQL Server Data Tools 的复选框后，转到“控制面板”中的“程序和功能”，找到 Visual Studio，然后选择“更改”以重新运行安装程序。  使用 SQL Server 对象资源管理器查看 SQL 数据库（如果它们具有 ADO.NET 提供程序）、创建新的数据库、修改架构、创建存储过程、检索连接字符串、查看数据等。 未安装 ADO.NET 提供程序的 SQL 数据库不会显示在此处，但是仍可以编程方式连接到这些数据库。

## <a name="add-a-connection-in-server-explorer"></a>在服务器资源管理器中添加连接

若要创建与数据库的连接，请单击“服务器资源管理器”中的“添加连接”图标，或右键单击“数据连接”节点上的“服务器资源管理器”，然后选择“添加连接”。     在此处，还可以连接到其他服务器上的数据库、SharePoint 服务或 Azure 服务。

![服务器资源管理器“新建连接”图标](../data-tools/media/raddata-server-explorer-new-connection-icon.png)

这将打开“添加连接”对话框。 这里，我们输入了 SQL Server LocalDB 实例的名称。

![添加新连接](../data-tools/media/raddata-add-new-connection-dialog.png)

## <a name="change-the-provider"></a>更改提供程序

如果该数据源不是你需要的，请单击“更改”按钮以选择新的数据源和/或新的 ADO.NET 数据提供程序。 新的提供程序可能会要求提供凭据，具体取决于你的配置方式。

::: moniker range=">=vs-2022"
> [!NOTE]
> 如果正在使用 Visual Studio 2022 连接到 OLEDB 或 ODBC 数据提供程序，则需要注意 Visual Studio 2022 现在是 64 位进程。
>
> 这意味着，Visual Studio 中的某些数据工具将无法使用 32 位数据提供程序连接到 OLEDB 或 ODBC 数据库。 其中包括 Microsoft Access 32 位 OLEDB 数据提供程序以及其他第三方 32 位提供程序。
>
>如果需要维护连接到 OLEDB 或 ODBC 的 32 位应用程序，仍可以使用 Visual Studio 2022 生成并运行该应用程序。 但是，如果需要使用任何 Visual Studio 数据工具（如服务器资源管理器、数据源向导或数据集设计器），则需要使用仍为 32 位进程的 Visual Studio 的早期版本。 32 位进程的 Visual Studio 的上一版本为 Visual Studio 2019。
>
>如果计划将项目转换为 64 位进程，则需要更新 OLEDB 和 ODBC 数据连接才能使用 64 位数据提供程序。
>
>如果你的应用程序使用 Microsoft Access 数据库，并可以将项目转换为 64 位，则建议你使用 64 位 Microsoft Access 数据库引擎，也称为访问连接引擎 (ACE)。 有关详细信息，请参阅[仅适用于 Jet 和 ODBC 驱动程序的 OLE DB 提供程序为 32 位版本](/office/troubleshoot/access/jet-odbc-driver-available-32-bit-version)。
>
>如果你使用的是第三方数据提供程序，我们建议与你的供应商取得联系，以了解他们在将项目转换为 64 位之前是否提供了 64 位提供程序。

::: moniker-end

![更改 AD0.NET 数据提供程序](../data-tools/media/raddata-change-ad0.net-data-provider.png)

## <a name="test-the-connection"></a>测试连接

选择数据源后，单击“测试连接”。 如果测试未成功，将需要根据供应商的文档进行故障排除。

![测试连接](../data-tools/media/raddata-test-connection.png)

如果测试成功，则可以创建数据源，它是一个表示基于基础数据库或服务的数据模型的 Visual Studio 术语。

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
