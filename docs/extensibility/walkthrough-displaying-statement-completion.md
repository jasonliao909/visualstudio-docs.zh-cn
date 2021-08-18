---
title: 演练：显示语句完成|Microsoft Docs
description: 了解如何使用此演练为纯文本内容实现基于语言的语句完成。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - statement completion
ms.assetid: f3152c4e-7673-4047-a079-2326941d1c83
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: 8dfea0b39cfeaccd01bde21d838a8f611a6b009a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122049033"
---
# <a name="walkthrough-display-statement-completion"></a>演练：显示语句完成
可以通过定义要提供完成项的标识符，然后触发完成会话来实现基于语言的语句完成。 可以在语言服务的上下文中定义语句完成，定义自己的文件扩展名和内容类型，然后仅显示该类型的完成。 或者，可以触发现有内容类型（例如"纯文本"）的完成。 本演练演示如何为"纯文本"内容类型（文本文件的内容类型）触发语句完成。 "text"内容类型是所有其他内容类型的上级，包括代码和 XML 文件。

 语句完成通常是通过键入某些字符触发的，例如，键入标识符的开头，例如"using"。 它通常通过按空格键 **、Tab** 或 **Enter** 键来提交选定内容来消除。 可以通过为接口) 的击键使用命令处理程序和实现 接口的处理程序提供程序 (键入字符时触发的 IntelliSense 功能 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> 。 若要创建完成源（参与完成的标识符列表），请实现 接口和完成源提供程序 (<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider> 接口) 。 这些提供程序Managed Extensibility Framework (MEF) 组件部件。 它们负责导出源和控制器类以及导入服务和代理（例如，在文本缓冲区中启用导航的 ）和 （ <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker> 触发完成会话）。

 本演练演示如何为一组硬编码的标识符实现语句完成。 在完整实现中，语言服务和语言文档负责提供该内容。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-a-mef-project"></a>创建 MEF Project

#### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建 C# VSIX 项目。  ("**新建** Project对话框中，选择 **"Visual C#/** 扩展性"，然后选择 **"VSIX Project**.) 将解决方案命名 `CompletionTest` "。

2. 向项目添加编辑器分类器项模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

4. 添加对项目的以下引用，并确保 **CopyLocal** 设置为 `false` ：

     Microsoft.VisualStudio.Editor

     Microsoft.VisualStudio.Language.Intellisense

     Microsoft.VisualStudio.OLE.Interop

     Microsoft.VisualStudio.Shell.15.0

     Microsoft.VisualStudio.Shell.Immutable.10.0

     Microsoft.VisualStudio.TextManager.Interop

## <a name="implement-the-completion-source"></a>实现完成源
 完成源负责收集标识符集，以及当用户类型完成触发器（如标识符的第一个字母）时将内容添加到完成窗口。 此示例在 方法中对标识符及其说明进行硬 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A> 编码。 在大多数实际使用中，你将使用语言分析器获取令牌以填充完成列表。

### <a name="to-implement-the-completion-source"></a>实现完成源

1. 添加一个类文件并将其命名为 `TestCompletionSource`。

2. 添加以下导入：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet1":::

3. 修改 的类 `TestCompletionSource` 声明，以便它实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> ：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet2":::

4. 为源提供程序、文本缓冲区和对象列表添加私有字段 (这些对象对应于将参与完成会话的 <xref:Microsoft.VisualStudio.Language.Intellisense.Completion>) ：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet3":::

5. 添加一个构造函数，用于设置源提供程序和缓冲区。 类 `TestCompletionSourceProvider` 在稍后的步骤中定义：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet4":::

6. 通过 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A> 添加包含你想要在上下文中提供的完成项的完成集来实现 方法。 每个完成集都包含一组 <xref:Microsoft.VisualStudio.Language.Intellisense.Completion> 完成，对应于完成窗口的选项卡。  (在Visual Basic中，完成窗口选项卡命名为"通用"和"所有 .) 下一步 `FindTokenSpanAtPosition` 中定义 方法。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet5":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet5":::

7. 以下方法用于从光标位置查找当前单词：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet6":::

8. 实现 `Dispose()` 方法：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet7":::

## <a name="implement-the-completion-source-provider"></a>实现完成源提供程序
 完成源提供程序是实例化完成源的 MEF 组件部分。

### <a name="to-implement-the-completion-source-provider"></a>实现完成源提供程序

1. 添加实现 的 `TestCompletionSourceProvider` 名为 的类 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider> 。 使用"纯文本" <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> 和"测试完成" <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 导出此类。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet8":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet8":::

2. 导入 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> ，它查找完成源中的当前单词。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet9":::

3. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider.TryCreateCompletionSource%2A> 方法以实例化完成源。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet10":::

## <a name="implement-the-completion-command-handler-provider"></a>实现完成命令处理程序提供程序
 完成命令处理程序提供程序派生自 ，它侦听文本视图创建事件，并将视图从 转换为 （这允许将命令加到 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> Visual Studio shell 的命令链 <xref:Microsoft.VisualStudio.Text.Editor.ITextView> ）。 由于此类是 MEF 导出，因此还可使用它导入命令处理程序本身所需的服务。

#### <a name="to-implement-the-completion-command-handler-provider"></a>实现完成命令处理程序提供程序

1. 添加名为 的文件 `TestCompletionCommandHandler` 。

2. 添加以下 using 指令：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet11":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet11":::

3. 添加实现 的 `TestCompletionHandlerProvider` 名为 的类 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> 。 使用 "标记 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 完成处理程序"、 "纯文本"和 的 导出 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> 此类 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Editable> 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet12":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet12":::

4. 导入 <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> ，它支持从 转换为 、、 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> ，从而 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker> <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> 允许访问标准Visual Studio服务。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet13":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet13":::

5. 实现 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A> 方法以实例化命令处理程序。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet14":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet14":::

## <a name="implement-the-completion-command-handler"></a>实现完成命令处理程序
 由于语句完成由击键触发，因此必须实现 接口以接收并处理触发、提交和关闭完成会话的 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 击键。

#### <a name="to-implement-the-completion-command-handler"></a>实现完成命令处理程序

1. 添加一个名为 `TestCompletionCommandHandler` 的类，该类实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ：

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet15":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet15":::

2. 为下一个命令处理程序添加专用字段 (将命令) 、文本视图、命令处理程序提供程序 (用于访问各种服务) 和完成会话：

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet16":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet16":::

3. 添加一个构造函数，用于设置文本视图和提供程序字段，并将 命令添加到命令链：

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet17":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet17":::

4. 通过 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 传递 命令来实现 方法：

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet18":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet18":::

5. 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法。 此方法收到击键时，必须执行以下操作之一：

   - 允许将字符写入缓冲区，然后触发或筛选完成。  (打印字符会这样做。) 

   - 提交完成，但不允许将字符写入缓冲区。  ("空格 **"、"Tab"** 和 **"Enter"** 在显示完成会话时) 

   - 允许将命令传递给下一个处理程序。  (所有其他命令.) 

     由于此方法可能会显示 UI，因此请调用 以确保不在自动化 <xref:Microsoft.VisualStudio.Shell.VsShellUtilities.IsInAutomationFunction%2A> 上下文中调用它：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet19":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet19":::

6. 此代码是触发完成会话的私有方法：

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet20":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet20":::

7. 下一个示例是取消订阅 事件的私有 <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSession.Dismissed> 方法：

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet21":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet21":::

## <a name="build-and-test-the-code"></a>生成并测试代码
 若要测试此代码，请生成 CompletionTest 解决方案，并运行它在实验实例中。

#### <a name="to-build-and-test-the-completiontest-solution"></a>生成和测试 CompletionTest 解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动第二Visual Studio实例。

3. 创建文本文件并键入一些包含单词"add"的文本。

4. 键入"a"后键入"d"时，应显示包含"加法"和"适应"的列表。 请注意，已选择"添加"。 键入另一个"d"时，列表应仅包含"加法"，此时已选中。 可以通过按空格键、Tab 或 **Enter** 键来提交"加法"，或者通过键入 Esc 或其他任何键来关闭列表。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
