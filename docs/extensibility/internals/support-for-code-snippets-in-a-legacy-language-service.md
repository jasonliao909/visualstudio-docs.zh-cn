---
title: 支持旧版语言服务中的代码片段|Microsoft Docs
description: 了解旧版语言服务如何支持代码片段。 代码片段是插入到源文件中的一段代码。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- snippets, supporting in language services
- code snippets, supporting in language services [managed package framework]
- language services [managed package framework], supporting code snippets
ms.assetid: 7490325b-acee-4c2d-ac56-1cd5db1a1083
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 2684e0f369320889f74656cd8b10003ee5187bf6c24d1daf5aa4932cbb993377
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432041"
---
# <a name="support-for-code-snippets-in-a-legacy-language-service"></a>旧版语言服务中的代码片段支持
代码片段是插入到源文件中的一段代码。 代码片段本身是基于 XML 的模板，包含一组字段。 这些字段在插入代码片段后突出显示，并且可以具有不同的值，具体取决于插入代码片段的上下文。 插入代码片段后立即，语言服务可以设置代码片段的格式。

 代码片段以特殊编辑模式插入，该模式允许使用 TAB 键导航代码片段的字段。 字段可以支持 IntelliSense 样式的下拉菜单。 用户通过键入 ENTER 或 ESC 键将代码片段提交到源文件。 若要详细了解代码片段，请参阅 [代码片段](../../ide/code-snippets.md)。

 旧版语言服务作为 VSPackage 的一部分实现，但实现语言服务功能的较新方式是使用 MEF 扩展。 若要了解更多信息，请参阅 [演练：实现代码片段](../../extensibility/walkthrough-implementing-code-snippets.md)。

> [!NOTE]
> 建议尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并让你能够利用新的编辑器功能。

## <a name="managed-package-framework-support-for-code-snippets"></a>代码片段的托管包框架支持
 MPF (包) 支持大多数代码片段功能，从读取模板到插入代码片段和启用特殊编辑模式。 支持通过 类 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 进行管理。

 实例化 类时，将调用 类中的 方法以获取对象 (请注意，基类始终返回每个对象的新 <xref:Microsoft.VisualStudio.Package.Source> <xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> <xref:Microsoft.VisualStudio.Package.ExpansionProvider> <xref:Microsoft.VisualStudio.Package.LanguageService> <xref:Microsoft.VisualStudio.Package.ExpansionProvider> <xref:Microsoft.VisualStudio.Package.Source> 对象) 。

 MPF 不支持扩展函数。 扩展函数是嵌入在代码片段模板中的命名函数，并返回要放置在字段中的一个或多个值。 语言服务本身通过 对象返回 <xref:Microsoft.VisualStudio.Package.ExpansionFunction> 值。 <xref:Microsoft.VisualStudio.Package.ExpansionFunction>对象必须由语言服务实现以支持扩展函数。

## <a name="providing-support-for-code-snippets"></a>为代码片段提供支持
 若要启用对代码片段的支持，必须提供或安装代码片段，并且必须为用户提供插入这些代码片段的方式。 启用对代码片段的支持有三个步骤：

1. 安装代码片段文件。

2. 为语言服务启用代码片段。

3. 调用 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 对象。

### <a name="installing-the-snippet-files"></a>安装代码片段文件
 语言的所有代码片段都作为模板存储在 XML 文件中，通常每个文件有一个代码片段模板。 有关用于代码片段模板的 XML 架构的详细信息，请参阅 [代码片段架构参考](../../ide/code-snippets-schema-reference.md)。 每个代码片段模板都使用语言 ID 进行标识。 此语言 ID 在注册表中指定，并放入模板 `Language` \<Code> 中标记的 属性中。

 通常有两个位置存储代码片段模板文件：1) 语言安装位置，2) 用户文件夹中。 这些位置将添加到注册表中，以便Visual Studio **代码片段管理器** 可以找到代码片段。 用户的文件夹是存储用户创建的代码段的位置。

 已安装的代码片段模板文件的典型文件夹布局如下所示 *：[InstallRoot]* \\ *[TestLanguage]* \Snippets \\ *[LCID]* \Snippets。

 *[InstallRoot]* 是安装语言的文件夹。

 *[TestLanguage]* 是语言作为文件夹名称的名称。

 *[LCID]* 是区域设置 ID。 这是存储代码段的本地化版本。 例如，英语区域设置 ID 为 1033，因此 *[LCID]* 替换为 1033。

 必须提供一个额外的文件，这是一个索引文件，通常SnippetsIndex.xml或ExpansionsIndex.xml (可以使用以 .xml) 结尾的任何有效文件名。 此文件通常存储在 *[InstallRoot]* \\ *[TestLanguage]* 文件夹中，并指定代码段文件夹的确切位置，以及使用该代码段的语言服务的语言 ID 和 GUID。 索引文件的确切路径将放入注册表中，如稍后的"安装注册表项"中所述。 下面是一个SnippetsIndex.xml示例：

