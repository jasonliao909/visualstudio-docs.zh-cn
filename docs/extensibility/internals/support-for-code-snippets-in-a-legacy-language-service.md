---
title: 支持旧版语言服务中的代码片段 |Microsoft Docs
description: 了解旧版语言服务如何支持代码片段。 代码段是插入到源文件中的代码片段。
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
代码段是插入到源文件中的代码片段。 代码段本身是一个基于 XML 的模板，其中包含一组字段。 在插入代码段后，这些字段将突出显示，并且可能会有不同的值，具体取决于代码段插入到的上下文。 在插入代码段后，语言服务可以立即设置代码段的格式。

 代码段以特殊编辑模式插入，该模式允许使用 TAB 键来导航代码段的字段。 这些字段可支持 IntelliSense 样式下拉菜单。 用户通过键入 ENTER 或 ESC 键将代码段提交到源文件。 若要了解有关代码片段的详细信息，请参阅 [代码片段](../../ide/code-snippets.md)。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解详细信息，请参阅 [演练：实现代码片段](../../extensibility/walkthrough-implementing-code-snippets.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

## <a name="managed-package-framework-support-for-code-snippets"></a>托管包框架对代码片段的支持
 托管包框架 (MPF) 支持大多数代码段功能，从读取模板到插入代码段和启用特殊编辑模式。 支持通过类进行管理 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 。

 当对 <xref:Microsoft.VisualStudio.Package.Source> 类进行实例化时，将 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A> 调用类中的方法 <xref:Microsoft.VisualStudio.Package.LanguageService> 来获取 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 对象 (请注意， <xref:Microsoft.VisualStudio.Package.LanguageService> <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 对于每个对象) ，基类始终返回一个新的对象 <xref:Microsoft.VisualStudio.Package.Source> 。

 MPF 不支持扩展功能。 扩展函数是嵌入到代码段模板中并返回一个或多个要放置在字段中的值的命名函数。 值由语言服务本身通过 <xref:Microsoft.VisualStudio.Package.ExpansionFunction> 对象返回。 <xref:Microsoft.VisualStudio.Package.ExpansionFunction>对象必须由语言服务实现才能支持扩展函数。

## <a name="providing-support-for-code-snippets"></a>为代码片段提供支持
 若要启用对代码片段的支持，必须提供或安装代码段，并且必须为用户提供插入这些代码段的方式。 为代码片段启用支持有三个步骤：

1. 安装代码段文件。

2. 为语言服务启用代码片段。

3. 调用 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 对象。

### <a name="installing-the-snippet-files"></a>安装代码段文件
 语言的所有代码段都作为模板存储在 XML 文件中，通常每个文件都有一个代码段模板。 有关用于代码段模板的 XML 架构的详细信息，请参阅 [代码片段架构参考](../../ide/code-snippets-schema-reference.md)。 每个代码段模板都用语言 ID 标识。 在注册表中指定该语言 ID，并将其放入 `Language` \<Code> 模板中标记的属性。

 通常，存储代码段模板文件的位置有两个： 1) 语言的安装位置，2) 用户的文件夹中。 将这些位置添加到注册表，以便 Visual Studio **代码片段管理器** 可以找到代码片段。 用户的文件夹存储用户创建的代码段。

 已安装代码段模板文件的典型文件夹布局如下所示： *[InstallRoot]* \\ *[TestLanguage]* \Snippets \\ *[LCID]* \snippets。

 *[InstallRoot]* 是你的语言所安装到的文件夹。

 *[TestLanguage]* 作为文件夹名称。

 *[LCID]* 为区域设置 ID。 这就是如何存储代码段的本地化版本。 例如，英语的区域设置 ID 为1033，因此 *[LCID]* 替换为1033。

 必须提供另一个文件，并且该文件是索引文件（通常称为 SnippetsIndex.xml 或 ExpansionsIndex.xml (可以使用以 .xml) 结尾的任何有效文件名。 此文件通常存储在 *[InstallRoot]* \\ *[TestLanguage]* 文件夹中，它指定了代码段文件夹的确切位置以及使用代码段的语言服务的语言 ID 和 GUID。 索引文件的确切路径将置于注册表中，如后面的 "安装注册表项" 中所述。 下面是 SnippetsIndex.xml 文件的示例：

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

 \<Language>标记指定 (`Lang` 属性) 和语言服务 GUID 的语言 ID。

 此示例假设已在 Visual Studio 安装文件夹中安装了语言服务。 % LCID% 将替换为用户的当前区域设置 ID。 \<SnippetDir>可以添加多个标记，分别用于每个不同的目录和区域设置。 此外，代码段文件夹可以包含子文件夹，其中每个子文件夹都在带有嵌入标记的标记的索引文件中标识 \<SnippetSubDir> \<SnippetDir> 。

 用户还可以为你的语言创建自己的代码段。 这些通常存储在用户的设置文件夹中，例如 *[TestDocs]* \Code 片段 \\ *[TestLanguage]* \Test 代码段，其中 *[TestDocs]* 是 Visual Studio 的用户设置文件夹的位置。

 以下替换元素可放置在存储在 \<DirPath> 索引文件的标记中的路径中。

