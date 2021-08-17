---
title: 升级 .mdf 文件
description: 在安装较新版本的 (.mdf) 后，查看用于升级数据库文件 Visual Studio。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122031570"
---
# <a name="upgrade-mdf-files"></a>升级 .mdf 文件

本主题介绍在安装较新版本的 (*.mdf*) 升级数据库文件Visual Studio。 它包括以下任务的说明：

- 升级数据库文件以使用较新版本SQL Server Express LocalDB

- 升级数据库文件以使用较新版本SQL Server Express

- 在 Visual Studio 中处理数据库文件，但保留与旧版本的 SQL Server Express 或 LocalDB

- 将SQL Server Express作为默认数据库引擎

可以使用 Visual Studio 打开包含数据库文件 (*.mdf*) 的项目，该文件是使用较旧版本的 SQL Server Express 或 LocalDB 创建的。 但是，若要在 Visual Studio 中继续开发项目，必须在与 Visual Studio 相同的计算机上安装该 SQL Server Express 或 LocalDB 版本，或者必须升级数据库文件。 如果升级数据库文件，则你将无法通过使用旧版本的 SQL Server Express 或 LocalDB。

如果该文件的版本与当前安装的 SQL Server Express 或 LocalDB 实例不兼容，则系统可能会提示你升级通过早期版本的 SQL Server Express 或 LocalDB 创建的数据库文件。 若要解决此问题，Visual Studio提示你升级文件。

> [!IMPORTANT]
> 建议在升级数据库文件之前备份它。

> [!WARNING]
> 如果将在 LocalDB 2014 (V12) 32 位中创建的 *.mdf* 文件升级到 LocalDB 2016 (V13) 或更高版本，将无法在 LocalDB 的 32 位版本中再次打开该文件。

升级数据库之前，请考虑以下条件：

- 如果要在较旧版本和较新版本的 Visual Studio 中处理项目，请不要Visual Studio。

- 如果应用程序将用于使用 SQL Server Express 而不是 LocalDB。

- 如果应用程序使用远程连接，请不要升级，LocalDB不接受远程连接。

- 如果应用程序依赖于 IIS Internet Information Services (，请不要) 。

- 如果要在沙盒环境中测试数据库应用程序，但不想管理数据库，请考虑升级。

### <a name="to-upgrade-a-database-file-to-use-the-localdb-version"></a>升级数据库文件以使用LocalDB版本

1. 在 **服务器资源管理器** 中，选择 **"连接数据库"** 按钮。

2. 在 **"添加连接** "对话框中，指定以下信息：

    - **数据源**： `Microsoft SQL Server (SqlClient)`

    - **服务器名称**：

        - 使用默认版本 `(localdb)\MSSQLLocalDB` ：。  这将指定 ProjectV12 或 ProjectV13，具体取决于安装Visual Studio版本以及创建第一LocalDB实例。 中的 **MSSQLLocalDB** **SQL Server 对象资源管理器** 显示它指向的版本。

        - 若要使用特定版本：或 ，其中 `(localdb)\ProjectsV12` `(localdb)\ProjectsV13` V12 LocalDB 2014，V13 为 2016 LocalDB版本。

    - **附加数据库文件**：主 *.mdf* 文件的物理路径。

    - **逻辑名称**： 你想要使用该文件的名称。

3. 选择“确定”按钮。

4. 系统提示时，选择"是 **"** 按钮升级文件。

    数据库已升级，已LocalDB数据库引擎，并且不再与较旧版本的 LocalDB。

还可通过打开SQL Server Express菜单，然后选择"修改连接LocalDB来修改连接以 **使用连接**。 在" **修改连接** "对话框中，将服务器名称更改为 `(LocalDB)\MSSQLLocalDB` 。 在"**高级属性**"对话框中，确保"**用户实例**"设置为 **"False"。**

### <a name="to-upgrade-a-database-file-to-use-the-sql-server-express-version"></a>升级数据库文件以使用SQL Server Express版本

1. 在数据库连接的快捷菜单上，选择"修改 **连接"。**

2. 在" **修改连接** "对话框中，选择"高级 **"** 按钮。

3. 在" **高级属性"** 对话框中，选择" **确定"** 按钮而不更改服务器名称。

    升级数据库文件以匹配当前版本的SQL Server Express。

### <a name="to-work-with-the-database-in-visual-studio-but-retain-compatibility-with-sql-server-express"></a>若要使用数据库中的数据库Visual Studio但保持与数据库SQL Server Express

- 在Visual Studio中，打开项目而不升级它。

  - 若要运行项目，请选择 **F5** 键。

  - 若要编辑数据库，请打开 解决方案资源管理器 中的 *.mdf* 文件，然后展开 服务器资源管理器 **中的** 节点以使用数据库。 

### <a name="to-make-sql-server-express-the-default-database-engine"></a>若要SQL Server Express默认数据库引擎

1. 在菜单栏上，选择“工具” > “选项”。

2. 在"**选项"** 对话框中，展开"**数据库工具"** 选项，然后选择"数据 **连接"。**

3. 在 **"SQL Server实例** 名称"文本框中，指定SQL Server Express或LocalDB实例的名称。 如果实例未命名，请指定 `.\SQLEXPRESS or (LocalDB)\MSSQLLocalDB` 。

4. 选择“确定”按钮。

    SQL Server Express将成为应用程序的默认数据库引擎。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](accessing-data-in-visual-studio.md)
