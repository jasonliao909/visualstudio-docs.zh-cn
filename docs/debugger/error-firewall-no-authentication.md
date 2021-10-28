---
description: 远程计算机上的 Internet 连接防火墙未设置为允许远程调试。
title: 防火墙无身份验证 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.firewall.noauth
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
ms.openlocfilehash: 7e42a9dd2856c9bee14b480b261231932dc30236
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126737157"
---
# <a name="error-firewall-no-authentication"></a>错误：防火墙无身份验证
远程计算机上的 Internet 连接防火墙未设置为允许远程调试。 对于遇到 `No Authentication` 错误的远程调试，必须将 msvsmon.exe 添加到例外列表。 可能还需要打开某些 IPSEC 端口。

> [!NOTE]
> 远程调试器可以自动配置 Windows 防火墙。 使用除 Windows 防火墙之外的防火墙（如第三方软件防火墙或硬件防火墙）时，必须手动将防火墙配置为允许远程调试。 为此，请允许 msvsmon.exe 侦听的 TCP/IP 端口的通信。 默认情况下，这些是端口 4018 和 4019，其中 4018 在所有操作系统上使用，而 4019 仅在 Windows x64 上使用以允许调试 x86 进程。

 有关详细信息，请参阅[远程调试](../debugger/remote-debugging.md)。