|元素|说明|
|-------------|-----------------|
|LCID|区域设置 ID。|
|InstallRoot|Visual Studio 的根安装文件夹，例如，C:\Program 文件 \ Microsoft Visual Studio 8。|
|%ProjDir%|包含当前项目的文件夹。|
|%ProjItem%|包含当前项目项的文件夹。|
|%TestDocs%|文件夹中的文件夹，例如，c:\documents and 和设置 \\ *[username]* \My Documents \ Visual Studio \ 8。|

### <a name="enabling-code-snippets-for-your-language-service"></a>启用语言服务的代码片段
 可以通过将属性添加到 VSPackage 来启用语言服务的代码片段 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> (参阅 [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md) 获取详细信息) 。 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.ShowRoots%2A>和 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.SearchPaths%2A> 参数是可选的，但你应该包含 `SearchPaths` 命名参数，以便向 **代码段管理器通知代码** 段的位置。

 下面的示例演示如何使用此属性：

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
 语言服务控制任何代码片段的插入以及调用插入的方式。

## <a name="calling-the-expansion-provider-for-code-snippets"></a>为代码片段调用扩展提供程序
 可以通过两种方法调用扩展提供程序：使用菜单命令或通过使用完成列表中的快捷方式。

### <a name="inserting-a-code-snippet-by-using-a-menu-command"></a>使用菜单命令插入代码片段
 若要使用菜单命令显示代码片段浏览器，请添加一个菜单命令，然后在 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A> 接口中调用该方法以 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 响应该菜单命令。

1. 将一个命令和一个按钮添加到 .vsct 文件。 可以在 [使用菜单命令创建扩展](../../extensibility/creating-an-extension-with-a-menu-command.md)中找到相关说明。

2. 从类派生一个类 <xref:Microsoft.VisualStudio.Package.ViewFilter> ，并重写 <xref:Microsoft.VisualStudio.Package.ViewFilter.QueryCommandStatus%2A> 方法以指示对新菜单命令的支持。 此示例始终启用菜单命令。

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

3. 重写 <xref:Microsoft.VisualStudio.Package.ViewFilter.HandlePreExec%2A> 类中的方法 <xref:Microsoft.VisualStudio.Package.ViewFilter> 以获取 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 对象，并对 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A> 该对象调用方法。

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

     在 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 插入代码段的过程中，按给定顺序 Visual Studio 调用类中的以下方法：

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnItemChosen%2A>

5. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

6. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

7. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

8. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

     <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>调用方法后，将插入代码段，并且 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 对象处于特殊编辑模式，用于修改刚刚插入的代码段。

