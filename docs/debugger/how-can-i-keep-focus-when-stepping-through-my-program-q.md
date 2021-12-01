---
title: 在单步跟踪程序时保持焦点 | Microsoft Docs
description: 调试窗口激活问题时，使用远程调试防止程序失去焦点。
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.stepping
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], stepping
- focus, keeping
- stepping, focus
- windows, troubleshooting activation
ms.assetid: 11a30580-3a1a-4be8-a241-0abdc758302e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 08c33da272aacbeb604df57b782cc0db532d30aa
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129971239"
---
# <a name="how-can-i-keep-focus-when-stepping-through-my-app"></a>如何在逐句执行应用代码时保持焦点？
## <a name="description"></a>描述
 我的程序存在窗口激活问题。 用调试器逐句通过程序时，因为程序不断失去焦点，所以妨碍了再现问题。 是否有方法可以避免该问题？

## <a name="solution"></a>解决方案
 如果有另一台计算机，请使用远程调试。 可以在远程计算机上运行您的程序，而在主机上运行调试器。 有关详细信息，请参阅[如何：选择远程计算机](/previous-versions/visualstudio/visual-studio-2010/w8wtw2f3(v=vs.100))。

## <a name="see-also"></a>请参阅
- [调试本机代码常见问题解答](../debugger/debugging-native-code-faqs.md)
- [附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [调试本机代码](../debugger/debugging-native-code.md)
