---
title: 创建托管对象的自定义视图 | Microsoft Docs
description: Visual Studio 调试器在其变量窗口中显示数据。 了解如何自定义数据类型（包括自定义类型）的显示方式。
ms.custom: SEO-VS-2020
ms.date: 01/08/2019
ms.topic: conceptual
f1_keywords:
- vs.debug.data.elements
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- data types, custom
- custom data types
- managed code, custom data types
- autoexp.dat file
- mcee_cs.dat file
- debugger, expanding data types
- mcee_mc.dat file
ms.assetid: 9969e9b2-9008-4729-8a14-0d6deaa61576
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- dotnet
ms.openlocfilehash: 327e8d74120555a4a121775f79b8ac5afe923f77
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122052429"
---
# <a name="create-custom-views-of-managed-objects-c-visual-basic-f-ccli"></a>创建托管对象的自定义视图（C#、Visual Basic、F#、C++/CLI）
可以在调试器变量窗口中自定义 Visual Studio 显示数据类型的方式。

## <a name="attributes"></a>特性

在 C#、Visual Basic、F# 和 C++（仅限 C++/CLI 代码）中，可以使用 <xref:System.Diagnostics.DebuggerTypeProxyAttribute>、<xref:System.Diagnostics.DebuggerDisplayAttribute> 和 <xref:System.Diagnostics.DebuggerBrowsableAttribute> 来添加自定义数据的扩展。

在 .NET Framework 2.0 代码中，Visual Basic 不支持 DebuggerBrowsable 特性。 此项限制在 .NET 较高版本中已经删除。

## <a name="visualizers"></a>可视化工具

可以编写可视化工具来显示任何托管数据类型。 有关详细信息，请参阅[如何：编写可视化工具](create-custom-visualizers-of-data.md)。

> [!NOTE]
> 对于 C++ 代码，可以使用 Natvis 框架添加自定义数据类型扩展，如[在调试器中创建 C++ 对象的自定义视图](create-custom-views-of-native-objects.md)中所述。

## <a name="see-also"></a>请参阅

- [使用 DebuggerDisplay 特性向调试器指示要显示的内容](../debugger/using-the-debuggerdisplay-attribute.md)
- [使用 DebuggerTypeProxy 特性向调试器指示要显示的类型](../debugger/using-debuggertypeproxy-attribute.md)
- [监视和快速监视窗口](../debugger/watch-and-quickwatch-windows.md)
- [使用调试器显示特性增强调试](/dotnet/framework/debug-trace-profile/enhancing-debugging-with-the-debugger-display-attributes)