### <a name="inserting-a-code-snippet-by-using-a-shortcut"></a>使用快捷方式插入代码片段
 完成列表中的快捷方式的实现比实现菜单命令更多。 必须首先将代码段快捷方式添加到 IntelliSense word 完成列表。 然后，必须检测在完成后插入了代码段快捷方式名称的时间。 最后，你必须使用快捷方式名称获取代码片段标题和路径，并将该信息传递给 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> 方法的方法 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 。

 若要将代码段快捷方式添加到单词完成列表，请将它们添加到 <xref:Microsoft.VisualStudio.Package.Declarations> 类中的对象 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 。 必须确保可以将快捷方式标识为代码段名称。 有关示例，请参阅 [演练：获取已安装代码片段的列表 (旧实现) ](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)。

 可以在类的方法中检测代码段快捷方式的插入 <xref:Microsoft.VisualStudio.Package.Declarations.OnAutoComplete%2A> <xref:Microsoft.VisualStudio.Package.Declarations> 。 因为代码段名称已经插入到源文件中，所以在插入扩展时必须将其删除。 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A>方法采用一个范围来描述代码段的插入点，如果跨距包含源文件中的整个代码段名称，则该名称将替换为代码段。

 下面是类的一个版本 <xref:Microsoft.VisualStudio.Package.Declarations> ，用于处理在给定快捷方式名称时插入的代码段。 <xref:Microsoft.VisualStudio.Package.Declarations>为了清楚起见，已省略类中的其他方法。 请注意，此类的构造函数采用 <xref:Microsoft.VisualStudio.Package.LanguageService> 对象。 这可以从你的对象的版本传入 <xref:Microsoft.VisualStudio.Package.AuthoringScope> (例如，类的实现 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 可能会 <xref:Microsoft.VisualStudio.Package.LanguageService> 在其构造函数中采用对象，并将该对象传递给 `TestDeclarations` 类构造函数) 。

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

 当语言服务获取快捷方式名称时，它会调用 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FindExpansionByShortcut%2A> 方法来获取文件名和代码片段标题。 然后，语言服务调用 <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> 类中的 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 方法来插入代码片段。 在插入代码片段的过程中，Visual Studio类中的给定顺序调用 <xref:Microsoft.VisualStudio.Package.ExpansionProvider> 以下方法：

1. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

2. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

3. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

   有关获取语言服务的已安装代码片段列表详细信息，请参阅演练：获取旧版实现中的已安装代码[ (列表) 。 ](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)

## <a name="implementing-the-expansionfunction-class"></a>实现 ExpansionFunction 类
 扩展函数是嵌入在代码片段模板中的命名函数，并返回要放置在字段中的一个或多个值。 为了支持语言服务中的扩展函数，必须从 类派生类 <xref:Microsoft.VisualStudio.Package.ExpansionFunction> 并实现 <xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetCurrentValue%2A> 方法。 然后，必须重写 类中的 方法，为支持的每个扩展函数返回类 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> <xref:Microsoft.VisualStudio.Package.ExpansionFunction> 版本的新实例化。 如果支持扩展函数中可能值的列表，则还必须重写 类中的 方法以 <xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetIntellisenseList%2A> <xref:Microsoft.VisualStudio.Package.ExpansionFunction> 返回这些值的列表。

 采用参数或需要访问其他字段的扩展函数不应与可编辑字段关联，因为扩展提供程序可能无法在调用扩展函数时完全初始化。 因此，扩展函数无法获取其参数或其他任何字段的值。

### <a name="example"></a>示例
 以下示例演示了如何实现调用的简单 `GetName` 扩展函数。 每次实例化扩展函数时，此扩展函数都向基类名称追加一个数字 (该数字对应于每次在基类中插入关联的代码) 。

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

## <a name="see-also"></a>另请参阅
- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
- [代码片段](../../ide/code-snippets.md)
- [演练：获取包含已安装的代码片段的列表（旧版实现）](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)
