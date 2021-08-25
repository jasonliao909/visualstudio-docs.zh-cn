---
description: 当远程计算机尝试与本地计算机通信时，发生 DCOM 错误。
title: 远程计算机无法启动 DCOM 通信 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.unmarshal_callback_failed
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
ms.openlocfilehash: 8a5141560aefaf31337ffc82eee1bfa0f413d43c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122058642"
---
# <a name="error-remote-computer-could-not-initiate-dcom-communications"></a>错误：远程计算机无法启动 DCOM 通信
当远程计算机尝试与本地计算机通信时，发生 DCOM 错误。 本地计算机是

 运行 Visual Studio 的计算机。 出现此错误的原因可能有多种：

- 本地计算机启用了防火墙。

- 从远程计算机到本地计算机的 Windows 身份验证不起作用。

### <a name="to-correct-this-error"></a>更正此错误

1. 如果本地计算机已启用 Windows 防火墙，则请参阅[远程调试](../debugger/remote-debugging.md)中有关如何针对本地调试配置防火墙的说明。

2. 通过尝试从远程服务器打开本地计算机上的文件共享来测试 Windows 身份验证。

3. 若要还原 Windows 身份验证，请尝试重新启动本地计算机和远程计算机。 检查本地和远程计算机上的事件日志以找出 Kerberos 错误，并与域管理员联系以了解已知问题。

## <a name="see-also"></a>请参阅
 [远程调试](../debugger/remote-debugging.md)
