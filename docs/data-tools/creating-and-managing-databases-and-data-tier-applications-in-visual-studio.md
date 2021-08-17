---
title: 数据库项目和 DAC 项目
description: 阅读有关数据库项目和数据层应用程序 (数据) 。 使用 DB 项目创建新数据库、创建新 DDC 以及更新现有数据库和 DDC。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122052819"
---
# <a name="database-projects-and-data-tier-applications"></a>数据库项目和数据层应用程序

可以使用数据库项目创建新数据库、使用 (数据层应用程序) 以及更新现有数据库和数据层应用程序。 使用数据库项目和 DAC 项目，你可以将版本控制和项目管理技术应用于数据库开发工作，其方式与将这些技术应用于托管代码或本机代码的方式非常相同。 可以通过创建 DAC 项目、数据库项目或服务器项目，并受版本控制，来帮助开发团队管理对数据库和数据库服务器的更改。 然后，团队成员可以签出文件，在隔离的开发环境或沙盒中进行更改、生成和测试更改，然后再与团队共享这些更改。 为了帮助确保代码质量，团队可以在将更改部署到生产环境之前完成和测试过渡环境中特定版本数据库的所有更改。

有关数据层应用程序支持的数据库功能的列表，请参阅[DAC 支持SQL Server对象](/sql/relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions)。 如果在数据库中使用数据层应用程序不支持的功能，应改为使用数据库项目来管理对数据库的更改。

## <a name="common-high-level-tasks"></a>常见高级任务

| High-Level任务 | 支持内容 |
| - | - |
| **开始开发数据层应用程序：** 2008 年 8 月 (引入了数据层应用程序) DAC SQL Server的概念。 DAC 包含客户端数据库SQL Server客户端服务器或 3 层应用程序使用的支持实例对象的定义。 DAC 包括数据库对象（如表和视图）以及实例实体（如登录名）。 可以使用 Visual Studio创建 DAC 项目、生成 DAC 包文件，并将 DAC 包文件发送给数据库管理员，以部署到 SQL Server 引擎的实例。 | - [数据层应用程序](/sql/relational-databases/data-tier-applications/data-tier-applications)<br />- [SQL Server Management Studio](/sql/ssms/sql-server-management-studio-ssms) |
| **执行迭代数据库开发：** 开发人员可以签出项目的各个部分，在隔离的开发环境中更新它们。 通过使用这种类型的环境，可以测试更改，而不会影响团队的其他成员。 更改完成后，将文件重新签入到版本控制中，其他团队成员可以在其中获取更改并生成这些更改，并部署到测试服务器。 | - [Project面向的脱机数据库开发 (SQL Server Data Tools) ](/sql/ssdt/project-oriented-offline-database-development)<br />- [Transact-SQL调试器 (SQL Server Management Studio) ](/sql/ssms/scripting/transact-sql-debugger) |
| **原型制作、验证测试结果以及修改数据库脚本和对象：** 可以使用 Transact-SQL编辑器执行这些常见任务之一。 | - [查询和文本编辑器 (SQL Server Management Studio) ](/sql/ssms/scripting/query-and-text-editors-sql-server-management-studio) |

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
