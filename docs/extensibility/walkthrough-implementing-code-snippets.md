---
title: 演练：实现代码片段|Microsoft Docs
description: 可以创建代码片段，将其包括在编辑器扩展中。 了解如何使用此演练创建/注册代码片段。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: adbc5382-d170-441c-9fd0-80faa1816478
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: 106339c932b0339542fd184675448b8ec8354bf0618fbddc7e351ab11763a289
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121234754"
---
# <a name="walkthrough-implement-code-snippets"></a>演练：实现代码片段
可以创建代码片段，并将其添加到编辑器扩展中，以便扩展的用户可以将其添加到其自己的代码中。

 代码片段是代码片段或可合并到文件的其他文本片段。 若要查看已注册特定编程语言的所有代码片段，请在"工具"菜单上单击"代码 **片段管理器"。** 若要在文件中插入代码片段，请右键单击需要代码段的位置，单击"插入代码段"或" **外** 带"，找到需要的代码片段，然后双击它。 按 **Tab** 或 **Shift** + **Tab** 修改代码片段的相关部分，然后按 **Enter** 或 **Esc** 接受它。 有关详细信息，请参阅 [代码片段](../ide/code-snippets.md)。

 代码片段包含在扩展名为 .snippet* 的 XML 文件中。 代码片段可以包含插入代码片段后突出显示的字段，以便用户可以查找和更改它们。 代码片段文件还提供代码片段 **管理器** 的信息，以便它可以在正确的类别中显示代码片段名称。 有关代码片段架构的信息，请参阅 [代码片段架构参考](../ide/code-snippets-schema-reference.md)。

 本演练将指导如何完成以下任务：

1. 创建并注册特定语言的代码片段。

2. 将" **插入代码片段** "命令添加到快捷菜单。

