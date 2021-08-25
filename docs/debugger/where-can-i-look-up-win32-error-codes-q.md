---
title: 可以在哪里查阅 Win32 错误代码？ | Microsoft Docs
description: 若要查找 Win32 错误代码，请在“监视”或“快速监视”中输入错误代码。 例如，“0x80000004,hr”。 此错误代码定义位于 INCLUDE\WINERROR.H 中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vc.errors
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- error codes, Win32
- Win32, error codes
ms.assetid: 8fb4ff42-b8eb-4152-b49e-b802d194b05e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 570b36b67fffbc65f5622601260b30dfb80a95bd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122112216"
---
# <a name="where-can-i-look-up-win32-error-codes"></a>可以在哪里查阅 Win32 错误代码？
默认系统安装的 INCLUDE 目录中的 WINERROR.H 包含 Win32 API 函数的错误代码定义。

 可以通过在“监视”窗口或“快速监视”对话框中键入错误代码来查阅该代码   。 例如：

`0x80000004,hr`

## <a name="see-also"></a>请参阅
- [调试本机代码常见问题解答](../debugger/debugging-native-code-faqs.md)
- [调试本机代码](../debugger/debugging-native-code.md)