---
title: 添加新连接
description: 在数据库或Visual Studio中添加连接，并浏览数据库内容和架构，使用 服务器资源管理器 或 SQL Server 对象资源管理器。
ms.custom: SEO-VS-2020
ms.date: 03/21/2022
ms.topic: how-to
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: d819240c934692046b9a28b2a5b68009d7bb91ee
ms.sourcegitcommit: 1ed233bb3afc5ae1f52aff8e41f7e650342033ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2022
ms.locfileid: "141275490"
---
# <a name="add-new-connections"></a>添加新连接

本文中的步骤介绍了如何连接到 IDE Visual Studio数据库。 可以使用这些步骤直接处理数据，例如执行查询、编辑数据、创建和编辑表和其他架构属性、编辑存储过程和函数、触发器等。 这些函数独立于你使用的编程语言或 .NET 版本。

:::moniker range="<=vs-2019"
通过使用服务器资源管理器、Cloud Explorer 或 SQL Server 对象资源管理器，可以测试对数据库或服务的连接，还可以浏览数据库内容和架构。   这些窗口的功能在一种程度上会重叠。 基本区别包括：

- 服务器资源管理器

   默认安装在 Visual Studio 中。 可以用来测试连接，查看 SQL Server 数据库、安装了 ADO.NET 提供程序的其他数据库以及一些 Azure 服务。 还显示低级对象，例如系统性能计数器、事件日志和消息队列。 如果数据源没有 ADO.NET 提供程序，则不会显示在此处，但仍可以通过以编程方式连接来从 Visual Studio 使用它。

- Cloud Explorer

   手动安装此窗口作为 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.CloudExplorerForVS) 的 Visual Studio 扩展。 提供用于浏览和连接到 Azure 服务的专用功能。

- SQL Server 对象资源管理器

   与 SQL Server Data Tools 一起安装，并可在“视图”菜单中显示。 如果在此处没有看到安装程序，则在选中 SQL Server Data Tools 的复选框后，转到“控制面板”中的“程序和功能”，找到 Visual Studio，然后选择“更改”以重新运行安装程序。  使用 SQL Server 对象资源管理器查看 SQL 数据库（如果它们具有 ADO.NET 提供程序）、创建新的数据库、修改架构、创建存储过程、检索连接字符串、查看数据等。 未安装 ADO.NET 提供程序的 SQL 数据库不会显示在此处，但是仍可以编程方式连接到这些数据库。
::: moniker-end
:::moniker range=">=vs-2022"
可以使用数据库或服务来测试与数据库或服务的连接，并浏览数据库 **内容和****服务器资源管理器** SQL Server 对象资源管理器。 这些窗口的功能在一种程度上会重叠。 基本区别包括：

- 服务器资源管理器

   默认安装在 Visual Studio 中。 可以用来测试连接，查看 SQL Server 数据库、安装了 ADO.NET 提供程序的其他数据库以及一些 Azure 服务。 还显示低级对象，例如系统性能计数器、事件日志和消息队列。 如果数据源没有 ADO.NET 提供程序，则不会显示在此处，但仍可以通过以编程方式连接来从 Visual Studio 使用它。

- SQL Server 对象资源管理器

   与 SQL Server Data Tools 一起安装，并可在“视图”菜单中显示。 如果在此处没有看到安装程序，则在选中 SQL Server Data Tools 的复选框后，转到“控制面板”中的“程序和功能”，找到 Visual Studio，然后选择“更改”以重新运行安装程序。  使用 SQL Server 对象资源管理器查看 SQL 数据库（如果它们具有 ADO.NET 提供程序）、创建新的数据库、修改架构、创建存储过程、检索连接字符串、查看数据等。 未安装 ADO.NET 提供程序的 SQL 数据库不会显示在此处，但是仍可以编程方式连接到这些数据库。
::: moniker-end

## <a name="add-a-connection-in-server-explorer"></a>在服务器资源管理器中添加连接

若要创建与数据库的连接，请单击“服务器资源管理器”中的“添加连接”图标，或右键单击“数据连接”节点上的“服务器资源管理器”，然后选择“添加连接”。     在此处，还可以连接到其他服务器上的数据库、SharePoint 服务或 Azure 服务。

