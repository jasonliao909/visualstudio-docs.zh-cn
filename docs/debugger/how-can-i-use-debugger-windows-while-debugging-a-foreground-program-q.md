---
title: 调试前台应用时使用调试器窗口 | Microsoft Docs
description: 如果要调试的程序必须留在前台，请使用远程调试以避免将其置于后台。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.background
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- foreground program debugging
- remote debugging, debugging foreground programs
- debugging [Visual Studio], while observing foreground programs
- focus, debugging while observing foreground programs
- debugging [Visual Studio], foreground programs
ms.assetid: 9e67a308-1c81-42ab-966b-7fc3c1d2bf7a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e8135bb76d8e3c6ae21e2287966b8478f9db6c07
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122105205"
---
# <a name="how-can-i-use-debugger-windows-while-debugging-a-foreground-program"></a>调试前台程序时如何使用调试器窗口？
## <a name="problem-description"></a>问题描述
 我在尝试调试屏幕绘制问题。 若要观察该问题，必须将程序保持在前台，这意味着不能访问调试窗口。 我该怎么办？

## <a name="solution"></a>解决方案
 如果有另一台计算机，则可以使用远程调试。 通过两台计算机的设置，当在主机上运行调试器时，可以监视远程计算机上的屏幕绘制。 有关远程调试的详细信息，请参阅[远程调试](../debugger/remote-debugging.md)。

## <a name="see-also"></a>请参阅
- [调试本机代码常见问题解答](../debugger/debugging-native-code-faqs.md)
- [调试本机代码](../debugger/debugging-native-code.md)
