---
title: 选项, 文本编辑器, C/C++, 视图
description: 了解如何使用 C/C++ 部分中的“查看”页面在 Visual Studio 中更改代码波形曲线、无效代码、大纲显示等的默认行为。
ms.custom: SEO-VS-2020
ms.date: 10/08/2021
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.C/C++.View
- VS.ToolsOptionsPages.Text_Editor.C%2FC%2B%2B.View
- VS.ToolsOptionsPages.Text_Editor.C\C++.View
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 733598702bfdd05de04249e19f4005af8af60d10
ms.sourcegitcommit: 5f1e0171626e13bb2c5a6825e28dde48061208a4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2021
ms.locfileid: "129704592"
---
# <a name="options-text-editor-cc-view"></a>选项, 文本编辑器, C/C++, 视图

使用 C 或 C++ 进行编程时，请使用以下属性页更改代码编辑器的默认行为。

要访问此属性页，请选择“工具” > “选项”并依次展开“文本编辑器”和“C/C++”，然后选择“视图”    。

## <a name="code-squiggles"></a>代码波形曲线

可以启用或禁用以下设置来管理文本编辑器为 C 和 C++ 处理代码波形曲线的方式：

- **已跳过的浏览区域中的宏** - 定义如何通过浏览数据库突出显示已跳过区域内的宏，例如其定义包含大括号的宏。

- **可转换为 constexpr 的宏** - 定义如何突出显示可转换为 `constexpr` 定义的宏定义。

## <a name="inactive-code"></a>非活动代码

- **显示非活动块** - 预处理器非活动块将以不同方式着色。

- **禁用非活动代码透明** - 使用纯色而非不透明色来显示非活动代码块。

- **非活动代码不透明度百分比** - 非活动代码块的不透明度百分比。

## <a name="intellisense-error-fix-suggestions"></a>IntelliSense 错误修复建议

- 启用 IntelliSense 错误修复建议 - 针对 IntelliSense 错误启用建议的修补程序。

- 最大 IntelliSense 错误修复建议线程数 - 用于查找 IntelliSense 错误修复建议的最大并发线程数。

- 最大 IntelliSense 错误修复错误数 - 要查找的最大 IntelliSense 错误修复数。

## <a name="miscellaneous"></a>杂项

- **枚举注释任务** - 扫描开放源文件以查找 VS 令牌并在“任务列表”窗口中报告它们。

- **突出显示匹配的令牌** - 突出显示与光标所在位置匹配的封闭括号或语法。

- 配色方案 - 各种默认配色方案，适用于特定于 C/C+ + 的自定义颜色。

## <a name="outlining"></a>大纲显示

- **启用大纲** - 打开文件时进入大纲模式。

- **大纲杂注区域** - 自动描绘 `#pragma` 区域块。

- **大纲语句块** - 自动描绘语句块。

## <a name="see-also"></a>请参阅

- [设置语言特定的编辑器选项](../../ide/reference/setting-language-specific-editor-options.md)
- [在 C++ 中重构（VC 博客）](https://devblogs.microsoft.com/cppblog/all-about-c-refactoring-in-visual-studio-2015-preview/)
