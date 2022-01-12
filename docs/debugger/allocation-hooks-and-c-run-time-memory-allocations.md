---
title: 分配挂钩和 C 运行时内存分配
description: 了解 Visual Studio 调试中的分配挂钩和 C 运行时内存分配。 分配挂钩函数必须显式忽略 _CRT_BLOCK 块。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], hook functions
- memory allocation, troubleshooting allocation hooks
- allocation hooks
- hooks, allocation
ms.assetid: cc34ee96-3d91-41bd-a019-aa3759139e7e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 4dc339e50c59339b0ed042303a8e60b7cb6867ad
ms.sourcegitcommit: 965372ad0d75f015403c1af508080bf799914ce3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "135802993"
---
# <a name="allocation-hooks-and-c-run-time-memory-allocations"></a>分配挂钩和 C 运行时内存分配
对分配挂钩函数的一个很重要的限制是，该函数必须显式忽略 `_CRT_BLOCK` 块。 这些块是 C 运行时库函数在内部进行的内存分配的结果（前提是调用分配内部内存的 C 运行时库函数）。 将以下代码添加到分配挂钩函数开始处即可忽略 `_CRT_BLOCK` 块：

```cpp
if ( nBlockUse == _CRT_BLOCK )
    return( TRUE );
```

如果分配挂钩不忽略 `_CRT_BLOCK` 块，则在挂钩中调用的任何 C 运行时库函数都可能会使程序陷入无限循环。 例如，`printf` 执行内部分配。 如果挂钩代码调用 `printf`，则进行的分配会导致挂钩再次被调用，于是会再次调用 “printf”，如此这样，直到堆栈溢出  。 如果需要报告 `_CRT_BLOCK` 分配操作，则避免该限制的一种方法是使用 Windows API 函数而不是 C 运行时函数进行格式化和输出。 Windows API 不使用 C 运行时库堆，因此不会让分配挂钩陷入无限循环。

如果检查运行时库源文件，则会看到默认的分配挂钩函数 **CrtDefaultAllocHook**（直接返回 **TRUE**）位于其自身的独立文件 DBGHOOK.C 中。 如果希望调用分配挂钩（即使分配是由在应用程序的 **main** 函数之前执行的运行时启动代码进行的），则可将此默认函数替换为你自己的一个函数，而不使用 [_CrtSetAllocHook](/cpp/c-runtime-library/reference/crtsetallochook)。

## <a name="see-also"></a>请参阅
- [编写调试挂钩函数](../debugger/debug-hook-function-writing.md)
