---
title: XAML 错误和警告
description: 了解 Visual Studio 中的 XAML 错误和警告，包括如何对错误进行分类、如何获取错误信息以及如何查找用于解决这些错误的选项。
ms.custom: SEO-VS-2020
ms.date: 03/06/2018
ms.topic: error-reference
ms.assetid: 34eac8a0-7ec5-4c40-b97a-0126ed367931
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-xaml-tools
ms.workload:
- multiple
ms.openlocfilehash: f164a002b5e2c221a10cade55c50fef120452ab6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666963"
---
# <a name="xaml-errors-and-warnings"></a>XAML 错误和警告

创作 XAML 时，Visual Studio 会分析键入的代码。 检测到错误时，代码行上会出现波浪线。 光标悬停在波浪线上可获取错误或警告的详细信息。 对于某些错误和警告，将显示“快速操作”灯泡，使用 Ctrl+.   键盘快捷方式可问题修复选项。

## <a name="error-types"></a>错误类型

多个工具后台并行分析 XAML。 XAML 错误可基于检测到错误的工具分为以下三种类型：

|**检测到错误的工具**|**错误代码格式**|**Visual Studio 版本**|
| - |-----------------| - |
|XAML 语言服务（XAML 编辑器）|XLSxxxx| 所有版本 |
|XAML 设计器|XDGxxxx| 所有版本 | 
|XAML 编辑和继续|XECxxxx| Visual Studio 2019 版本 16.1 或更低版本 |
|XAML 热重载 | XHRxxxx | Visual Studio 2019 版本 16.2 或更高版本 |

有关将“XAML 编辑并继续”更名为“XAML 热重载”的更多详细信息，请参阅我们的[发行说明](/visualstudio/releases/2019/release-notes-v16.2#wpfuwp-tooling)

> [!Note]
> 并非所有错误或警告都有相应的代码。 此类错误通常是 XAML 设计器错误。

## <a name="suppress-xaml-designer-errors"></a>取消显示 XAML 设计器错误

选择“工具”和“选项”，再选择“文本编辑器”和“XAML”>“其他”，即可打开“选项”对话框。

取消选中“显示 XAML 设计器检测到的错误”复选框。

![取消显示 XAML 设计器错误](media/suppress_xaml_designer_errors.png)