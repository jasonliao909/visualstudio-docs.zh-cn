---
description: 当本地计算机尝试与远程计算机通信时，发生 DCOM 错误。
title: 无法启动 DCOM 通信 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.unmarshal_server_failed
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
ms.openlocfilehash: 5890fc9772e3645aca16893ab8b9c3b3d3af7d31
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122074346"
---
# <a name="error-unable-to-initiate-dcom-communication"></a>错误：无法启动 DCOM 通信
当本地计算机尝试与远程计算机通信时，发生 DCOM 错误。 这是由于远程服务器上存在防火墙或远程计算机上的 Windows 身份验证已中断。

### <a name="to-correct-this-error"></a>更正此错误

- 如果远程计算机已启用 Windows 防火墙，请参阅[远程调试](../debugger/remote-debugging.md)中有关如何针对本地调试配置防火墙的说明。

- 若要还原 Windows 身份验证，请尝试重新启动本地计算机和远程计算机。 检查本地和远程计算机上的事件日志以找出 Kerberos 错误，并与域管理员联系以了解已知问题。

## <a name="see-also"></a>请参阅
- [远程调试](../debugger/remote-debugging.md)
