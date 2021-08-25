---
title: 在调试器中创建数据的自定义视图 | Microsoft Docs
description: 了解在 Visual Studio 调试器中检查和修改程序状态的各种方法。 其中包括“自动”和“监视”窗口、数据提示和可视化工具。
ms.custom: SEO-VS-2020
ms.date: 01/09/2019
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugging [Visual Studio], inspecting programs
- debugger, viewing data
ms.assetid: 13e1105f-f987-402e-9108-ec6ac12be042
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9cdce099df34fbf7937ed83d1adc70fe36c13176
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122043903"
---
# <a name="create-custom-views-of-data-in-the-visual-studio-debugger-c-visual-basic-c"></a>在 Visual Studio 调试器中创建数据的自定义视图（C#、Visual Basic、C++）

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 调试器提供了许多用于检查和修改程序状态的工具。 这些工具中的大多数仅在中断模式下有效。

## <a name="create-custom-views-of-data-in-variable-windows-and-datatips"></a>在变量窗口和数据提示中创建数据的自定义视图

 许多[调试器窗口](../debugger/debugger-windows.md)（例如“自动”和“监视”窗口）允许检查变量。 你可以自定义 C++ 类型、托管对象和你自己的类型在调试器变量窗口和[数据提示](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)中的显示方式。 有关详细信息，请参阅[创建 C++ 对象的自定义视图](../debugger/create-custom-views-of-native-objects.md)和[创建托管对象的自定义视图](../debugger/create-custom-views-of-managed-objects.md)。

## <a name="create-custom-visualizers"></a>创建自定义可视化工具

 可视化工具使你能够以有意义的方式查看对象或变量的内容。 在 Visual Studio 调试器中，可视化工具是指可以使用放大镜 ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "可视化工具图标") 图标打开的不同窗口。 例如，HTML 可视化工具显示如何在浏览器中解释和显示 HTML 字符串。 可以通过数据提示、“监视”窗口、“自动”窗口和“局部变量”窗口来访问可视化工具  。 “快速监视”对话框也提供可视化工具。 有关详细信息，请参阅[创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)。

## <a name="see-also"></a>请参阅

- [初探调试器](../debugger/debugger-feature-tour.md)
- [“命令”窗口](../ide/reference/command-window.md)
- [调试器安全](../debugger/debugger-security.md)
