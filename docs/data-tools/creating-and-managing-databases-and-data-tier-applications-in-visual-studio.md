---
title: 数据库项目和 DAC 项目
description: 了解数据库项目和数据层应用程序 (DAC)。 使用 DB 项目创建新的数据库，创建新的 DAC 并更新现有的 DB 和 DAC。
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
ms.topic: conceptual
helpviewer_keywords:
- databases, managing change
ms.assetid: 40b51f5a-d52c-44ac-8f84-037a0917af33
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 0d9ed2d258fba0e8c6e1970bc758d0285bb4276c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601178"
---
# <a name="database-projects-and-data-tier-applications"></a>数据库项目和数据层应用程序

可以使用数据库项目创建新的数据库、新的数据层应用程序 (DAC) 并更新现有数据库和数据层应用程序。 使用数据库项目和 DAC 项目，可以将版本控制和项目管理技术应用于数据库开发工作，就像将这些技术应用于托管代码或本机代码一样。 通过创建 DAC 项目、数据库项目或服务器项目并将其置于版本控制下，可以帮助开发团队管理对数据库和数据库服务器所做的更改。 然后，团队成员可以签出文件，在独立开发环境或沙盒中创建、生成和测试更改，然后再与团队共享这些更改。 为了帮助确保代码质量，团队可以先在过渡环境中完成并测试对特定版本的数据库的所有更改，然后再将这些更改部署到生产环境。

有关数据层应用程序支持的数据库功能的列表，请参阅 [DAC 对 SQL Server 对象的支持](/sql/relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions)。 如果在数据库中使用数据层应用程序不支持的功能，则应改用数据库项目来管理对数据库的更改。

## <a name="common-high-level-tasks"></a>常见的高级任务

| 高级任务 | 支持内容 |
| - | - |
| **开始开发数据层应用程序：** SQL Server 2008 引入了数据层应用程序 (DAC) 概念。 DAC 包含 SQL Server 数据库的定义，以及客户端-服务器或 3 层应用程序使用的支持实例对象。 DAC 包括数据库对象（如表和视图）以及实例实体（例如登录名）。 可以使用 Visual Studio 来创建 DAC 项目、生成 DAC 包文件并将 DAC 包文件发送给数据库管理员，以部署到 SQL Server 数据库引擎的实例上。 | - [数据层应用程序](/sql/relational-databases/data-tier-applications/data-tier-applications)<br />- [SQL Server Management Studio](/sql/ssms/sql-server-management-studio-ssms) |
| **执行迭代数据库开发：** 开发人员可以签出项目的各个部分，并在独立开发环境中对它们进行更新。 借助这种类型的环境，可以在不影响团队其他成员的情况下测试所做的更改。 更改完成后，可将文件签回版本控制中，其他团队成员可在其中获取所做的更改，并将它们生成并部署到测试服务器。 | - [面向项目的脱机数据库开发 (SQL Server Data Tools)](/sql/ssdt/project-oriented-offline-database-development)<br />- [Transact-SQL 调试器 (SQL Server Management Studio)](/sql/ssms/scripting/transact-sql-debugger) |
| **制作原型、验证测试结果并修改数据库脚本和对象：** 可使用 Transact SQL 编辑器执行这些常见任务的任何一项。 | - [查询和文本编辑器 (SQL Server Management Studio)](/sql/ssms/scripting/query-and-text-editors-sql-server-management-studio) |

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
