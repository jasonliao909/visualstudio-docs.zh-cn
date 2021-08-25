---
title: 使用本机运行时检查 | Microsoft Docs
description: 在 Visual Studio 中使用本机运行时检查来捕获常见的运行时错误，例如堆栈指针损坏、本地数组溢出和堆栈损坏。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- c.runtime.errorchecks
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- /RTC compiler option [C++], /O compiler option
- run-time checks, native
- stack, pointer corruption
- stack pointers, corruption
- /O compiler option, /RTC option
- run-time errors, error checks
- O compiler option, /RTC option
- debugger, runtime errors
- variables [debugger], loss of data
- runtime_checks pragma
- variables [debugger], catching dependencies on uninitialized local variables
- run-time errors, debugging
- debugger, native run-time checks
- optimized build option
- RTC compiler option, /O compiler option
- native run-time checks
- run-time checks
- debugging arrays
- stack pointers
- arrays [Visual Studio], debugging
ms.assetid: dc7b2f1e-5ff6-42e0-89b3-dc9dead83ee1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- cplusplus
ms.openlocfilehash: 5189712cbaff2abd2fb814ee23dc6a87ae086fc7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122051867"
---
# <a name="how-to-use-native-run-time-checks"></a>如何：使用本机运行时检查
在 Visual Studio C++ 项目中，可以使用本机 [runtime_checks](/cpp/preprocessor/runtime-checks) 捕获常见的运行时错误，例如：

- 堆栈指针损坏。

- 本地数组溢出。

- 堆栈损坏。

- 未初始化的局部变量上的依赖项。

- 较短变量赋值的数据丢失。

  如果使用带有优化 ( **/RTC** ) 版本的 **/O**，将导致编译器错误。 如果在优化版本中使用 `runtime_checks` 杂注，则该杂注无效。

  调试启用了运行时检查的程序时，如果出现运行时错误，该程序的默认操作是停止并切换到调试器。 可以更改任何运行时检查的此默认行为。 有关详细信息，请参阅[使用调试器管理异常](../debugger/managing-exceptions-with-the-debugger.md)。

  下面的过程介绍了如何在调试版本中启用本机运行时检查，以及如何修改本机运行时检查的行为。

  本节的其他主题提供了有关以下方面的信息：

- [用 C 运行库自定义运行时检查](../debugger/native-run-time-checks-customization.md)

### <a name="to-enable-native-run-time-checks-in-a-debug-build"></a>在调试版本中启用本机运行时检查

- 使用 **/RTC** 选项，并与 C 运行库（如 /MDd）调试版链接。

### <a name="to-modify-native-run-time-check-behavior"></a>更改本机运行时检查操作

- 使用 `runtime_checks` 杂注。

## <a name="see-also"></a>请参阅
- [在 Visual Studio 中进行调试](../debugger/index.yml)
- [初探调试器](../debugger/debugger-feature-tour.md)
- [runtime_checks](/cpp/preprocessor/runtime-checks)
- [运行时错误检查](/cpp/c-runtime-library/run-time-error-checking)