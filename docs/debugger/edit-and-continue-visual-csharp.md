---
title: 编辑并继续 (Visual C#) | Microsoft Docs
description: Visual C# 项目可使用“编辑并继续”。 了解支持哪些编辑，以及如何控制是否应用编辑和何时应用编辑。
ms.custom: SEO-VS-2020
ms.date: 02/22/2022
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Edit and Continue
- Edit and Continue [C#]
- debugging [C#], Edit and Continue
ms.assetid: 591bd1b7-ef10-4d10-817b-3f92ca4be006
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- dotnet
ms.openlocfilehash: c5121198a45298d659dc253cd92a4e614fbc8d02
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139551828"
---
# <a name="edit-and-continue-visual-c"></a>编辑并继续 (Visual C#)
 使用 C# 的“编辑并继续”，可以一边进行调试一边在中断模式下更改代码。 不必停止并重新启动调试会话即可应用更改。 在运行模式下，源编辑器是只读的。

 “编辑并继续”支持在调试会话期间可能做出的大多数更改，但有某些例外。 有关详细信息，请参阅[受支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)。

 Windows 10 或更高版本中的 UWP 支持 "编辑并继续"，以及面向 .NET Framework 4.6 桌面版或更高版本的 x86 和 x64 应用 (.NET Framework 是仅) 的桌面版本。

 > [!NOTE]
 > 不受支持的应用和平台包括 Silverlight 5 和 Windows 8.1。

 如果启用了“编辑并继续”，在使用调试器执行命令（如“继续”、“单步执行”、“设置下一语句”）或在调试器窗口中执行函数计算时，会自动应用受支持的更改  。

 有关详细信息，请参阅[如何：使用“编辑并继续”(C#)](../debugger/how-to-use-edit-and-continue-csharp.md)。

## <a name="see-also"></a>请参阅
- [如何：使用“编辑并继续”(C#)](../debugger/how-to-use-edit-and-continue-csharp.md)
- [支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)
- [在 Visual Studio 中使用 XAML 热重载编写和调试正在运行的 XAML 代码](../xaml-tools/xaml-hot-reload.md)
