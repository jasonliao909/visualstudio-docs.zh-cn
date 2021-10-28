---
title: 本机运行时检查自定义 | Microsoft Docs
description: 了解自定义运行时检查的方法，包括：指定消息目标、编写错误报告函数，以及查询错误信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.crt
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- runtime_checks pragma
- debugger, native run-time checks
- /RTC compiler option [C++], native run-time checks
- customizing CRT error checking
- native run-time checks, customizing
ms.assetid: 76a365fe-6439-49db-8603-34058b78e5a8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- cplusplus
ms.openlocfilehash: 0be145d41fbc2ae112372ba1653caca983118605
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736916"
---
# <a name="native-run-time-checks-customization"></a>本机运行时检查自定义
在使用 /RTC（运行时检查）进行编译或使用 `runtime_checks` 杂注时，C 运行时库会提供本机运行时检查。 某些情况下，可能需要自定义运行时检查：

- 将运行时检查信息传送到默认以外的文件或目标。

- 为第三方调试器的运行时检查信息指定输出目标。

- 报告用 C 运行库发布版本编译的程序中的运行时检查信息。 该库的发布版本不使用 `_CrtDbgReportW` 报告运行时错误。 相反，它们为每个运行时错误显示“断言”对话框。

  若要自定义运行时错误检查，可以：

- 编写一个运行时错误报告函数。 有关详细信息，请参阅[如何：编写运行时错误报告函数](../debugger/how-to-write-a-run-time-error-reporting-function.md)。

- 自定义错误消息目标。

- 查询有关运行时检查错误的信息。

## <a name="customize-the-error-message-destination"></a>自定义错误消息目标
 如果使用 `_CrtDbgReportW` 报告错误，可以使用 `_CrtSetReportMode` 指定错误消息的目标。

 如果使用自定义报告函数，则使用 `_RTC_SetErrorType` 将错误与报告类型关联。

## <a name="query-for-information-about-run-time-checks"></a>查询有关运行时检查的信息
 `_RTC_NumErrors` 返回运行时错误检查所检测到的错误类型的数量。 要得到每个错误的简短说明，可以从 0 循环到 `_RTC_NumErrors` 的返回值，并在每次循环中将迭代值传递给 `_RTC_GetErrDesc`。 有关详细信息，请参阅 [_RTC_NumErrors](/cpp/c-runtime-library/reference/rtc-numerrors) 和 [_RTC_GetErrDesc](/cpp/c-runtime-library/reference/rtc-geterrdesc)。

## <a name="see-also"></a>请参阅
- [如何：使用本机运行时检查](../debugger/how-to-use-native-run-time-checks.md)
- [runtime_checks](/cpp/preprocessor/runtime-checks)
- [_CrtDbgReport、_CrtDbgReportW](/cpp/c-runtime-library/reference/crtdbgreport-crtdbgreportw)