---
title: 演练：显示签名帮助|Microsoft Docs
description: 了解如何使用此演练显示文本内容类型的签名帮助。 签名帮助在工具提示中显示方法的签名。
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
ms.openlocfilehash: d4c8e69c261b25a4f3a425fc11eb8ccd259dbad2bf951f980e985163a23b4d0d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121374619"
---
# <a name="walkthrough-display-signature-help"></a>演练：显示签名帮助
签名 (也称为参数 *信息) 当用户* 在工具提示中输入参数列表开始字符时，在工具提示中显示方法的签名 (通常是一个) 。 作为参数和参数分隔符 (键入逗号) ，工具提示会更新为以粗体显示下一个参数。 可以按照以下方式定义签名帮助：在语言服务的上下文中，定义自己的文件扩展名和内容类型，仅显示该类型的签名帮助，或显示现有内容类型的签名帮助 (例如"text") 。 本演练演示如何显示"文本"内容类型的签名帮助。

 签名帮助通常通过键入特定字符（例如" (" (右括号) ）触发，然后通过键入另一个字符（例如，") " (右括号) ）来消除签名帮助。 通过键入字符触发的 IntelliSense 功能可以通过对接口) 的击键使用命令处理程序 (以及实现 接口的处理程序提供程序来实现。 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> 若要创建签名帮助源（即参与签名帮助的签名列表），请实现 接口和运行 接口 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> 的源 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> 提供程序。 提供程序是Managed Extensibility Framework (MEF) 组件部件，负责导出源和控制器类以及导入服务和代理（例如 ，允许导航到文本缓冲区中的 ）和 （触发签名帮助会话）。 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>

 本演练演示如何为一组硬编码标识符设置签名帮助。 在完整实现中，语言负责提供该内容。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="creating-a-mef-project"></a>创建 MEF 项目

#### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建 C# VSIX 项目。  ("**新建** Project对话框中，选择 **"Visual C#/** 扩展性"，然后选择 **"VSIX Project**.) 将解决方案命名 `SignatureHelpTest` "。

2. 向项目添加编辑器分类器项模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

4. 将以下引用添加到项目，并确保 **CopyLocal** 设置为 `false` ：

     Microsoft.VisualStudio.Editor

     Microsoft.VisualStudio.Language.Intellisense

     Microsoft.VisualStudio.OLE.Interop

     Microsoft.VisualStudio.Shell.14.0

     Microsoft.VisualStudio.TextManager.Interop

## <a name="implement-signature-help-signatures-and-parameters"></a>实现签名帮助签名和参数
 签名帮助源基于实现 的签名， <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> 其中每个签名都包含实现 的参数 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> 。 在完整实现中，此信息会从语言文档获取，但此示例中，签名是硬编码的。

#### <a name="to-implement-the-signature-help-signatures-and-parameters"></a>实现签名帮助签名和参数

1. 添加一个类文件并将其命名为 `SignatureHelpSource`。

2. 添加以下 import 语句。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet1":::

3. 添加实现 的 `TestParameter` 名为 的类 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet2":::

4. 添加一个构造函数，用于设置所有属性。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet3":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet3":::

5. 添加 的属性 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet4":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet4":::

6. 添加实现 的 `TestSignature` 名为 的类 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet5":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet5":::

7. 添加一些专用字段。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet6":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet6":::

8. 添加一个构造函数，用于设置字段并订阅 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> 事件。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet7":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet7":::

9. 声明 `CurrentParameterChanged` 事件。 当用户在签名中填充其中一个参数时，将引发此事件。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet8":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet8":::

10. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A> 属性，以便当 `CurrentParameterChanged` 属性值更改时引发 事件。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet9":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet9":::

11. 添加引发 事件 `CurrentParameterChanged` 的方法。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet10":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet10":::

12. 添加一个方法，该方法通过将 中的逗号数与签名中的 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> 逗号数进行比较来计算当前参数。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet11":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet11":::

13. 为调用 方法 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> 的事件添加事件 `ComputeCurrentParameter()` 处理程序。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet12":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet12":::

14. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> 属性。 此属性包含 <xref:Microsoft.VisualStudio.Text.ITrackingSpan> 一个 ，它对应于应用签名的缓冲区中的文本范围。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet13":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet13":::

15. 实现其他参数。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet14":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet14":::

## <a name="implement-the-signature-help-source"></a>实现签名帮助源
 签名帮助源是一组你提供相关信息的签名。

#### <a name="to-implement-the-signature-help-source"></a>实现签名帮助源

1. 添加实现 的 `TestSignatureHelpSource` 名为 的类 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet15":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet15":::

2. 添加对文本缓冲区的引用。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet16":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet16":::

3. 添加一个构造函数，用于设置文本缓冲区和签名帮助源提供程序。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet17":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet17":::

4. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> 方法。 此示例中，签名是硬编码的，但在完整实现中，你会从语言文档中获取此信息。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet18":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet18":::

5. 提供帮助程序 `CreateSignature()` 方法只是为了进行演示。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet19":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet19":::

6. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> 方法。 此示例中只有两个签名，每个签名都有两个参数。 因此，此方法不是必需的。 在具有多个签名帮助源的更完整实现中，此方法用于确定最高优先级的签名帮助源是否可以提供匹配的签名。 如果无法，该方法将返回 null，并且要求下一个优先级最高的源提供匹配项。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet20":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet20":::

7. 实现 `Dispose()` 方法：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet21":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet21":::

## <a name="implement-the-signature-help-source-provider"></a>实现签名帮助源提供程序
 签名帮助源提供程序负责导出 MEF Managed Extensibility Framework (组件) 签名帮助源。

#### <a name="to-implement-the-signature-help-source-provider"></a>实现签名帮助源提供程序

1. 添加实现 的名为 的类，然后使用 `TestSignatureHelpSourceProvider` <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 、"text"的 和 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> Before="default"的 导出它。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet22":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet22":::

2. 通过 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A> 实例化 来实现 `TestSignatureHelpSource` 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet23":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet23":::

## <a name="implement-the-command-handler"></a>实现命令处理程序
 签名帮助通常由右括号" ("字符触发，由右括号") "字符消除。 可以通过运行 来处理这些击键，以便它收到前面带有已知方法名称的开始括号字符时触发签名帮助会话，并接收右括号字符时关闭会话。 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>

#### <a name="to-implement-the-command-handler"></a>实现命令处理程序

1. 添加实现 的 `TestSignatureHelpCommand` 名为 的类 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet24":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet24":::

2. 为适配器添加专用字段 (这样一来，可以将命令处理程序添加到命令 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 处理程序链) 、文本视图、签名帮助代理和会话、和下一个 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet25":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet25":::

3. 添加构造函数以初始化这些字段，以及将命令筛选器添加到命令筛选器链。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet26":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet26":::

4. 实现 方法，在命令筛选器在已知方法名称之一后收到一个开始括号" ("字符时触发签名帮助会话，在会话仍处于活动状态时收到右括号 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> ") "字符时关闭会话。 在每种情况下，都会转发命令。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet27":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet27":::

5. 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法，以便它始终转发命令。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet28":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet28":::

## <a name="implement-the-signature-help-command-provider"></a>实现签名帮助命令提供程序
 可以通过实现 来提供 Signature Help 命令，以在文本视图创建时实例化 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> 命令处理程序。

### <a name="to-implement-the-signature-help-command-provider"></a>实现签名帮助命令提供程序

1. 添加一个名为 `TestSignatureHelpController` 的类，该类实现 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> ，然后使用 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 、 和 导出 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> 它。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet29":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet29":::

2. 导入用于 (的 、给定对象) 、用于查找当前单词) 的 (以及用于触发签名帮助会话的 (<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>) 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet30":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet30":::

3. 通过 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A> 实例化 来实现 方法 `TestSignatureCommandHandler` 。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet31":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet31":::

## <a name="build-and-test-the-code"></a>生成和测试代码
 若要测试此代码，请生成 SignatureHelpTest 解决方案，并运行它在实验实例中。

#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>生成和测试 SignatureHelpTest 解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动第二Visual Studio实例。

3. 创建文本文件并键入一些文本，其中包括单词"add"和一个开始括号。

4. 键入开始括号后，应会看到一个工具提示，其中显示了方法的两个签名 `add()` 的列表。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
