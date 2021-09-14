---
title: 升级 .mdf 文件
description: 查看在安装了较新版本的 Visual Studio 后升级数据库文件 ( .mdf) 的选项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- SQL Server Express
- SQL Server LocalDB
- LocalDB
- SQLEXPRESS
- upgrading SQLExpress to SQLExpress
- upgrading to LocalDB
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 8a84ef3c52092feab447dfb26110129f89b1a766
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601067"
---
# <a name="upgrade-mdf-files"></a>升级 .mdf 文件

本主题介绍在安装了较新版本的 Visual Studio 后用于升级数据库文件 (*.mdf*) 的选项。 其中包括以下任务的说明：

- 升级数据库文件以使用较新版本的 SQL Server Express LocalDB

- 升级数据库文件以使用较新版本的 SQL Server Express

- 使用 Visual Studio 中的数据库文件，但保留与较旧版本 SQL Server Express 或 LocalDB 的兼容性

- 使 SQL Server Express 成为默认数据库引擎

您可以使用 Visual Studio 来打开一个项目，该项目包含通过使用旧版本的 SQL Server Express 或 LocalDB 创建的 (*.mdf*) 的数据库文件。 但是，若要继续开发 Visual Studio 中的项目，你必须将该版本的 SQL Server Express 或 LocalDB 与 Visual Studio 安装在同一台计算机上，或者必须升级数据库文件。 如果升级数据库文件，将无法使用旧版本的 SQL Server Express 或 LocalDB 来访问该文件。

还可能会提示你升级通过早期版本的 SQL Server Express 创建的数据库文件，如果该文件的版本与当前安装的 SQL Server Express 或 LocalDB 实例不兼容，则为 LocalDB。 若要解决此问题，Visual Studio 会提示你升级该文件。

> [!IMPORTANT]
> 建议在升级数据库文件之前对其进行备份。

> [!WARNING]
> 如果将在 LocalDB 2014 (V12) 32 位中创建的 *.mdf* 文件升级到 LocalDB 2016 (V13) 或更高版本，则将无法在 LocalDB 的32位版本中再次打开该文件。

升级数据库之前，请考虑以下条件：

- 如果要在较旧版本和较新版本的 Visual Studio 中处理项目，请不要升级。

- 如果你的应用程序将用于使用 SQL Server Express 而不是 LocalDB 的环境中，请不要升级。

- 如果你的应用程序使用远程连接，请不要升级，因为 LocalDB 不接受它们。

- 如果你的应用程序依赖于 Internet Information Services (IIS) ，请不要升级。

- 如果要在沙盒环境中测试数据库应用程序，但不想管理数据库，请考虑进行升级。

### <a name="to-upgrade-a-database-file-to-use-the-localdb-version"></a>升级数据库文件以使用 LocalDB 版本

1. 在 **服务器资源管理器** 中，选择 "**连接到数据库**" 按钮。

2. 在 " **添加连接** " 对话框中，指定下列信息：

    - **数据源**： `Microsoft SQL Server (SqlClient)`

    - **服务器名称**：

        - 使用默认版本： `(localdb)\MSSQLLocalDB` 。  这将指定 ProjectV12 或 ProjectV13，具体取决于安装的 Visual Studio 版本以及第一个 LocalDB 实例的创建时间。 **SQL Server 对象资源管理器** 中的 **MSSQLLocalDB** 节点显示了它指向的版本。

        - 若要使用特定版本 `(localdb)\ProjectsV12` `(localdb)\ProjectsV13` ，请使用或，其中 V12 为 LocalDB 2014，V13 为 LocalDB 2016。

    - **附加数据库文件**：主 *.mdf* 文件的物理路径。

    - **逻辑名称**： 你想要使用该文件的名称。

3. 选择“确定”按钮。

4. 出现提示时，请选择 " **是"** 按钮来升级文件。

    数据库已升级，连接到 LocalDB 数据库引擎，不再与早期版本的 LocalDB 兼容。

还可以通过打开连接的快捷菜单，然后选择 "**修改连接**" 来修改 SQL Server Express 连接以使用 LocalDB。 在 " **修改连接** " 对话框中，将服务器名称更改为 `(LocalDB)\MSSQLLocalDB` 。 在 " **高级属性** " 对话框中，确保 " **用户实例** " 设置为 " **False**"。

### <a name="to-upgrade-a-database-file-to-use-the-sql-server-express-version"></a>升级数据库文件以使用 SQL Server Express 版本

1. 在连接到数据库的快捷菜单上，选择 " **修改连接**"。

2. 在 " **修改连接** " 对话框中，选择 " **高级** " 按钮。

3. 在 " **高级属性** " 对话框中，选择 " **确定"** 按钮，而不会更改服务器名称。

    数据库文件已升级，以匹配 SQL Server Express 的当前版本。

### <a name="to-work-with-the-database-in-visual-studio-but-retain-compatibility-with-sql-server-express"></a>在 Visual Studio 中使用数据库但保持与 SQL Server Express 的兼容性

- 在 Visual Studio 中，打开项目但不进行升级。

  - 若要运行项目，请选择 **F5** 键。

  - 若要编辑数据库，请在 **解决方案资源管理器** 中打开 *.mdf* 文件，然后展开 **服务器资源管理器** 中的节点以使用您的数据库。

### <a name="to-make-sql-server-express-the-default-database-engine"></a>使 SQL Server Express 默认的数据库引擎

1. 在菜单栏上，选择“工具” > “选项”。

2. 在 " **选项** " 对话框中，展开 " **数据库工具** " 选项，然后选择 " **数据连接**"。

3. 在 " **SQL Server 实例名称**" 文本框中，指定要使用 SQL Server Express 或 LocalDB 实例的名称。 如果该实例未命名，则指定 `.\SQLEXPRESS or (LocalDB)\MSSQLLocalDB` 。

4. 选择“确定”按钮。

    SQL Server Express 将是应用程序的默认数据库引擎。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](accessing-data-in-visual-studio.md)
