---
title: 滚动条的地图模式和滚动条模式
description: 了解如何通过自定义滚动条来跟踪代码中的更改，并了解如何使用“滚动条”模式和“地图”模式。
ms.custom: SEO-VS-2020
ms.date: 03/20/2020
ms.topic: how-to
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: eb56e1dfe2e5410761fc52e2c9edc5fa04095b91
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122086009"
---
# <a name="how-to-customize-the-scroll-bar"></a>如何：自定义滚动条

处理很长的代码文件时，可能很难跟踪所有代码在文件中的位置。 可自定义代码编辑器的滚动条，以了解代码的整体使用情况。

## <a name="annotations"></a>批注

可选择滚动条是否显示注释（如代码更改、断点、书签、错误和插入点位置）。

   1. 依次选择“工具”   > “选项”   > “文本编辑器”   > “所有语言”   > “滚动条”  ，以打开“滚动条”  选项页。

   2. 依次选择“在垂直滚动条上方显示注释”  和所需的注释。 可选择下列注释：

      - 更改
      - 标记
      - 错误
      - 插入点位置

      > [!TIP]
      > “显示标记”  选项包括断点和书签。

试试吧！请打开一个大型代码文件，并替换文件中多处出现的某文本。 滚动条将显示替换的效果，从而在替换了不应替换的内容时可撤回更改。

下面是搜索字符串后滚动条的外观。 请注意，字符串的所有实例都会显示在滚动条中。

![搜索字符串后的 Visual Studio 滚动条](../ide/media/enhancedscrollbarsearch.png)

下面是替换字符串的所有实例后滚动条的外观。 滚动条中的红色标记表明文本替换位置抛出错误。

![替换字符串出错后的 Visual Studio 滚动条](../ide/media/enhancedscrollbarreplace.png)

## <a name="display-modes"></a>显示模式

滚动条有两种模式：滚动条模式和地图模式。

### <a name="bar-mode"></a>滚动条模式

滚动条模式  在滚动条上显示注释指示器。 单击滚动条会向上或向下滚动页面，但不会跳到文件中的相应位置。

### <a name="map-mode"></a>地图模式

“地图模式”在滚动条上以缩图形式显示代码行  。 可选择地图列的宽度，具体方法是在“源代码概述”  中设置值。 若要在将指针悬停在地图之上时放大预览代码，请选择“显示预览工具提示”  选项。 折叠区域进行了不同的阴影化处理，双击阴影即可展开此类区域。

> [!TIP]
> 在地图模式下，可禁用代码缩图，具体方法是将“源代码概述”  设置为“关”  。 如果已选择“显示预览工具提示”  ，仍可在将指针悬停在滚动条之上时预览相应位置的代码，并且在你单击滚动条后光标仍会跳到文件中的相应位置。

下图展示了地图模式已启用且宽度设置为“中等”  时的搜索示例：

![地图模式下的 Visual Studio 滚动条](../ide/media/enhancedscrollbar.png)

下图展示了“显示预览工具提示”  选项：

![显示工具提示的 Visual Studio 滚动条](../ide/media/enhancedscrollbarsearchtooltip.png)

> [!TIP]
> 要更改地图模式中显示的颜色，请选择“工具” > “选项” > “环境” > “字体和颜色”     。 接下来，在“显示项”中，选择前面带有“概述”的所有项，进行所需的颜色更改，然后选择“确定”   。

## <a name="see-also"></a>请参阅

- [代码编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md)
