---
title: “Microsoft Visual Studio 调试器（引发异常）”对话框 | Microsoft Docs
titleSuffix: ''
description: 了解发生程序需要处理的异常时的处理方法。 你可以：1) 中断到调试器；2) 继续；或 3) 忽略。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.exceptions.thrown
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Microsoft Visual Studio Debugger (Exception Thrown) dialog box
- exception handling, during debugging
- debugger, exceptions
- throwing exceptions, during debugging
ms.assetid: 1fe98d10-c8f9-4b39-a920-99169bfd542e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e5a45ef315d29c5b47684c93cbb9e74055fc9990
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122030719"
---
# <a name="microsoft-visual-studio-debugger-exception-thrown-dialog-box"></a>“Microsoft Visual Studio 调试器（引发异常）”对话框
程序中发生了异常。 此对话框报告引发异常的类型。 你的代码需要处理此异常。 可从下列用于处理异常的选项中进行选择：

 **中断** 允许执行中断调试器。 在中断之前不调用异常处理程序。 如果您从中断继续执行，则将调用异常处理程序。

 **继续** 允许执行继续，并使异常处理程序有机会处理异常。 此选项对某些类型的异常不可用。 “继续”将允许应用程序继续。 在本机应用程序中，它将导致再次引发异常。 在托管应用程序中，它使程序终止或由主机应用程序处理异常。

> [!NOTE]
> 在托管代码中出现未经处理的异常后将无法继续。 在托管代码中出现未经处理的异常后选择“继续”将导致调试停止。

 **忽略** 允许执行继续，但不调用异常处理程序。 由于未调用异常处理程序，这会导致更严重的后果，包括更多的异常和错误。 此选项对某些类型的异常不可用。

## <a name="see-also"></a>请参阅
- [管理调试器的异常](../debugger/managing-exceptions-with-the-debugger.md)
- [与异常有关的最佳做法](/dotnet/standard/exceptions/best-practices-for-exceptions)
- [异常处理](/cpp/extensions/exception-handling-cpp-component-extensions)