---
title: 添加新连接
description: 在数据库或Visual Studio中添加连接，并浏览数据库内容和架构，使用 服务器资源管理器、Cloud Explorer 或 SQL Server 对象资源管理器。
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

可以使用 服务器资源管理器、Cloud Explorer 或 来测试与数据库或服务的连接，并浏览SQL Server 对象资源管理器 **和SQL Server 对象资源管理器。**   这些窗口的功能在一定程度上重叠。 基本区别包括：

- 服务器资源管理器

   默认安装在 Visual Studio。 可用于测试连接和查看SQL Server数据库、安装了 ADO.NET 提供程序的其他任何数据库以及某些 Azure 服务。 还显示低级别对象，例如系统性能计数器、事件日志和消息队列。 如果数据源没有 ADO.NET 提供程序，则它不会显示在此处，但你仍可以通过以编程方式连接Visual Studio数据源。

- Cloud Explorer

   手动安装此窗口作为 Visual Studio Marketplace [Visual Studio扩展](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.CloudExplorerForVS)。 提供用于浏览和连接到 Azure 服务的专用功能。

- SQL Server 对象资源管理器

   随 SQL Server Data Tools一起安装，在"视图"菜单 **下可见**。 如果看不到它，请转到 控制面板 中的"程序和功能"，找到"Visual Studio"，然后选择"更改"，在选中"SQL Server Data Tools"复选框后重新运行安装程序。 使用 **SQL Server 对象资源管理器** 查看 SQL 数据库 (如果它们具有 ADO.NET 提供程序) 、创建新数据库、修改架构、创建存储过程、检索连接字符串、查看数据等。 SQL未安装 ADO.NET 数据库不会在此处显示，但你仍然可以以编程方式连接到它们。

## <a name="add-a-connection-in-server-explorer"></a>在 服务器资源管理器

若要创建与数据库的连接，请单击 "添加连接" 服务器资源管理器 **，或** 右键单击 "数据连接" 节点上的 服务器资源管理器 **并选择**"添加 **连接"。** 在此处，还可以连接到另一台服务器、SharePoint服务或 Azure 服务上的数据库。

![服务器资源管理器"新建连接"图标](../data-tools/media/raddata-server-explorer-new-connection-icon.png)

此时会打开" **添加连接"** 对话框。 此处，我们输入了实例SQL Server LocalDB的名称。

![添加新连接](../data-tools/media/raddata-add-new-connection-dialog.png)

## <a name="change-the-provider"></a>更改提供程序

如果数据源不是你需要的，请单击"更改"按钮以选择新的数据源和/或新的 ADO.NET 提供程序。 新提供程序可能会要求提供凭据，具体取决于你的配置方式。

::: moniker range=">=vs-2022"
> [!NOTE]
> 如果使用 Visual Studio 2022 连接到 OLEDB 或 ODBC 数据提供程序，则需要注意，Visual Studio 2022 现在是一个 64 位进程。
>
> 这意味着，Visual Studio中的某些数据工具将不能使用 32 位数据提供程序连接到 OLEDB 或 ODBC 数据库。 这包括 Microsoft Access 32 位 OLEDB 数据提供程序以及其他第三方 32 位提供程序。
>
>如果需要维护连接到 OLEDB 或 ODBC 的 32 位应用程序，仍可使用 Visual Studio 2022 生成和运行应用程序。 但是，如果需要使用任何 Visual Studio Data Tools（如 服务器资源管理器、数据源向导或数据集设计器），则需要使用早期版本的 Visual Studio，该版本仍为 32 位进程。 2019 Visual Studio 32 位进程的最后一Visual Studio版本。
>
>如果计划将项目转换为 64 位进程，则需要更新 OLEDB 和 ODBC 数据连接以使用 64 位数据访问接口。
>
>如果应用程序使用 Microsoft Access 数据库，并且可以将项目转换为 64 位，则建议使用 64 位 Microsoft Access 数据库引擎，也称为访问连接引擎 (ACE) 。 有关详细信息OLE DB，请参阅适用于 Jet 和 ODBC 驱动程序的提供程序是 [32](/office/troubleshoot/access/jet-odbc-driver-available-32-bit-version) 位版本。
>
>如果使用的是第三方数据访问接口，建议在将项目转换为 64 位之前，与供应商联系，看其是否提供 64 位提供程序。

::: moniker-end

![更改 AD0.NET 提供程序](../data-tools/media/raddata-change-ad0.net-data-provider.png)

## <a name="test-the-connection"></a>测试连接

选择数据源后，单击"测试 **连接"。** 如果不成功，则需要根据供应商的文档进行故障排除。

![测试连接](../data-tools/media/raddata-test-connection.png)

如果测试成功，你已准备好创建数据源 ，这是一个Visual Studio，它实际上意味着基于基础数据库或服务的数据模型。 

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
