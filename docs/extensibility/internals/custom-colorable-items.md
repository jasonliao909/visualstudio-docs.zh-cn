---
title: 自定义可着色项|Microsoft Docs
description: 了解如何通过重写"字体和颜色"对话框中的项（如关键字和注释）创建自定义可着色项作为语言服务的一部分。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, custom colorable items
ms.assetid: b4d0ddee-c04b-48dc-ba82-f6068570cef0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 662b440b716eed2f878f6ede3e21e7339ab209ded5055e8dbd0dcca02017d408
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121261367"
---
# <a name="custom-colorable-items"></a>自定义可着色项
可以通过将自定义可着色项作为语言服务的一部分实现，重写用于着色的类型列表（如关键字和注释）。

## <a name="user-settings-of-colorable-items"></a>可着色项的用户设置
 可以通过在"工具 **"菜单** 上选择"选项"，然后在"环境"下选择"字体 **和颜色"来显示"字体和颜色****"对话框**。  选择显示（如文本编辑器或命令窗口）时，"显示 **项**"列表框将显示该显示的所有可着色项。 可以查看和更改每个可着色项的字体、大小、前景色和背景色。 你的选择存储在注册表的缓存中，并按可着色项名称访问。

## <a name="presentation-of-colorable-items"></a>可着色项的呈现
 由于 IDE 处理"字体和颜色"对话框中可着色项的用户替代，因此只需提供每个具有名称的自定义可着色项。 此名称显示在"显示项 **"** 列表中。 可着色项按字母顺序显示。 若要对语言服务的自定义可着色项进行分组，可以使用语言名称开头每个名称，例如 **NewLanguage - Comment** 和 **NewLanguage - 关键字**。

> [!CAUTION]
> 应在可着色项名称中包括语言名称，以避免与现有的可着色项名称发生冲突。 如果在开发过程中更改了其中一个可着色项的名称，则必须重置首次访问可着色项时创建的缓存。 可以使用 **CreateExpInstance** 工具重置实验性缓存，该工具随 Visual Studio SDK 一起安装，通常位于 Visual Studio 安装文件夹下的以下目录中：
>
> *VSSDK\VisualStudioIntegration\Tools\Bin*
>
> 若要重置缓存，请输入 **CreateExpInstance /Reset**。 有关 **CreateExpInstance 详细信息，** 请参阅 [CreateExpInstance 实用工具](../../extensibility/internals/createexpinstance-utility.md)。

 永远不会引用可着色项列表中的第一项。 第一项对应于可着色项索引 0，并始终提供该项 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的默认文本颜色和属性。 处理此未引用项的最简单方法是在列表中提供占位符可着色项作为第一项。

## <a name="implement-custom-colorable-items"></a>实现自定义可着色项

1. 定义必须以语言着色的项，例如关键字、运算符和标识符。

2. 创建这些可着色项的枚举。

3. 将分析器或扫描程序返回的标记类型与枚举值关联。

    例如，表示标记类型的值可能是自定义可着色项枚举中的相同值。

4. 在 对象的 方法的实现中，使用自定义可着色项枚举中的值填充属性列表，这些值对应于从分析器或扫描程序返回的标记 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 类型。

5. 在实现 接口的同一个类中 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> ，实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> 接口及其两个方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> ： 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> 。

6. 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> 接口。

7. 如果要支持 24 位或高颜色值，则还要实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 接口。

8. 在语言服务对象中，创建一个包含对象的列表，一个列表用于分析器或扫描程序可以识别的每个可着色 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> 项。

    可以使用自定义可着色项枚举中的相应值访问列表中的每个项。 使用 枚举值作为列表中的索引。 永远不会访问列表中的第一项，因为它对应于始终处理自身 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的默认文本样式。 可以通过在列表的开头插入占位符可着色项来弥补这一问题。

9. 在 方法的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> 实现中，返回自定义可着色项列表中的项数。

10. 在 方法的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> 实现中，从列表中返回请求的可着色项。

    有关实现 和 接口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 的示例，请参阅 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 。

## <a name="see-also"></a>另请参阅
- [旧版语言服务模型](../../extensibility/internals/model-of-a-legacy-language-service.md)
- [自定义编辑器中的语法着色](../../extensibility/syntax-coloring-in-custom-editors.md)
- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [实现语法着色](../../extensibility/internals/implementing-syntax-coloring.md)
- [如何：使用内置可着色项](../../extensibility/internals/how-to-use-built-in-colorable-items.md)
