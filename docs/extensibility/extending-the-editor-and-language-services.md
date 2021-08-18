---
title: 扩展编辑器和语言服务|Microsoft Docs
description: 可以将语言服务功能添加到编辑器并扩展Visual Studio编辑器的功能。 了解Managed Extensibility Framework。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new -
ms.assetid: 8d04f8db-eda7-4b3e-b6eb-c06df104502a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 8fa21afe5bffa298847aa90229e087c94b38f8a1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122125122"
---
# <a name="extend-the-editor-and-language-services"></a>扩展编辑器和语言服务
可以将语言服务功能 (IntelliSense) 添加到自己的编辑器，并扩展代码编辑器Visual Studio功能。  有关可以扩展内容的完整列表，请参阅 [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)。

 使用 MEF 应用扩展大多数Managed Extensibility Framework (功能) 。 例如，如果要扩展的编辑器功能是语法着色，可以编写 *MEF* 组件部分，用于定义需要不同着色的分类及其处理方式。 编辑器还支持同一功能的多个扩展。

 编辑器呈现层基于 Windows Framework (WPF) 。 WPF 为灵活的文本格式设置提供图形库，并提供图形和动画等可视化效果。

 Visual Studio SDK 提供 *称为填充码* 的适配器，以支持为早期版本编写的 VSPackage。 不过，如果你有现有的 VSPackage，我们建议将其更新为新技术，以获得更好的性能和可靠性。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[语言服务和编辑器扩展入门](../extensibility/getting-started-with-language-service-and-editor-extensions.md)|说明如何创建编辑器的扩展。|
|[在编辑器中](../extensibility/inside-the-editor.md)|描述编辑器的一般结构，并列出其一些功能。|
|[Managed Extensibility Framework编辑器中](../extensibility/managed-extensibility-framework-in-the-editor.md)|说明如何将 MEF Managed Extensibility Framework (与) 一起使用。|
|[语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)|列出编辑器的扩展点。 扩展点表示可以扩展的编辑器功能。|
|[演练：使用列指南创建视图修饰、命令和 (设置) ](../extensibility/walkthrough-creating-a-view-adornment-commands-and-settings-column-guides.md)|逐步讲解如何生成视图修饰，该装饰可绘制列指南行，以帮助将代码保持在特定的显示宽度。  还显示读取和写入设置，以及声明和实现可以从命令窗口调用的命令。|
|[编辑器导入](../extensibility/editor-imports.md)|列出扩展可以导入的服务。|
|[根据编辑器调整旧代码](/previous-versions/visualstudio/visual-studio-2015/extensibility/adapting-legacy-code-to-the-editor?preserve-view=true&view=vs-2015)|介绍在 2010 (2010 Visual Studio之前调整旧) 以扩展编辑器的不同方法。|
|[迁移旧版语言服务](../extensibility/internals/migrating-a-legacy-language-service.md)|说明如何迁移基于 VSPackage 的语言服务。|
|[演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)|演示如何将内容类型链接到文件扩展名。|
|[演练：创建边距字形](../extensibility/walkthrough-creating-a-margin-glyph.md)|演示如何向边距添加图标。|
|[演练：突出显示文本](../extensibility/walkthrough-highlighting-text.md)|演示如何使用标记 *突出显示* 文本。|
|[演练：添加大纲显示](../extensibility/walkthrough-outlining.md)|演示如何为特定种类的大括号添加大纲显示。|
|[演练：显示匹配的大括号](../extensibility/walkthrough-displaying-matching-braces.md)|演示如何突出显示匹配的大括号。|
|[演练：显示 QuickInfo 工具提示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)|演示如何显示描述代码元素（如属性、方法和事件）的 QuickInfo 弹出窗口。|
|[演练：显示签名帮助](../extensibility/walkthrough-displaying-signature-help.md)|演示如何显示弹出窗口，这些弹出窗口提供有关签名中参数的数量和类型的信息。|
|[演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)|演示如何实现语句完成。|
|[演练：实现代码片段](../extensibility/walkthrough-implementing-code-snippets.md)|演示如何实现代码片段扩展。|
|[演练：显示灯泡建议](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)|演示如何显示代码建议的灯泡。|
|[演练：将 shell 命令与编辑器扩展一同使用](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)|演示如何将 VSPackage 中的菜单命令与 MEF 组件关联。|
|[演练：将快捷键与编辑器扩展一同使用](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)|演示如何将 VSPackage 中的菜单快捷方式与 MEF 组件关联。|
|[Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)|提供有关 MEF Managed Extensibility Framework (的信息) 。|
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|提供有关 WPF Windows Presentation Foundation (的信息) 。|

## <a name="reference"></a>参考
 "Visual Studio编辑器"包括以下命名空间。

 <xref:Microsoft.VisualStudio.Language.Intellisense>

 <xref:Microsoft.VisualStudio.Language.StandardClassification>

 <xref:Microsoft.VisualStudio.Editor>

 <xref:Microsoft.VisualStudio.Text>

 <xref:Microsoft.VisualStudio.Text.Adornments>

 <xref:Microsoft.VisualStudio.Text.Classification>

 <xref:Microsoft.VisualStudio.Text.Differencing>

 <xref:Microsoft.VisualStudio.Text.Document>

 <xref:Microsoft.VisualStudio.Text.Editor>

 <xref:Microsoft.VisualStudio.Text.Editor.OptionsExtensionMethods>

 <xref:Microsoft.VisualStudio.Text.Formatting>

 <xref:Microsoft.VisualStudio.Text.IncrementalSearch>

 <xref:Microsoft.VisualStudio.Text.Operations>

 <xref:Microsoft.VisualStudio.Text.Outlining>

 <xref:Microsoft.VisualStudio.Text.Projection>

 <xref:Microsoft.VisualStudio.Text.Tagging>

 <xref:Microsoft.VisualStudio.Utilities>