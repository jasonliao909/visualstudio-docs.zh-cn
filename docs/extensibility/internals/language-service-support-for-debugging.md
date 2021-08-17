---
title: 调试语言语言服务|Microsoft Docs
description: 了解 IVsLanguageDebugInfo 接口中的语言服务功能，这些功能支持在 Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugger, language support
- language services, debugging support
ms.assetid: 7a44067f-a410-4a6a-84d2-bda5184140bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 72cac3ff7768d49f66c87b569312253669d735fa2e64fdb895b51ff29aae2ca4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121375891"
---
# <a name="language-service-support-for-debugging"></a>用于调试的语言服务支持
语言服务可以通过 接口提供支持调试器 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo> 的功能。 这些功能包括验证断点，以及向"自动"窗口 **提供表达式** 列表。

 但是，你需要有一个表达式计算程序来调试语言。 表达式计算程序负责计算表达式，以在调试时生成值。 有关实现 CLR 表达式计算程序的信息，请参阅：

- [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)

- [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)

## <a name="compiler-output"></a>编译器输出
 编译器的类型决定了实现语言调试所需的操作。 如果编译器面向 Windows操作系统并写入 .pdb 文件，可以使用集成到 Visual Studio 中的本机代码调试引擎来调试Visual Studio。 如果编译器使用 MSIL (生成 Microsoft 中间) ，可以使用托管代码调试引擎（也集成到 MSIL Visual Studio） 来调试程序。 如果编译器面向专有操作系统或其他运行时环境，则需要编写自己的调试引擎。

 有关为语言实现调试详细信息，请参阅 入门[调试](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)SDK Visual Studio中的代码。
