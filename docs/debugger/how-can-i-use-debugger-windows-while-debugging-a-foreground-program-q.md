---
title: 调试前台应用时使用调试器窗口 | Microsoft Docs
description: 如果要调试的程序必须留在前台，请使用远程调试以避免将其置于后台。
ms.custom: SEO-VS-2020, seodec18
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
ms.workload:
- multiple
ms.openlocfilehash: 03a143ee2d04227171895bf2b14dff92545b9952
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102155089"
---
# <a name="how-can-i-use-debugger-windows-while-debugging-a-foreground-program"></a>调试前台程序时如何使用调试器窗口？
## <a name="problem-description"></a>问题描述
 我在尝试调试屏幕绘制问题。 若要观察该问题，必须将程序保持在前台，这意味着不能访问调试窗口。 我该怎么办？

## <a name="solution"></a>解决方案
 如果有另一台计算机，则可以使用远程调试。 通过两台计算机的设置，当在主机上运行调试器时，可以监视远程计算机上的屏幕绘制。 有关远程调试的详细信息，请参阅[远程调试](../debugger/remote-debugging.md)。

## <a name="see-also"></a>请参阅
- [调试本机代码常见问题解答](../debugger/debugging-native-code-faqs.md)
- [调试本机代码](../debugger/debugging-native-code.md)
