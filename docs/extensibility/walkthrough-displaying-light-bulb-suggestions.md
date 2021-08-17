---
title: 演练：显示灯泡建议|Microsoft Docs
description: 了解如何使用本演练在 Visual Studio编辑器中创建一个灯泡，该灯泡显示在当前单词上，并具有两个建议的操作。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 99e5566d-450e-4660-9bca-454e1c056a02
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 0cdb146d44b768912a157a5d60a91d20957553c13f3c2303a5bdd8d9cf82d58f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121374977"
---
# <a name="walkthrough-display-light-bulb-suggestions"></a>演练：显示灯泡建议
灯泡是编辑器中的Visual Studio图标，可展开以显示一组操作，例如，修复由内置代码分析器或代码重构识别的问题。

 在 Visual C# 和 Visual Basic 编辑器中，还可使用 .NET Compiler Platform ("Roslyn") 编写和打包自己的代码分析器，以及自动显示灯泡的操作。 有关详细信息，请参阅：

- [如何：编写 C# 诊断和代码修复](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md)

- [如何：编写Visual Basic和代码修复](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-Visual-Basic-Analyzer-and-Code-Fix.md)

  其他语言（如 C++）也提供一些快速操作（例如，创建该函数的存根实现的建议）的灯泡。

  灯泡如下所示。 在 Visual Basic 或 Visual C# 项目中，如果变量名称无效，则变量名称下会显示一条红色长线。 如果将鼠标悬停在无效标识符上，光标附近会出现一个灯泡。

  ![灯泡](../extensibility/media/lightbulb.png "灯泡")

  如果单击灯泡的向下箭头，则会显示一组建议的操作，以及所选操作预览。 在这种情况下，它显示执行该操作时对代码所做的更改。

  ![灯泡预览](../extensibility/media/lightbulbpreview.png "LightBulbPreview")

  可以使用灯泡提供自己的建议操作。 例如，可以提供将左大括号移动到新行或将其移到前一行末尾的操作。 下面的演练演示如何创建在当前单词上出现的灯泡，并具有以下两个建议操作：转换为大写和 **转换为小写**。 

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-a-managed-extensibility-framework-mef-project"></a>创建一Managed Extensibility Framework (MEF) 项目

1. 创建 C# VSIX 项目。  ("**新建** Project对话框中，选择 **"Visual C#/** 扩展性"，然后选择 **"VSIX Project**.) 将解决方案命名 `LightBulbTest` "。

2. 向 **项目添加编辑器** 分类器项模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

4. 将以下引用添加到项目，将" **复制本地"** 设置为 `False` ：

     *Microsoft.VisualStudio.Language.Intellisense*

5. 添加新的类文件，将其命名 **为 LightBulbTest**。

6. 添加以下 using 指令：

    ```csharp
    using System;
    using System.Linq;
    using System.Collections.Generic;
    using System.Threading.Tasks;
    using Microsoft.VisualStudio.Language.Intellisense;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Operations;
    using Microsoft.VisualStudio.Utilities;
    using System.ComponentModel.Composition;
    using System.Threading;

    ```

## <a name="implement-the-light-bulb-source-provider"></a>实现灯泡源提供程序

1. 在 *LightBulbTest.cs* 类文件中，删除 LightBulbTest 类。 添加一个名为 **TestSuggestedActionsSourceProvider 的** 类，该类实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider> 。 使用"测试建议 **的操作的名称"和** " <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> 文本"导出它。

    ```csharp
    [Export(typeof(ISuggestedActionsSourceProvider))]
    [Name("Test Suggested Actions")]
    [ContentType("text")]
    internal class TestSuggestedActionsSourceProvider : ISuggestedActionsSourceProvider
    ```

2. 在源提供程序类中，导入 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 并添加为 属性。

    ```csharp
    [Import(typeof(ITextStructureNavigatorSelectorService))]
    internal ITextStructureNavigatorSelectorService NavigatorService { get; set; }
    ```

3. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider.CreateSuggestedActionsSource%2A> 方法以返回 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> 对象。 下一部分将讨论源。

    ```csharp
    public ISuggestedActionsSource CreateSuggestedActionsSource(ITextView textView, ITextBuffer textBuffer)
    {
        if (textBuffer == null || textView == null)
        {
            return null;
        }
        return new TestSuggestedActionsSource(this, textView, textBuffer);
    }
    ```

## <a name="implement-the-isuggestedactionsource"></a>实现 ISuggestedActionSource
 建议的操作源负责收集一组建议的操作，并将它们添加到正确的上下文中。 在这种情况下，上下文是当前单词，建议的操作是 **UpperCaseSuggestedAction** 和 **LowerCaseSuggestedAction**，下一节将对此进行讨论。

1. 添加实现 **的 TestSuggestedActionsSource** 类 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> 。

    ```csharp
    internal class TestSuggestedActionsSource : ISuggestedActionsSource
    ```

2. 为建议的操作源提供程序、文本缓冲区和文本视图添加专用只读字段。

    ```csharp
    private readonly TestSuggestedActionsSourceProvider m_factory;
    private readonly ITextBuffer m_textBuffer;
    private readonly ITextView m_textView;
    ```

3. 添加用于设置私有字段的构造函数。

    ```csharp
    public TestSuggestedActionsSource(TestSuggestedActionsSourceProvider testSuggestedActionsSourceProvider, ITextView textView, ITextBuffer textBuffer)
    {
        m_factory = testSuggestedActionsSourceProvider;
        m_textBuffer = textBuffer;
        m_textView = textView;
    }
    ```

4. 添加一个私有方法，该方法返回当前位于光标下的单词。 下面的方法查看光标的当前位置，并要求文本结构导航器提供单词的范围。 如果光标位于单词上，则在 out 参数中 <xref:Microsoft.VisualStudio.Text.Operations.TextExtent> 返回 ;否则， `out` 参数为 `null` ，并且 方法返回 `false` 。

    ```csharp
    private bool TryGetWordUnderCaret(out TextExtent wordExtent)
    {
        ITextCaret caret = m_textView.Caret;
        SnapshotPoint point;

        if (caret.Position.BufferPosition > 0)
        {
            point = caret.Position.BufferPosition - 1;
        }
        else
        {
            wordExtent = default(TextExtent);
            return false;
        }

        ITextStructureNavigator navigator = m_factory.NavigatorService.GetTextStructureNavigator(m_textBuffer);

        wordExtent = navigator.GetExtentOfWord(point);
        return true;
    }
    ```

5. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.HasSuggestedActionsAsync%2A> 方法。 编辑器调用此方法来确定是否显示灯泡。 通常进行此调用，例如，每当光标从一行移动到另一行，或鼠标悬停在错误悬停处时。 它是异步的，以便允许在此方法正常工作时执行其他 UI 操作。 在大多数情况下，此方法需要执行当前行的一些分析和分析，因此处理可能需要一些时间。

     在此实现中，它异步获取 并确定区是否重要（如 中一样）是否 <xref:Microsoft.VisualStudio.Text.Operations.TextExtent> 具有空格外的其他文本。

    ```csharp
    public Task<bool> HasSuggestedActionsAsync(ISuggestedActionCategorySet requestedActionCategories, SnapshotSpan range, CancellationToken cancellationToken)
    {
        return Task.Factory.StartNew(() =>
        {
            TextExtent extent;
            if (TryGetWordUnderCaret(out extent))
            {
                // don't display the action if the extent has whitespace
                return extent.IsSignificant;
              }
            return false;
        });
    }
    ```

6. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.GetSuggestedActions%2A> 方法，该方法返回包含 <xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet> 不同对象的 对象的 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction> 数组。 当灯泡展开时，将调用此方法。

    > [!WARNING]
    > 应确保 和 的实现一致;也就是说，如果 返回 `HasSuggestedActionsAsync()` `GetSuggestedActions()` `HasSuggestedActionsAsync()` `true` ， `GetSuggestedActions()` 则应显示一些操作。 在许多情况下， `HasSuggestedActionsAsync()` 在 之前调用 `GetSuggestedActions()` ，但并不总是这样。 例如，如果用户通过按 **Ctrl+** . (调用灯泡操作) 仅 `GetSuggestedActions()` 调用 。

    ```csharp
    public IEnumerable<SuggestedActionSet> GetSuggestedActions(ISuggestedActionCategorySet requestedActionCategories, SnapshotSpan range, CancellationToken cancellationToken)
    {
        TextExtent extent;
        if (TryGetWordUnderCaret(out extent) && extent.IsSignificant)
        {
            ITrackingSpan trackingSpan = range.Snapshot.CreateTrackingSpan(extent.Span, SpanTrackingMode.EdgeInclusive);
            var upperAction = new UpperCaseSuggestedAction(trackingSpan);
            var lowerAction = new LowerCaseSuggestedAction(trackingSpan);
            return new SuggestedActionSet[] { new SuggestedActionSet(new ISuggestedAction[] { upperAction, lowerAction }) };
        }
        return Enumerable.Empty<SuggestedActionSet>();
    }
    ```

7. 定义 `SuggestedActionsChanged` 事件。

    ```csharp
    public event EventHandler<EventArgs> SuggestedActionsChanged;
    ```

8. 若要完成实现，请添加 和 方法 `Dispose()` 的 `TryGetTelemetryId()` 实现。 你不想执行遥测，因此只需返回 `false` GUID，将 GUID 设置为 `Empty` 。

    ```csharp
    public void Dispose()
    {
    }

    public bool TryGetTelemetryId(out Guid telemetryId)
    {
        // This is a sample provider and doesn't participate in LightBulb telemetry
        telemetryId = Guid.Empty;
        return false;
    }
    ```

## <a name="implement-light-bulb-actions"></a>实现灯泡操作

1. 在项目中，添加对Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime.dll的引用，将 **"复制***本地"* 设置为 `False` 。

2. 创建两个类，第一个名为 `UpperCaseSuggestedAction` ，第二个名为 `LowerCaseSuggestedAction`。 两个类都实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction>。

    ```csharp
    internal class UpperCaseSuggestedAction : ISuggestedAction
    internal class LowerCaseSuggestedAction : ISuggestedAction
    ```

     这两个类相似，只不过其中一个调用 <xref:System.String.ToUpper%2A>，另一个调用 <xref:System.String.ToLower%2A>。 以下步骤仅说明大写操作类，但你必须实现这两个类。 将实现大写操作的步骤用作实现小写操作的模式。

3. 为这些类添加以下 using 指令：

    ```csharp
    using Microsoft.VisualStudio.Imaging.Interop;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Documents;
    using System.Windows.Media;

    ```

4. 声明一组私有字段。

    ```csharp
    private ITrackingSpan m_span;
    private string m_upper;
    private string m_display;
    private ITextSnapshot m_snapshot;
    ```

5. 添加设置该字段的构造函数。

    ```csharp
    public UpperCaseSuggestedAction(ITrackingSpan span)
    {
        m_span = span;
        m_snapshot = span.TextBuffer.CurrentSnapshot;
        m_upper = span.GetText(m_snapshot).ToUpper();
        m_display = string.Format("Convert '{0}' to upper case", span.GetText(m_snapshot));
    }
    ```

6. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetPreviewAsync%2A> 方法，以便它显示操作预览。

    ```csharp
    public Task<object> GetPreviewAsync(CancellationToken cancellationToken)
    {
        var textBlock = new TextBlock();
        textBlock.Padding = new Thickness(5);
        textBlock.Inlines.Add(new Run() { Text = m_upper });
        return Task.FromResult<object>(textBlock);
    }
    ```

7. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetActionSetsAsync%2A> 方法，以便返回空 <xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet> 枚举。

    ```csharp
    public Task<IEnumerable<SuggestedActionSet>> GetActionSetsAsync(CancellationToken cancellationToken)
    {
        return Task.FromResult<IEnumerable<SuggestedActionSet>>(null);
    }
    ```

8. 如下所示实现属性。

    ```csharp
    public bool HasActionSets
    {
        get { return false; }
    }
    public string DisplayText
    {
        get { return m_display; }
    }
    public ImageMoniker IconMoniker
    {
       get { return default(ImageMoniker); }
    }
    public string IconAutomationText
    {
        get
        {
            return null;
        }
    }
    public string InputGestureText
    {
        get
        {
            return null;
        }
    }
    public bool HasPreview
    {
        get { return true; }
    }
    ```

9. 通过将范围中的文本替换为其大写形式来实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.Invoke%2A> 方法。

    ```csharp
    public void Invoke(CancellationToken cancellationToken)
    {
        m_span.TextBuffer.Replace(m_span.GetSpan(m_snapshot), m_upper);
    }
    ```

    > [!WARNING]
    > 灯泡操作 **Invoke** 方法不应显示 UI。 如果操作确实显示新的 UI (例如预览或选择对话框) ，则不要直接从 **Invoke** 方法中显示 UI，而是计划从 Invoke 返回后显示 **UI。**

10. 若要完成实现，请添加 `Dispose()` 和 `TryGetTelemetryId()` 方法。

    ```csharp
    public void Dispose()
    {
    }

    public bool TryGetTelemetryId(out Guid telemetryId)
    {
        // This is a sample action and doesn't participate in LightBulb telemetry
        telemetryId = Guid.Empty;
        return false;
    }
    ```

11. 不要忘记执行相同的工作，将显示文本更改为"将 ' ' 转换为小写 `LowerCaseSuggestedAction` {0} "和 <xref:System.String.ToUpper%2A> 调用 <xref:System.String.ToLower%2A> 。

## <a name="build-and-test-the-code"></a>生成并测试代码
 若要测试此代码，请生成 LightBulbTest 解决方案，并运行它在实验实例中。

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动第二Visual Studio实例。

3. 创建一个文本文件并键入一些文本。 文本左侧应显示一个灯泡。

     ![测试灯泡](../extensibility/media/testlightbulb.png "TestLIghtBulb")

4. 指向灯泡。 应会看到向下箭头。

5. 单击灯泡时，应显示两个建议的操作，以及所选操作预览。

     ![测试灯泡，已展开](../extensibility/media/testlightbulbexpanded.gif "TestLIghtBulbExpanded")

6. 如果单击第一个操作，则当前单词的所有文本都应转换为大写。 如果单击第二个操作，则所有文本都应转换为小写。
