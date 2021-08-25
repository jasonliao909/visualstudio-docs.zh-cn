---
description: 在服务器上未能执行存储过程 sp_enable_sql_debug。
title: 用户无法执行存储过程 sp_enable_sql_debug | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: df25fb20fcf824c09b46a13eb704015d196a2930
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122097163"
---
# <a name="error-user-could-not-execute-stored-procedure-sp_enable_sql_debug"></a>错误：用户无法执行存储过程 sp_enable_sql_debug

在服务器上未能执行存储过程 sp_enable_sql_debug。 这可能是由于：

- 连接问题。 需要有一个到服务器的稳定连接。

- 在服务器上缺少必要的权限。 若要在 SQL Server 2005 上调试，运行 Visual Studio 的帐户和用于连接 SQL Server 的帐户都必须是 sysadmin 角色的成员。 用于连接 SQL Server 的帐户要么是 Windows 用户帐户（如果您正在使用 Windows 身份验证），要么是具有用户 ID 和密码的帐户（如果您使用 SQL 身份验证）。

有关详细信息，请参阅[如何：设置 SQL Server 调试权限](/previous-versions/w1bhybwz(v=vs.100))。

## <a name="see-also"></a>请参阅

- [如何：设置 SQL Server 调试权限](/previous-versions/w1bhybwz(v=vs.100))
- [设置 SQL 调试](/previous-versions/visualstudio/visual-studio-2010/s4sszxst\(v\=vs.100\))
