---
title: 源服务器安全警报 | Microsoft Docs
description: 了解 Visual Studio 调试器中的源服务器安全警报警告。 使用源服务器时，请注意潜在的安全威胁。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.sourceserver.enablewarning
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 8451c281-6914-469c-b80c-6271cc3f3d17
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 567440c7395982fb3894c783790eee12c9056abc
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126642230"
---
# <a name="source-server-security-alert"></a>源服务器安全警报
使用源服务器时，只能使用来自已知和受信任位置的符号文件。

 此警告会在你启用源服务器支持时出现。 源服务器命令嵌套在调试符号文件（\*.pdb 文件）中。 请确保你知道自己的 PDB 文件来自何处。

> [!IMPORTANT]
> 使用源服务器时必须考虑以下潜在的安全威胁：任意命令都可嵌入应用程序的 PDB 文件中，因此请确保在 srcsrv.ini 文件中仅放入要执行的命令。 任何尝试执行不在 srcsvr.ini 文件中的命令都将导致出现一个确认对话框。 有关详细信息，请参阅[安全警告：调试器必须执行不受信任的命令](../debugger/security-warning-debugger-must-execute-untrusted-command.md)。 未对命令参数执行任何验证，因此请慎用受信任的命令。 例如，如果你信任 cmd.exe，恶意用户则可能会指定使该命令变得危险的参数。

## <a name="see-also"></a>请参阅
- [指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [调试器安全](../debugger/debugger-security.md)
- [源服务器](/windows/desktop/Debug/source-server-and-source-indexing)
