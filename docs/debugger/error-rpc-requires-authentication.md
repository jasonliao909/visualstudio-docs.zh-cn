---
description: Visual Studio 调试器无法连接到远程计算机。
title: RPC 要求身份验证 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.rpc_requires_authentication
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
ms.openlocfilehash: 6de57ce80e15087b7c66986e0c44a3d7a1e3868e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735799"
---
# <a name="error-rpc-requires-authentication"></a>错误：RPC 要求身份验证
Visual Studio 调试器无法连接到远程计算机。 本地计算机上启用了阻止远程调试的 RPC 策略。

### <a name="to-correct-this-error"></a>更正此错误

1. 运行 `\`windir`\system32\regedt32.exe`

2. 找到并删除 `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows NT\RPC\RestrictRemoteClients`。

3. 重新启动计算机以使注册表更改生效。

4. 如果问题仍然存在，请联系域管理员，咨询“计算机配置”>“管理模板”>“系统”>“远程过程调用”>“用于未验证的 RPC 客户端的限制”组策略设置方面的问题。
