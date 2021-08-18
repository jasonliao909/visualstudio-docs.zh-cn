---
title: 演练：显示签名帮助 |Microsoft Docs
description: 了解如何使用本演练显示文本内容类型的签名帮助。 签名帮助在工具提示中显示方法的签名。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - signature help/parameter info
ms.assetid: 4a6a884b-5730-4b54-9264-99684f5b523c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b1f7685f54daeb2c2299b5b6866295fce4bafd79
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122144179"
---
# <a name="walkthrough-display-signature-help"></a>演练：显示签名帮助
签名帮助 (也称为 *参数信息*) 当用户键入参数列表开始字符时，将在工具提示中显示方法的签名， (通常为左括号) 。 作为参数和参数分隔符 (通常会键入逗号) ，工具提示将更新以以粗体显示下一个参数。 可以通过以下方式定义签名帮助：在语言服务的上下文中，定义自己的文件扩展名和内容类型，并为现有内容类型显示签名帮助 (例如，"text" ) 。 本演练演示如何为 "文本" 内容类型显示签名帮助。

 签名帮助通常是通过键入特定字符来触发的，例如 " (" (左括号) ，并通过键入另一个字符来消除，如 ") " (右括号) 。 通过使用命令处理程序 (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口) 和实现接口的处理程序提供程序，可以实现通过键入字符触发的 IntelliSense 功能 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> 。 若要创建签名帮助源（参与签名帮助的签名列表），请实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> 接口和运行接口的源提供程序 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> 。 提供程序 Managed Extensibility Framework (MEF) 组件部件，并负责导出源和控制器类，以及导入服务和代理，例如，可 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 让你在文本缓冲区中导航，并将 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> 触发签名帮助会话。

 本演练演示如何为硬编码的标识符集设置签名帮助。 在完整实现中，语言负责提供该内容。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，你不会从下载中心安装 Visual Studio 的 SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 也可稍后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="creating-a-mef-project"></a>创建 MEF 项目

#### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建 c # VSIX 项目。  (在 "**新建 Project** " 对话框中，依次选择 " **Visual c #/扩展性**"、" **VSIX Project**"。 ) `SignatureHelpTest` 将解决方案命名为。

2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

4. 将以下引用添加到项目，并确保 **CopyLocal** 设置为 `false` ：

     VisualStudio

     Microsoft.VisualStudio.Language.Intellisense

     VisualStudio。

     VisualStudio。14。0

     VisualStudio. TextManager

## <a name="implement-signature-help-signatures-and-parameters"></a>实现签名帮助签名和参数
 签名帮助源基于实现的签名 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> ，其中每个都包含实现的参数 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> 。 在完整的实现中，将从语言文档中获取此信息，但在此示例中，签名是硬编码的。

#### <a name="to-implement-the-signature-help-signatures-and-parameters"></a>实现签名帮助签名和参数

1. 添加一个类文件并将其命名为 `SignatureHelpSource`。

2. 添加以下 import 语句。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet1":::

3. 添加一个名为 `TestParameter` 的类，该类实现 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet2":::

4. 添加设置所有属性的构造函数。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet3":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet3":::

5. 添加的属性 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet4":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet4":::

6. 添加一个名为 `TestSignature` 的类，该类实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet5":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet5":::

7. 添加一些私有字段。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet6":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet6":::

8. 添加一个构造函数，该构造函数设置字段并订阅 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> 事件。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet7":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet7":::

9. 声明 `CurrentParameterChanged` 事件。 当用户填写签名中的一个参数时，将引发此事件。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet8":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet8":::

10. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A> 属性，以便 `CurrentParameterChanged` 在属性值更改时引发事件。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet9":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet9":::

11. 添加引发事件的方法 `CurrentParameterChanged` 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet10":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet10":::

12. 添加一个方法，该方法通过将中的逗号数 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> 与签名中的逗号数进行比较来计算当前参数。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet11":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet11":::

13. 为调用方法的事件添加事件处理程序 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> `ComputeCurrentParameter()` 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet12":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet12":::

14. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> 属性。 此属性包含与 <xref:Microsoft.VisualStudio.Text.ITrackingSpan> 签名应用到的缓冲区中的文本范围相对应的。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet13":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet13":::