```
<?xml version="1.0" encoding="utf-8" ?>
<SnippetCollection>
    <Language Lang="Testlanguage" Guid="{b614a40a-80d9-4fac-a6ad-fc2868fff7cd}">
        <SnippetDir>
            <OnOff>On</OnOff>
            <Installed>true</Installed>
            <Locale>1033</Locale>
            <DirPath>%InstallRoot%\TestLanguage\Snippets\%LCID%\Snippets\</DirPath>
            <LocalizedName>Snippets</LocalizedName>
        </SnippetDir>
    </Language>
</SnippetCollection>
```

 标记 \<Language> 指定属性 (和) `Lang` GUID 的语言 ID。

 此示例假定你已安装语言服务Visual Studio安装文件夹中。 %LCID% 替换为用户的当前区域设置 ID。 可以 \<SnippetDir> 添加多个标记，每个标记分别用于不同的目录和区域设置。 此外，代码片段文件夹可以包含子文件夹，每个子文件夹在索引文件中使用嵌入在标记中的 \<SnippetSubDir> \<SnippetDir> 标记进行标识。

 用户还可以为语言创建自己的代码片段。 它们通常存储在用户的设置文件夹中，例如 *[TestDocs]* \Code Snippets \\ *[TestLanguage]* \Test Code Snippets，其中 *[TestDocs]* 是 Visual Studio 的用户设置文件夹的位置。

 以下替换元素可以放置在索引文件中标记 \<DirPath> 中存储的路径中。

|元素|说明|
|-------------|-----------------|
|%LCID%|区域设置 ID。|
|%InstallRoot%|根安装文件夹Visual Studio，例如 C：\Program Files\Microsoft Visual Studio 8。|
|%ProjDir%|包含当前项目的文件夹。|
|%ProjItem%|包含当前项目项的文件夹。|
|%TestDocs%|用户设置文件夹中的文件夹，例如 C：\Documents 和 设置 \\ *[username]* \我的文档\Visual Studio\8。|

### <a name="enabling-code-snippets-for-your-language-service"></a>为语言服务启用代码片段
 若要为语言服务启用代码片段，可以将 属性添加到 VSPackage (请参阅注册旧版语言服务，了解 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute>) 。 [](../../extensibility/internals/registering-a-legacy-language-service1.md) 和 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.ShowRoots%2A> <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.SearchPaths%2A> 参数是可选的，但应包含命名参数，以便通知代码片段管理器代码片段 `SearchPaths` 的位置。

 下面是如何使用此属性的示例：

```
[ProvideLanguageCodeExpansion(
         typeof(TestSnippetLanguageService),
         "Test Snippet Language",          // Name of language used as registry key
         0,                               // Resource ID of localized name of language service
         "Test Snippet Language",        // Name of Language attribute in snippet template
         @"%InstallRoot%\Test Snippet Language\Snippets\%LCID%\SnippetsIndex.xml",  // Path to snippets index
         SearchPaths = @"%InstallRoot%\Test Snippet Language\Snippets\%LCID%\")]    // Path to snippets
```

### <a name="calling-the-expansion-provider"></a>调用扩展提供程序
 语言服务控制任何代码片段的插入，以及调用插入的方式。

## <a name="calling-the-expansion-provider-for-code-snippets"></a>调用代码片段的扩展提供程序
 有两种方法可以调用扩展提供程序：使用菜单命令，或者使用完成列表中的快捷方式。

### <a name="inserting-a-code-snippet-by-using-a-menu-command"></a>使用菜单命令插入代码片段
 若要使用菜单命令显示代码段浏览器，请添加菜单命令，然后在 接口中调用 方法以响应 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A> <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 该菜单命令。

