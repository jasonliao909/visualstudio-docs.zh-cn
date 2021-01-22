---
title: “解析多义性”对话框 | Microsoft Docs
description: 查看 Visual Studio 的“解析多义性”对话框，该框在调试器无法选择要显示的位置时出现。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.Disambig
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Resolve Ambiguity dialog box
- debugger, Resolve Ambiguity dialog box
- debugging [C++], resolving ambiguity
ms.assetid: d9f47455-a116-4c84-8bad-2dfbf4d77f74
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c6f7156a43bc8c5c60415680b4380600e9e695cc
ms.sourcegitcommit: a436ba564717b992eb1984b28ea0aec801eacaec
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98205601"
---
# <a name="resolve-ambiguity-dialog-box"></a>“解析多义性”对话框
当调试器无法选择要显示的位置时，将显示 `Resolve Ambiguity` 对话框。 例如，如果正在使用 C++ 模板，则可以从一个函数模板中创建多个函数。 如果调试器在模板的源位置停止，并且选择了 `Go To Disassembly`，则调试器会有多个选项。 从模板创建的每个函数都有它自己的反汇编代码，而调试器不知道需要查看哪些代码。 利用 `Resolve Ambiguity` 对话框，您可以从所有对应位置的列表中选择所需的位置。

 `Choose the specific location` 列出与命令对应的所有位置。

 `Address` 显示每个函数的内存地址。

 `Function` 显示每个函数的名称。

 `Module` 显示包含函数对象代码的模块（EXE 或 DLL）。

## <a name="see-also"></a>请参阅
- [调试器中的表达式](../debugger/expressions-in-the-debugger.md)