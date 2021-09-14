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
ms.openlocfilehash: 0348a3ba4db339e7472fc3ff72b09fe8cc23135e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601236"
---
# <a name="add-new-connections"></a>添加新连接

可以使用 服务器资源管理器、Cloud Explorer 或 SQL Server 对象资源管理器 来测试与数据库或服务的连接，并浏览 **SQL Server 对象资源管理器。**   这些窗口的功能在一定程度上重叠。 基本区别包括：

- 服务器资源管理器

   默认安装在 Visual Studio。 可用于测试连接和查看SQL Server数据库、安装了 ADO.NET 提供程序的其他任何数据库以及某些 Azure 服务。 还显示低级别对象，例如系统性能计数器、事件日志和消息队列。 如果数据源没有 ADO.NET 提供程序，则它不会显示在此处，但你仍可以通过以编程方式连接Visual Studio数据源。

- 云资源管理器

   从市场 手动安装此Visual Studio扩展Visual Studio[扩展](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.CloudExplorerForVS)。 提供用于浏览和连接到 Azure 服务的专用功能。

- SQL Server 对象资源管理器

   随 SQL Server Data Tools一起安装，在"视图"菜单 **下** 可见。 如果看不到它，请转到 控制面板 中的"程序和功能"，找到"Visual Studio"，然后选择"更改"，在选中"SQL Server Data Tools"复选框后重新运行安装程序。 使用 **SQL Server 对象资源管理器** 查看 SQL (（如果它们具有 ADO.NET 提供程序) 、创建新数据库、修改架构、创建存储过程、检索连接字符串、查看数据等）。 SQL未安装 ADO.NET 数据库不会在此处显示，但你仍然可以以编程方式连接到它们。

## <a name="add-a-connection-in-server-explorer"></a>在 服务器资源管理器

若要创建与数据库的连接，请单击"连接"节点 **服务器资源管理器"连接**"图标，或右键单击"数据服务器资源管理器节点上的"连接"，然后选择"添加 **连接"。** 在此处，还可以连接到另一台服务器、SharePoint或 Azure 服务上的数据库。

![服务器资源管理器"新建连接"图标](../data-tools/media/raddata-server-explorer-new-connection-icon.png)

此时会打开" **添加连接"** 对话框。 此处，我们输入了实例SQL Server LocalDB的名称。

![添加新连接](../data-tools/media/raddata-add-new-connection-dialog.png)

## <a name="change-the-provider"></a>更改提供程序

如果数据源不是你需要的，请单击"更改"按钮以选择新的数据源和/或新的 ADO.NET 提供程序。 新提供程序可能会要求提供凭据，具体取决于你的配置方式。

![更改 AD0.NET 提供程序](../data-tools/media/raddata-change-ad0.net-data-provider.png)

## <a name="test-the-connection"></a>测试连接

选择数据源后，单击"测试 **连接"。** 如果不成功，则需要根据供应商的文档进行故障排除。

![测试连接](../data-tools/media/raddata-test-connection.png)

如果测试成功，你已准备好创建数据源 ，这是一个Visual Studio，它实际上意味着基于基础数据库或服务的数据模型。 

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