:::moniker range="<=vs-2019"
![显示"新建服务器资源管理器图标的屏幕截图。](../data-tools/media/server-explorer-new-connection-icon.png)
:::moniker-end
:::moniker range=">=vs-2022"
![显示"服务器资源管理器 连接数据库"图标的屏幕截图。](./media/vs-2022/connect-to-database-server-explorer.png)
:::moniker-end

这将打开“添加连接”对话框。 此处，我们输入了 SQL Server LocalDB 实例的名称`(localdb)\MSSqlLocalDB`，该实例通常随 Visual Studio 一起安装。

:::moniker range="<=vs-2019"
!["添加新连接"对话框的屏幕截图。](../data-tools/media/add-new-connection-dialog.png)
:::moniker-end
:::moniker range=">=vs-2022"
!["添加新连接"对话框的屏幕截图。](./media/vs-2022/add-new-connection.png)
:::moniker-end

如果无法访问另一个数据库，并且未看到安装 LocalDB，则可以通过 Visual Studio 安装程序 安装 LocalDB，作为"数据 存储 和处理"工作负载、**ASP.NET 和 Web** 开发工作负载的一部分，或者作为单个组件安装。 请参阅[修改 Visual Studio](../install/modify-visual-studio.md)。

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

:::moniker range="<=vs-2019"
![显示如何更改数据提供程序 ADO.NET 屏幕截图。](../data-tools/media/change-ado-net-data-provider.png)
:::moniker-end
:::moniker range=">=vs-2022"
![显示如何更改数据提供程序 ADO.NET 屏幕截图。](../data-tools/media/vs-2022/change-data-source-2.png)
:::moniker-end

## <a name="test-the-connection"></a>测试连接

选择数据源后，单击“测试连接”。 如果测试未成功，将需要根据供应商的文档进行故障排除。

:::moniker range="<=vs-2019"
![显示"测试连接成功"消息框的屏幕截图。](../data-tools/media/test-connection.png)
:::moniker-end
:::moniker range=">=vs-2022"
![显示"测试连接成功"消息框的屏幕截图。](./media/vs-2022/test-connection-succeeded.png)
:::moniker-end

如果测试成功，则可以创建数据源，它是一个表示基于基础数据库或服务的数据模型的 Visual Studio 术语。

:::moniker range=">=vs-2022"

## <a name="connect-using-sql-server-object-explorer"></a>连接 SQL Server 对象资源管理器

如果使用 SQL Server 对象资源管理器，则体验可能更简单，该对话框提供了一个对话框，该对话框在本地、本地网络和 Azure 订阅中查找可用的数据库提供了更多帮助，并提供了最近使用的选项的历史记录。

若要从 SQL Server 对象资源管理器 访问连接 **对话框**，请单击工具栏按钮"添加 **SQL Server**" 。

!["添加SQL Server 对象资源管理器"按钮SQL Server屏幕截图](./media/vs-2022/sql-server-object-explorer-add-sql-server-button.png)

将出现"连接"对话框。 选择本地、网络或Azure SQL服务器，选择数据库，提供凭据，然后选择 **连接。**

![对话框的SQL Server 对象资源管理器 连接屏幕截图。](./media/vs-2022/sql-server-object-explorer-connect-dialog.png)

如果需要在连接字符串中设置其他设置，可以使用"高级"链接，其中显示所有设置。

![显示"高级设置"的屏幕截图。](./media/vs-2022/sql-connect-advanced-options.png)

设置完连接后，服务器和数据库将显示在"SQL Server 对象资源管理器窗口中。

![显示"已成功连接"消息的屏幕截图。](./media/vs-2022/successfully-added-connection.png)

在这里，你可以浏览数据库、编写和执行查询、编辑数据、存储过程和函数，以及直接在Visual Studio。

:::moniker-end

## <a name="next-steps"></a>后续步骤

如果使用 .NET Framework (而不是 .NET Core 或 .NET 5 或更高版本) 以及 Windows 窗体 或 WPF，可以使用"数据源"窗口，例如，若要为 Windows 窗体 和 WPF 应用程序中的控件设置数据绑定，[请参阅添加新数据源](add-new-data-sources.md)。 这些工具旨在让你快速创建Windows用户需要输入、显示和操作数据的应用程序。

如果使用 .NET 5 或更高版本、.NET Core 或 ASP.NET Core，可以使用 [连接的服务。](../azure/overview-connected-services.md) 使用 连接的服务，可以轻松使用由 SQL LocalDB 托管的本地开发数据库、在容器中运行的 SQL Server 或 SQL Server 的本地实例，然后在准备好部署到云时转换到 Azure SQL 数据库。 对于 .NET 5 或更高版本、.NET Core ASP.NET Core，应考虑使用 [Entity Framework Core 作为数据库](/ef/core)框架。

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
