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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`require-mssql` 工具用于通过 MS SQL Server ISO 安装 [Microsoft SQL Server 2019 Developer Edition](https://www.microsoft.com/sql-server/application-development)。 SQL Server 将在 `localhost` 上使用集成 Windows 身份验证提供，SQL Server 将可以通过连接字符串 `"Server=localhost;Integrated Security=true;"` 进行访问。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性省略或为空，则该工具将遵循下面详述的[默认](#default-behavior)行为。

| 名称                                             | 类型   | 必须 | 值                                                                                   |
|--------------------------------------------------|--------|----------|-----------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                                   |
| [input](#input)                              | 字符串型 | 否       | 有关详细信息，请参阅下方的 [Input](#input)。                                                  |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 未使用。 有关详细信息，请参阅下方的[其他选项](#additional-options)。              |

### <a name="input"></a>输入

`input` 属性可以是具有以下两个值之一的字符串：

| 值     | 说明                              |
|-----------|------------------------------------------|
| 安装   | 安装 SQL Server。                     |
| 卸载 | 卸载所有 SQL Server 安装。 |

### <a name="additional-options"></a>附加选项

未使用。

### <a name="default-behavior"></a>默认行为

`require-mssql` 工具的默认行为是安装 SQL Server。

### <a name="built-in-options"></a>内置选项

`require-mssql` 工具设置了多个安装程序命令行参数，以确保安装程序能够无外设运行。 下面列出了这些参数，相关文档可在 [SQL 安装文档](/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-ver15&preserve-view=true)中找到。

| 名称                                                               | 说明 |
|--------------------------------------------------------------------|-------------|
| /q                                                                 |             |
| /ACTION=Install                                                    |             |
| /FEATURES=SQLEngine, LocalDB                                       |             |
| /UpdateEnabled                                                     |             |
| /UpdateSource=MU                                                   |             |
| /X86=false                                                         |             |
| /INSTANCENAME=MSSQLSERVER                                          |             |
| /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server"          |             |
| /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" |             |
| /SQLSVCINSTANTFILEINIT=True                                        |             |
| /INSTANCEDIR="C:\Program Files\Microsoft SQL Server"               |             |
| /AGTSVCACCOUNT="NT Service\SQLSERVERAGENT"                         |             |
| /AGTSVCSTARTUPTYPE=Manual                                          |             |
| /SQLSVCSTARTUPTYPE=Automatic                                       |             |
| /SQLCOLLATION="SQL_Latin1_General_CP1_CI_AS"                       |             |
| /SQLSVCACCOUNT="NT Service\MSSQLSERVER"                            |             |
| /SQLSYSADMINACCOUNTS=Administrators                                |             |
| /IACCEPTSQLSERVERLICENSETERMS                                      |             |

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `require-msssql` 的示例。

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