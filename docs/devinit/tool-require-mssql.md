---
title: require-mssql
description: devinit 工具 require-mssql。
ms.date: 11/20/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: e39a03fe70d2e4399b758e06e9acb2e0de59ef08
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832966"
---
# <a name="require-mssql"></a>require-mssql

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们专注于为云支持的内部循环和 VDI 解决方案提供不断发展的体验，这些解决方案针对一组广泛的Visual Studio工作负载进行优化。 作为此和 `devinit` 关联工具的一部分，将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该工具用于通过 MS Microsoft SQL Server 服务器 ISO 从 安装 SQL `require-mssql` Developer Edition。 [](https://www.microsoft.com/sql-server/application-development) 使用SQL身份验证时，Windows服务器SQL连接字符串 访问 `localhost` `"Server=localhost;Integrated Security=true;"` 该服务器。

## <a name="usage"></a>使用情况

如果省略 `input` 和 属性或属性 `additionalOptions` 为空，该工具将遵循 [下面详述](#default-behavior) 的默认行为。

| 名称                                             | 类型   | 必须 | 值                                                                                   |
|--------------------------------------------------|--------|----------|-----------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                                   |
| [**输入**](#input)                              | 字符串型 | 否       | 有关详细信息 [，](#input) 请参阅下面的输入。                                                  |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 未使用。 有关详细信息 [，请参阅](#additional-options) 下面的其他选项。              |

### <a name="input"></a>输入

属性 `input` 可以是具有以下两个值之一的字符串：

| 值     | 说明                              |
|-----------|------------------------------------------|
| 安装   | 安装SQL服务器。                     |
| 卸载 | 卸载所有SQL服务器安装。 |

### <a name="additional-options"></a>附加选项

未使用。

### <a name="default-behavior"></a>默认行为

该工具的默认行为 `require-mssql` 是安装SQL服务器。

### <a name="built-in-options"></a>内置选项

该工具 `require-mssql` 设置大量安装程序命令行参数，以确保安装程序可以无头运行。 下面列出了这些参数，有关这些参数的文档可在安装文档[SQL找到](/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-ver15&preserve-view=true)。

| 名称                                                               | 说明 |
|--------------------------------------------------------------------|-------------|
| /q                                                                 |             |
| /ACTION=Install                                                    |             |
| /FEATURES=SQLEngine，LocalDB                                       |             |
| /UpdateEnabled                                                     |             |
| /UpdateSource=MU                                                   |             |
| /X86=false                                                         |             |
| /INSTANCENAME=MSSQLSERVER                                          |             |
| /INSTALLSHAREDDIR="C：\Program Files\Microsoft SQL Server"          |             |
| /INSTALLSHAREDWOWDIR="C：\Program Files (x86) \Microsoft SQL Server" |             |
| /SQLSVCINSTANTFILEINIT=True                                        |             |
| /INSTANCEDIR="C：\Program Files\Microsoft SQL Server"               |             |
| /AGTSVCACCOUNT="NT Service\SQLSERVERAGENT"                         |             |
| /AGTSVCSTARTUPTYPE=Manual                                          |             |
| /SQLSVCSTARTUPTYPE=Automatic                                       |             |
| /SQLCOLLATION="SQL_Latin1_General_CP1_CI_AS"                       |             |
| /SQLSVCACCOUNT="NT Service\MSSQLSERVER"                            |             |
| /SQLSYSADMINACCOUNTS=Administrators                                |             |
| /IACCEPTSQLSERVERLICENSETERMS                                      |             |

## <a name="example-usage"></a>用法示例
下面是如何使用 运行 `require-msssql` 的示例 `.devinit.json` 。

#### <a name="devinitjson-that-will-install-mssql"></a>将安装 MSSQL 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-mssql",
            "input": "install",
        }
    ]
}
```