15. 实现其他参数。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet14":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet14":::

## <a name="implement-the-signature-help-source"></a>实现签名帮助源
 签名帮助源是您提供信息的一组签名。

#### <a name="to-implement-the-signature-help-source"></a>实现签名帮助源

1. 添加一个名为 `TestSignatureHelpSource` 的类，该类实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet15":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet15":::

2. 添加对文本缓冲区的引用。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet16":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet16":::

3. 添加一个构造函数，用于设置文本缓冲区和签名帮助源提供程序。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet17":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet17":::

4. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> 方法。 在此示例中，签名是硬编码的，但在完整实现中，你将从语言文档中获取此信息。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet18":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet18":::

5. `CreateSignature()`仅为说明提供帮助器方法。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet19":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet19":::

6. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> 方法。 在此示例中，只有两个签名，其中每个都有两个参数。 因此，此方法不是必需的。 在更完整的实现中，有多个签名帮助源可用时，此方法用于确定最高优先级的签名帮助源是否可提供匹配的签名。 如果无法实现，该方法将返回 null，并要求下一个最高优先级的源提供匹配项。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet20":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet20":::

7. 实现 `Dispose()` 方法：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet21":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet21":::

## <a name="implement-the-signature-help-source-provider"></a>实现签名帮助源提供程序
 签名帮助源提供程序负责导出 Managed Extensibility Framework (MEF) 组件部件和实例化签名帮助源。

#### <a name="to-implement-the-signature-help-source-provider"></a>实现签名帮助源提供程序

1. 添加一个名为的名为的类， `TestSignatureHelpSourceProvider` <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> 并将其导出为 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 、一个为 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "text"，并将指定为 <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> Before = "default"。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet22":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet22":::

2. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A>通过实例化实现 `TestSignatureHelpSource` 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet23":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet23":::

## <a name="implement-the-command-handler"></a>实现命令处理程序
 签名帮助通常由左括号 " (" 字符触发，并由右括号 ") " 字符消除。 你可以通过运行来处理这些击键 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ，使其在收到一个带有已知方法名称的左括号字符时触发签名帮助会话，并在收到右括号字符时关闭会话。

#### <a name="to-implement-the-command-handler"></a>实现命令处理程序

1. 添加一个名为 `TestSignatureHelpCommand` 的类，该类实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet24":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet24":::

2. 为适配器 (添加私有字段 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ，该字段允许你将命令处理程序添加到命令处理程序链，) ，文本视图，签名帮助代理和会话， <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> ，以及下一步 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet25":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet25":::

3. 添加构造函数以初始化这些字段并将命令筛选器添加到命令筛选器链。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet26":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet26":::

4. 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法，以便在命令筛选器接收到一个已知方法名称后的左括号 " (" 字符时触发签名帮助会话，并在会话仍处于活动状态的情况下，在收到右括号 ") " 字符时关闭会话。 在每种情况下，都将转发该命令。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet27":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet27":::

5. 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法，以便始终转发命令。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet28":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet28":::

## <a name="implement-the-signature-help-command-provider"></a>实现签名帮助命令提供程序
 可以通过实现来提供签名帮助命令 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> ，以便在创建文本视图时实例化命令处理程序。

### <a name="to-implement-the-signature-help-command-provider"></a>实现签名帮助命令提供程序

1. 添加一个名为 `TestSignatureHelpController` 的类，该类实现 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> 并将其与 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 、和一起导出 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet29":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet29":::

2. 导入 <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> 用于获取的 (<xref:Microsoft.VisualStudio.Text.Editor.ITextView> ，给定 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 对象) 、 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 用于查找当前单词) 的 (和用于 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> 触发签名帮助会话 (的) 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet30":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet30":::

3. <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>通过实例化实现方法 `TestSignatureCommandHandler` 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet31":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet31":::

## <a name="build-and-test-the-code"></a>生成和测试代码
 若要测试此代码，请生成 SignatureHelpTest 解决方案并在实验实例中运行它。

#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>生成和测试 SignatureHelpTest 解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建一个文本文件并键入一些文本，其中包含单词 "add" 加上一个左括号。

4. 键入左括号后，应该会看到工具提示，其中显示了该方法的两个签名的列表 `add()` 。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