1. 将命令和按钮添加到 .vsct 文件。 可以在使用菜单命令 [创建扩展中查找执行此操作的说明](../../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 从 类派生 <xref:Microsoft.VisualStudio.Package.ViewFilter> 类并重写 <xref:Microsoft.VisualStudio.Package.ViewFilter.QueryCommandStatus%2A> 方法以指示支持新的菜单命令。 此示例始终启用菜单命令。

    ```csharp
    using Microsoft.VisualStudio.Package;

    namespace TestLanguagePackage
    {
        class TestViewFilter : ViewFilter
        {
            public TestViewFilter(CodeWindowManager mgr, IVsTextView view)
                : base(mgr, view)
            {
            }

            protected override int QueryCommandStatus(ref Guid guidCmdGroup,
                                                      uint nCmdId)
            {
                int hr = base.QueryCommandStatus(ref guidCmdGroup, nCmdId);
                // If the base class did not recognize the command then
                // see if we can handle the command.
                if (hr == (int)Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP)
                {
                    if (guidCmdGroup == GuidList.guidTestLanguagePackageCmdSet)
                    {
                        if (nCmdId == PkgCmdIDList.InvokeCodeSnippetsBrowser)
                        {
                            hr = (int)(OLECMDF.OLECMDF_SUPPORTED | OLECMDF.OLECMDF_ENABLED);
                        }
                    }
                }
                return hr;
            }
        }
    }
    ```

3. 重写 <xref:Microsoft.VisualStudio.Package.ViewFilter.HandlePreExec%2A> 类中的 <xref:Microsoft.VisualStudio.Package.ViewFilter> 方法以获取 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 对象，并 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A> 调用该对象上的 方法。

    ```csharp
    using Microsoft.VisualStudio.Package;

    namespace TestLanguagePackage
    {
        class TestViewFilter : ViewFilter
        {
            public override bool HandlePreExec(ref Guid guidCmdGroup,
                                               uint nCmdId,
                                               uint nCmdexecopt,
                                               IntPtr pvaIn,
                                               IntPtr pvaOut)
            {
                if (base.HandlePreExec(ref guidCmdGroup,
                                       nCmdId,
                                       nCmdexecopt,
                                       pvaIn,
                                       pvaOut))
                {
                    // Base class handled the command.  Do nothing more here.
                    return true;
                }

                if (guidCmdGroup == GuidList.guidTestLanguagePackageCmdSet)
                {
                    if (nCmdId == PkgCmdIDList.InvokeCodeSnippetsBrowser)
                    {
                        ExpansionProvider ep = this.GetExpansionProvider();
                        if (this.TextView != null && ep != null)
                        {
                            bool bDisplayed = ep.DisplayExpansionBrowser(
                                this.TextView,
                                "TestLanguagePackage Snippet:",
                                null,
                                false,
                                null,
                                false);
                        }
                        return true;   // Handled the command.
                    }
                }
                return false;   // Did not handle the command.
            }
        }
    }

    ```

     在插入代码片段的过程中，Visual Studio按给定顺序调用 类 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 中的以下方法：

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnItemChosen%2A>

5. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

6. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

7. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

8. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

     调用 方法后，已插入代码片段，并且对象在特殊编辑模式下，用于修改刚插入 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A> <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 的代码片段。

### <a name="inserting-a-code-snippet-by-using-a-shortcut"></a>使用快捷方式插入代码片段
 实现完成列表中的快捷方式比实现菜单命令要多。 必须先将代码片段快捷方式添加到 IntelliSense 单词完成列表。 然后，必须检测代码片段快捷方式名称何时因完成而插入。 最后，必须使用快捷方式名称获取代码片段标题和路径，将该信息传递给 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> 方法上的 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 方法。

 若要将代码片段快捷方式添加到单词完成列表，请将其添加到 <xref:Microsoft.VisualStudio.Package.Declarations> 类中的 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 对象。 必须确保可以将快捷方式标识为代码片段名称。 有关示例，请参阅演练：获取旧版实现中已安装[ (代码片段) 。 ](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)

 可以在 类的 方法中检测代码片段 <xref:Microsoft.VisualStudio.Package.Declarations.OnAutoComplete%2A> 快捷方式的 <xref:Microsoft.VisualStudio.Package.Declarations> 插入。 由于代码片段名称已插入到源文件中，因此在插入扩展时必须将其删除。 方法采用描述代码段插入点的范围;如果范围在源文件中包含整个代码段名称，该名称 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> 将被代码片段替换。

 下面是一个类版本 <xref:Microsoft.VisualStudio.Package.Declarations> ，它根据快捷方式名称处理代码片段插入。 为清楚起见 <xref:Microsoft.VisualStudio.Package.Declarations> ，省略了 类中的其他方法。 请注意，此类的构造函数采用 <xref:Microsoft.VisualStudio.Package.LanguageService> 对象。 这可以从对象版本传入 (例如，类的实现可能会在其构造函数中接受 对象，并且将该对象传递给类构造函数 <xref:Microsoft.VisualStudio.Package.AuthoringScope> <xref:Microsoft.VisualStudio.Package.AuthoringScope> <xref:Microsoft.VisualStudio.Package.LanguageService> `TestDeclarations`) 。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    internal class TestDeclarations : Declarations
    {
        private ArrayList       declarations;
        private LanguageService languageService;
        private TextSpan        commitSpan;

        public TestDeclarations(LanguageService langService)
            : base()
        {
            languageService = langService;
            declarations = new ArrayList();
        }

        // This method is used to add declarations to the internal list.
        public void AddDeclaration(TestDeclaration declaration)
        {
            declarations.Add(declaration);
        }

        // This method is called to get the string to commit to the source buffer.
        // Note that the initial extent is only what the user has typed so far.
        public override string OnCommit(IVsTextView textView,
                                        string textSoFar,
                                        char commitCharacter,
                                        int index,
                                        ref TextSpan initialExtent)
        {
            // We intercept this call only to get the initial extent
            // of what was committed to the source buffer.
            commitSpan = initialExtent;

            return base.OnCommit(textView,
                                 textSoFar,
                                 commitCharacter,
                                 index,
                                 ref initialExtent);
        }

        // This method is called after the string has been committed to the source buffer.
        public override char OnAutoComplete(IVsTextView textView,
                                            string committedText,
                                            char commitCharacter,
                                            int index)
        {
            TestDeclaration item = declarations[index] as TestDeclaration;
            if (item != null)
            {
                // In this example, TestDeclaration identifies types with a string.
                // You can choose a different approach.
                if (item.Type == "snippet")
                {
                    Source src = languageService.GetSource(textView);
                    if (src != null)
                    {
                        ExpansionProvider ep = src.GetExpansionProvider();
                        if (ep != null)
                        {
                            string title;
                            string path;
                            int commitLength = commitSpan.iEndIndex - commitSpan.iStartIndex;
                            if (commitLength < committedText.Length)
                            {
                                // Replace everything that was inserted
                                // so calculate the span of the full
                                // insertion, taking into account what
                                // was inserted when the commitSpan
                                // was obtained in the first place.
                                commitSpan.iEndIndex += (committedText.Length - commitLength);
                            }

                            if (ep.FindExpansionByShortcut(textView,
                                                           committedText,
                                                           commitSpan,
                                                           true,
                                                           out title,
                                                           out path))
                            {
                                ep.InsertNamedExpansion(textView,
                                                        title,
                                                        path,
                                                        commitSpan,
                                                        false);
                            }
                        }
                    }
                }
            }
            return '\0';
        }
    }
}
```

 当语言服务获取快捷方式名称时，它会调用 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FindExpansionByShortcut%2A> 方法来获取文件名和代码片段标题。 然后，语言服务将调用 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> 类中的方法 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 来插入代码段。 在插入代码段的过程中，将在类中按给定顺序 Visual Studio 调用以下方法 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> ：

1. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

2. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

3. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

   有关获取语言服务的已安装代码段列表的详细信息，请参阅 [演练：获取已安装代码段的列表 (旧实现) ](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)。

## <a name="implementing-the-expansionfunction-class"></a>实现 ExpansionFunction 类
 扩展函数是嵌入到代码段模板中并返回一个或多个要放置在字段中的值的命名函数。 为了支持语言服务中的扩展函数，你必须从类派生一个类 <xref:Microsoft.VisualStudio.Package.ExpansionFunction> 并实现 <xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetCurrentValue%2A> 方法。 然后必须重写 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A> 类中的方法 <xref:Microsoft.VisualStudio.Package.LanguageService> ，以便 <xref:Microsoft.VisualStudio.Package.ExpansionFunction> 为你支持的每个扩展函数返回类版本的新实例化。 如果支持某个扩展函数的可能值列表，则还必须重写 <xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetIntellisenseList%2A> 类中的方法， <xref:Microsoft.VisualStudio.Package.ExpansionFunction> 以返回这些值的列表。

 使用参数或需要访问其他字段的扩展函数不应与可编辑字段关联，因为在调用扩展函数时，扩展提供程序可能不会完全初始化。 因此，扩展函数无法获取其参数或任何其他字段的值。

### <a name="example"></a>示例
 下面是一个示例，说明如何实现称为简单扩展函数的示例 `GetName` 。 每次实例化扩展函数时，此扩展函数都会在基类名称后面追加一个数字 (这对应于每次插入关联的代码片段) 。

```csharp
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private int classNameCounter = 0;

        public override ExpansionFunction CreateExpansionFunction(
            ExpansionProvider provider,
            string functionName)
        {
            ExpansionFunction function = null;
            if (functionName == "GetName")
            {
                ++classNameCounter;
                function = new TestGetNameExpansionFunction(provider, classNameCounter);
            }
            return function;
        }
    }

    internal class TestGetNameExpansionFunction : ExpansionFunction
    {
        private int nameCount;

        TestGetNameExpansionFunction(ExpansionProvider provider, int counter)
            : base(provider)
        {
            nameCount = counter;
        }

        public override string GetCurrentValue()
        {
            string name = "TestClass";
            name += nameCount.ToString();
            return name;
        }
    }
}
```

## <a name="see-also"></a>请参阅
- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
- [代码片段](../../ide/code-snippets.md)
- [演练：获取包含已安装的代码片段的列表（旧版实现）](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)