3. 实现代码片段扩展。

   本演练基于演练 [：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-and-register-code-snippets"></a>创建和注册代码片段
 通常，代码片段与已注册的语言服务相关联。 但是，不需要实现 来 <xref:Microsoft.VisualStudio.Package.LanguageService> 注册代码片段。 只需在代码片段索引文件中指定 GUID，然后在添加到项目的 中使用相同的 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> GUID。

 以下步骤演示如何创建代码片段并将其与特定 GUID 关联。

1. 创建以下目录结构：

    **%InstallDir%\TestSnippets\Snippets\1033\\**

    其中 *%InstallDir%* 是Visual Studio文件夹。  (尽管此路径通常用于安装代码片段，但可以指定任何 path.) 

2. 在 \1033\ 文件夹中，创建 *一.xml* 文件，并命名 **TestSnippets.xml。**  (尽管此名称通常用于代码段索引文件，但只要其文件扩展名为 *.xml，* 就可以指定任何名称。) 添加以下文本，然后删除占位符 GUID 并添加你自己的名称。

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <SnippetCollection>
       <Language Lang="TestSnippets" Guid="{00000000-0000-0000-0000-000000000000}">
           <SnippetDir>
               <OnOff>On</OnOff>
               <Installed>true</Installed>
               <Locale>1033</Locale>
               <DirPath>%InstallRoot%\TestSnippets\Snippets\%LCID%\</DirPath>
               <LocalizedName>Snippets</LocalizedName>
           </SnippetDir>
       </Language>
   </SnippetCollection>
   ```

3. 在代码片段文件夹中创建文件，将其命名 **测试** `.snippet` ，然后添加以下文本：

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
       <CodeSnippet Format="1.0.0">
           <Header>
               <Title>Test replacement fields</Title>
               <Shortcut>test</Shortcut>
               <Description>Code snippet for testing replacement fields</Description>
               <Author>MSIT</Author>
               <SnippetTypes>
                   <SnippetType>Expansion</SnippetType>
               </SnippetTypes>
           </Header>
           <Snippet>
               <Declarations>
                   <Literal>
                     <ID>param1</ID>
                       <ToolTip>First field</ToolTip>
                       <Default>first</Default>
                   </Literal>
                   <Literal>
                       <ID>param2</ID>
                       <ToolTip>Second field</ToolTip>
                       <Default>second</Default>
                   </Literal>
               </Declarations>
               <References>
                  <Reference>
                      <Assembly>System.Windows.Forms.dll</Assembly>
                  </Reference>
               </References>
               <Code Language="TestSnippets">
                   <![CDATA[MessageBox.Show("$param1$");
        MessageBox.Show("$param2$");]]>
               </Code>
           </Snippet>
       </CodeSnippet>
   </CodeSnippets>
   ```

   以下步骤显示如何注册代码片段。

### <a name="to-register-code-snippets-for-a-specific-guid"></a>为特定 GUID 注册代码片段

1. 打开 **CompletionTest** 项目。 若要了解如何创建此项目，请参阅 [演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)。

2. 在 项目中，添加对以下程序集的引用：

    - Microsoft.VisualStudio.TextManager.Interop

    - Microsoft.VisualStudio.TextManager.Interop.8.0

    - microsoft.msxml

3. 在项目中，打开 **source.extension.vsixmanifest** 文件。

4. 确保"**资产"** 选项卡包含 **VsPackage** 内容类型，Project **设置为项目** 名称。

5. 选择 CompletionTest 项目，然后 **属性窗口"生成 Pkgdef 文件"** 设置为 **true。** 保存项目。

6. 向项目 `SnippetUtilities` 添加静态类。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet22":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet22":::

7. 在 SnippetUtilities 类中，定义 GUID，并赋予它在SnippetsIndex.xml *中使用的值* 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet23":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet23":::

8. 将 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> 添加到 `TestCompletionHandler` 类。 此属性可以添加到项目中任何公共或 (非静态) 类。  (可能需要为 `using` Microsoft.VisualStudio.Shell namespace.) 

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet24":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet24":::

9. 生成并运行该项目。 在运行项目Visual Studio启动的试验实例中，刚刚注册的代码片段应显示在 **TestSnippets** 语言下的"代码片段管理器"中。

## <a name="add-the-insert-snippet-command-to-the-shortcut-menu"></a>将"插入代码片段"命令添加到快捷菜单
 文本文件 **的** 快捷菜单不包含"插入代码片段"命令。 因此，必须启用 命令。

#### <a name="to-add-the-insert-snippet-command-to-the-shortcut-menu"></a>将"插入代码片段"命令添加到快捷菜单

1. 打开 `TestCompletionCommandHandler` 类文件。

     由于此类实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ，因此可以在 方法中激活 Insert **Snippet** <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 命令。 在启用命令之前，请检查是否未在自动化函数中调用此方法，因为单击"插入代码段"命令时，它会在 UI (显示代码片段) 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet25":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet25":::

2. 生成并运行该项目。 在实验实例中，打开扩展名为 *.zzz* 的文件，然后右键单击该文件中的任意位置。 " **插入代码** 片段"命令应显示在快捷菜单上。

## <a name="implement-snippet-expansion-in-the-snippet-picker-ui"></a>在代码片段选取器 UI 中实现代码片段扩展
 本部分演示如何实现代码片段扩展，以便单击快捷菜单上的"插入代码段"时显示代码片段选取器 UI。 当用户输入代码片段快捷方式，然后按 Tab 时，代码片段也会 **展开**。

 若要显示代码片段选取器 UI 并启用导航和插入后代码片段接受，请使用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法。 插入本身由 方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> 处理。

 代码片段扩展的实现使用旧 <xref:Microsoft.VisualStudio.TextManager.Interop> 接口。 从当前编辑器类转换为旧代码时，请记住，旧接口使用行号和列号的组合来指定文本缓冲区中的位置，但当前类使用一个索引。 因此，如果缓冲区有三行，每行包含 10 个字符 (加上一个换行符（计为一个字符) ）时，第三行的第四个字符在当前实现中位于位置 27，但它位于旧实现中第 2 行的位置 3。

#### <a name="to-implement-snippet-expansion"></a>实现代码片段扩展

1. 将以下 指令添加到包含 `TestCompletionCommandHandler` 类 `using` 的 文件中。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet26":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet26":::

2. 使 `TestCompletionCommandHandler` 类实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient> 接口。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet27":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet27":::

3. 在 类 `TestCompletionCommandHandlerProvider` 中，导入 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet28":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet28":::

4. 为代码扩展接口和 添加一些私有字段 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet29":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet29":::

5. 在 类的构造函数 `TestCompletionCommandHandler` 中，设置以下字段。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet30":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet30":::

6. 若要在用户单击"插入代码段"命令时显示代码片段选取器，请将以下代码添加到 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法。  (使此说明更具可读性，不会显示用于语句完成的代码;相反，代码块将添加到现有方法。) 在检查字符的代码后添加以下代码块。 `Exec()`

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet31":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet31":::

7. 如果代码片段包含可导航的字段，则扩展会话将保持打开状态，直到显式接受扩展;如果代码片段没有字段，则会话将关闭，并且由 `null` 方法作为 返回 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.InvokeInsertionUI%2A> 。 在 方法中，在上一步骤中添加的代码片段选取器 UI 代码之后，添加以下代码以处理代码片段导航 (当用户在插入代码片段后按 Tab 或 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> **Shift** + **选项卡** 时) 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet32":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet32":::

8. 若要在用户输入相应的快捷方式，然后按 **Tab** 时插入代码片段，请将代码添加到 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法。 插入代码片段的私有方法将在稍后的步骤中显示。 在上一步中添加的导航代码后添加以下代码。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet33":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet33":::

9. 实现 接口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient> 的方法。 在此实现中，唯一感兴趣的方法是 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.EndExpansion%2A> 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> 。 其他方法应只返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet34":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet34":::

10. 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> 方法。 稍后的步骤将介绍实际插入扩展的帮助器方法。 <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan>提供行和列信息，可以从 获取 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 这些信息。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet35":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet35":::

11. 以下专用方法基于快捷方式或标题和路径插入代码片段。 然后，它 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansion.InsertNamedExpansion%2A> 使用代码片段调用 方法。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet36":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet36":::

## <a name="build-and-test-code-snippet-expansion"></a>生成和测试代码片段扩展
 可以测试代码片段扩展在项目中是否有效。

1. 生成解决方案。 在调试器中运行此项目时，将启动第二Visual Studio实例。

2. 打开文本文件并键入一些文本。

3. 右键单击文本中的某个位置，然后单击"**插入代码片段"。**

4. 代码段选取器 UI 应显示一个弹出窗口，其中显示了 " **测试替换字段**"。 双击弹出窗口。

     应插入以下代码段。

    ```
    MessageBox.Show("first");
    MessageBox.Show("second");
    ```

     不要按 **enter** 或 **Esc 键**。

5. 按 **tab** 键和 **Shift** + **tab** 在 "first" 和 "second" 之间切换。

6. 按 **enter** 或 **Esc** 接受插入。

7. 在文本的其他部分中，键入 "test"，然后按 **tab**。由于 "test" 是代码段快捷方式，因此应再次插入代码段。

## <a name="next-steps"></a>后续步骤
