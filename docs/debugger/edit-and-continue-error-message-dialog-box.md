---
title: “编辑并继续”错误消息对话框 | Microsoft Docs
description: “编辑并继续”可能会报告它无法用于代码更改。 本文介绍可能的原因。
ms.custom: SEO-VS-2020
ms.date: 10/15/2018
ms.topic: reference
f1_keywords:
- vs.debug.ENC.SupportedButNotAvailable
- vs.debug.ENC.CannotEditWhileException
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue Error Message dialog box
ms.assetid: f98c91c0-447a-4533-85b6-87170a0dc4c3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 28fee1e361afbd40e8ebd134dfd702beb9c2b270
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122147009"
---
# <a name="edit-and-continue-error-message"></a>“编辑并继续”错误消息

当你对支持“编辑并继续”的代码语言进行调试，但“编辑并继续”并不适用于你所做的代码更改时，会显示“编辑并继续”错误消息框。 该错误消息提供了更详细的说明。 若要响应该对话框，选择 **确定** 按钮以关闭对话框并取消编辑尝试。

此错误消息的可能原因包括：

- 尝试编辑 SQL Server 代码。
- 尝试编辑优化的代码。 可能需要从发布版本切换为调试版本。
- 尝试在代码运行时而不是在调试器中暂停时对其进行编辑。 尝试[设置断点](../debugger/using-breakpoints.md)，并在暂停时编辑代码。
- 尝试在仅启用非托管调试时编辑托管代码。 “编辑并继续”不可用于[混合模式调试](../debugger/how-to-debug-in-mixed-mode.md)。
- 使用编程语言进行“编辑并继续”不支持的代码更改。 有关详细信息，请参阅 [C# 中支持的代码更改](supported-code-changes-csharp.md)、[Visual Basic“编辑并继续”中不支持的编辑](supported-code-changes-csharp.md)和[支持的 C++ 代码更改](supported-code-changes-cpp.md)等相关文章。
- 尝试在附加到的应用中编辑代码，而不是从“调试”菜单开始调试。
- 尝试在调试 Dr.Watson 转储期间编辑代码。
- 尝试在发生未经处理的异常且未选择“对未经处理的异常展开调用堆栈”选项时编辑代码。
- 尝试在调试嵌入的运行时应用程序时编辑代码。
- 尝试使用具有 64 位应用目标，版本低于 4.5.1 的 .NET Framework 版本来编辑托管代码。 要对版本低于 4.5.1 的 .NET Framework 使用“编辑并继续”，请在“高级编译器”设置下的“\<ProjectName>” > “属性” > “编译”选项卡中将目标设置为“x86”    。
- 尝试编辑在调试过程中修改过并已重新加载的程序集中的代码。
- 尝试编辑尚未加载的程序集中的代码。
- 开始调试应用的旧版本，因为最新版本具有生成错误。

有关详细信息，请参见:
- [“C++ 编辑并继续”博客文章](https://devblogs.microsoft.com/cppblog/c-edit-and-continue-in-visual-studio-2015-update-3/)
- [受支持的代码更改 (C++)](../debugger/supported-code-changes-cpp.md)
- [编辑并继续](../debugger/edit-and-continue.md)