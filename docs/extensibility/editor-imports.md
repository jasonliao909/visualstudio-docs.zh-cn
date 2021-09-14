---
title: 编辑器导入|Microsoft Docs
description: 了解如何导入编辑器服务、工厂和代理，这些服务、工厂和代理可为扩展提供对核心编辑器的不同类型的访问。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- editors [Visual Studio SDK], new - services
ms.assetid: 8d096de3-33b4-427a-a122-4aeff8a72da0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f263a8748e68395b333d5f34fd00e326736afaf2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665352"
---
# <a name="editor-imports"></a>编辑器导入
可以导入许多编辑器服务、工厂和代理，为扩展提供对核心编辑器的不同类型的访问。 例如，可以导入 来提供 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 给定 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> 内容类型的 。  (此导航器允许在文本缓冲区上执行不同类型的搜索。) 

 若要使用编辑器导入，请将其导入为导出编辑器组件部件的类Managed Extensibility Framework属性。

> [!NOTE]
> 有关此Managed Extensibility Framework，请参阅 Managed Extensibility Framework ([MEF) 。 ](/dotnet/framework/mef/index)

## <a name="import-syntax"></a>导入语法
 以下示例演示如何导入编辑器选项工厂服务。

```
[Import]
internal IEditorOptionsFactoryService EditorOptions { get; set; }
```

 如果要将服务导入为字段而不是属性，应在声明中将其设置为 ，以避免编译器警告未分配给 `null` 变量：

```
[Import]
internal IEditorOptionsFactoryService m_editorOptions = null;
```

 有关使用导入的更多示例，请参阅以下演练：

- [演练：创建边距字形](../extensibility/walkthrough-creating-a-margin-glyph.md)

- [演练：自定义文本视图](../extensibility/walkthrough-customizing-the-text-view.md)

- [演练：突出显示文本](../extensibility/walkthrough-highlighting-text.md)

- [演练：显示 QuickInfo 工具提示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)

- [演练：显示签名帮助](../extensibility/walkthrough-displaying-signature-help.md)

- [演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)

- [演练：显示灯泡建议](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)

## <a name="import-the-service-provider"></a>导入服务提供商
 还可以 (导入程序集 <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> Microsoft.VisualStudio.Shell.Immutable.10.0) 中的) ，以访问 Visual Studio 服务：

```csharp
[Import]
internal SVsServiceProvider ServiceProvider = null;
```

 [有关详细信息，请参阅演练：从编辑器扩展访问 DTE](../extensibility/walkthrough-accessing-the-dte-object-from-an-editor-extension.md)对象。

## <a name="services"></a>服务
 编辑器服务通常是单个实体，它们提供服务，并在多个组件之间共享。

|导入|提供|
|------------|--------------|
|<xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService>|文件扩展名和对象 <xref:Microsoft.VisualStudio.Utilities.IContentType> 之间的关系。|
|<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>|<xref:Microsoft.VisualStudio.Utilities.IContentType> 对象的集合。|
|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformationService>|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformation> 对象。|
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>|许多编辑器适配器对象：<br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|
|<xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearchFactoryService>|<xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearch>给定文本视图的对象。|
|<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>|<xref:Microsoft.VisualStudio.Text.ITextBuffer>。|
|<xref:Microsoft.VisualStudio.Text.ITextDocumentFactoryService>|<xref:Microsoft.VisualStudio.Text.ITextDocument>。|
|<xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceService>|差异 <xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceCollection%601> 的 。|
|<xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalStringDifferenceService>|差异 <xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalDifferenceCollection> 的 。|
|<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService>|<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer>或 <xref:Microsoft.VisualStudio.Text.Projection.IElisionBuffer> 。|
|<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService>|一 <xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph> 组 对象的 <xref:Microsoft.VisualStudio.Text.ITextBuffer> 。|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService>|的 <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> <xref:Microsoft.VisualStudio.Text.ITextBuffer> 。|
|<xref:Microsoft.VisualStudio.Text.Classification.IViewClassifierAggregatorService>|的 <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMapService>|的 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>|的 <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>|维护 对象 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> 的集合。|
|<xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService>|文本 <xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601> 缓冲区的 。|
|<xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService>|文本 <xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601> 视图的 。|
|<xref:Microsoft.VisualStudio.Text.Editor.IEditorOptionsFactoryService>|指定 <xref:Microsoft.VisualStudio.Text.Editor.IEditorOptions> 范围的 。|
|<xref:Microsoft.VisualStudio.Text.Editor.IScrollMapFactoryService>|文本 <xref:Microsoft.VisualStudio.Text.Editor.IScrollMap> 视图的 。|
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|的 <xref:Microsoft.VisualStudio.Text.Editor.ISmartIndent> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|获取通过 对象自动缩 <xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentProvider> 进。|
|<xref:Microsoft.VisualStudio.Text.Editor.ITextEditorFactoryService>|管理 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> 的 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> 。|
|<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedTextSourceFactoryService>|<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>。|
|<xref:Microsoft.VisualStudio.Text.Formatting.IRtfBuilderService>|从一组快照范围生成 RTF 格式的文本。|
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencerFactoryService>|的 <xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencer> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextParagraphPropertiesFactoryService>|一 <xref:System.Windows.Media.TextFormatting.TextParagraphProperties> 个 ，用于设置视图中文本行的格式。|
|<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService>|<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperations>的 对象 <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>|搜索文本快照。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>|for <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> by 的 <xref:Microsoft.VisualStudio.Text.ITextBuffer> <xref:Microsoft.VisualStudio.Utilities.IContentType> 。|
|<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService>|文本 <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager> 视图的 。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IGlyphService>|一组标准字形。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStackMapService>|的 <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStack> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IWpfKeyboardTrackingService>|跟踪键盘处理。|
|<xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService>|标准 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> 对象。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistoryRegistry>|维护文本缓冲区和对象  <xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistory> 之间的关系。|

## <a name="other-imports"></a>其他导入
 提供程序工厂和代理通常是可在多个组件中具有多个实例的实体。

|导入|提供|
|------------|--------------|
|<xref:Microsoft.VisualStudio.Text.Adornments.IErrorProviderFactory>|一 <xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601> 个 <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag> 类型) 给定缓冲区的 。|
|<xref:Microsoft.VisualStudio.Text.Adornments.ITextMarkerProviderFactory>|文本标记标记 (类型 <xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601> 为 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>) 。|
|<xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProviderFactory>|给定 <xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProvider> 的 <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSession>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSession>。|

## <a name="see-also"></a>另请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
