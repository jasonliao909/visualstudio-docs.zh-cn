---
title: 旧版语言服务中的成员完成 |Microsoft Docs
description: 了解 IntelliSense 成员完成工具提示在旧版语言服务中的工作方式，以及它如何受托管包框架 (MPF) 支持。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense, Member Completion tool tip
- Member Completion, supporting in language services [managed package framework]
- language services [managed package framework], IntelliSense Member Completion
ms.assetid: 500f718d-9028-49a4-8615-ba95cf47fc52
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: beb0dc40253ddf4280a3cd4854c53151369098a0ef03c1c275769c498570966a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414644"
---
# <a name="member-completion-in-a-legacy-language-service"></a>旧版语言服务中的成员完成

IntelliSense 成员完成是一个工具提示，可显示特定范围（如类、结构、枚举或命名空间）的可能成员的列表。 例如，在 c # 中，如果用户键入 "this" 后跟一个句点，则当前范围内的类或结构的所有成员的列表将显示在用户可以从中选择的列表中。

托管包框架 (MPF) 为工具提示提供支持，并在工具提示中管理列表;所有需要的都是从分析器协作来提供列表中显示的数据。

旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解详细信息，请参阅 [扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

## <a name="how-it-works"></a>工作原理

下面是使用 MPF 类显示成员列表的两种方式：

- 将插入符号定位于标识符上，或在成员完成字符后定位，并从 " **IntelliSense** " 菜单中选择 "**列出成员**"。

- <xref:Microsoft.VisualStudio.Package.IScanner>扫描器检测成员完成字符，并为该字符设置 TokenTriggers 的令牌触发器[。](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)

成员完成字符指示要遵循的类、结构或枚举的成员。 例如，在 c # 或 Visual Basic，成员完成字符为 `.` ，而在 c + + 中，字符是 `.` 或 `->` 。 当扫描成员选择字符时，将设置触发器值。

### <a name="the-intellisense-member-list-command"></a>IntelliSense 成员列表命令

<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>命令启动对类的方法的调用， <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> <xref:Microsoft.VisualStudio.Package.Source> 然后 <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> 方法调用 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法分析器，分析原因为[ParseReason. DisplayMemberList](<xref:Microsoft.VisualStudio.Package.ParseReason.DisplayMemberList>)。

分析器确定当前位置的上下文以及标记下或紧靠当前位置之前的标记。 根据此标记，将显示声明列表。 例如，在 c # 中，如果将插入符号放置在类成员上，并选择 " **列出成员**"，则会获得类的所有成员的列表。 如果将脱字号置于对象变量后跟的句点之后，则将获得该对象所表示的类的所有成员的列表。 请注意，如果显示的是在显示成员列表时在成员上定位插入符号，则从列表中选择成员会将插入符号所在的成员替换为列表中的成员。

### <a name="the-token-trigger"></a>标记触发器

[TokenTriggers MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)触发器启动对类的方法的调用， <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> <xref:Microsoft.VisualStudio.Package.Source> 而方法则 <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> 调用分析器，分析原因为[ParseReason. MemberSelect](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>)。 如果标记触发器同时包含 [TokenTriggers. MatchBraces](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MatchBraces>) 标志，则分析原因为 [ParseReason. MemberSelectAndHighlightBraces](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>)，它结合了成员选择和大括号突出显示。

分析器确定当前位置的上下文以及在成员选择字符之前键入的内容。 通过此信息，分析器创建请求范围的所有成员的列表。 此声明列表存储在 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 从方法返回的对象中 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 。 如果返回任何声明，则显示成员完成工具提示。 工具提示由类的实例管理 <xref:Microsoft.VisualStudio.Package.CompletionSet> 。

## <a name="enable-support-for-member-completion"></a>启用成员完成支持

必须将 `CodeSense` 注册表项设置为1才能支持任何 IntelliSense 操作。 可以使用传递给 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 与语言包关联的用户属性的命名参数来设置此注册表项。 语言服务类从类的属性中读取此注册表项的值 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 。

如果扫描仪返回 [TokenTriggers](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)的令牌触发器，而您的分析器返回声明列表，则显示成员完成列表。

## <a name="support-member-completion-in-the-scanner"></a>支持在扫描仪中完成成员

扫描程序必须能够检测成员完成字符，并在分析该字符时设置 [TokenTriggers](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>) 的令牌触发器。

### <a name="scanner-example"></a>扫描器示例

下面是一个简单的示例，说明如何检测成员完成字符并设置适当的 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 标志。 此示例仅用于说明目的。 它假定您的扫描程序包含一个方法 `GetNextToken` ，该方法用于标识和返回文本行中的标记。 示例代码只是在它看到正确的字符类型时设置触发器。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private Lexer lex;
        private const char memberSelectChar = '.';

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char c = token[0];
                if (c == memberSelectChar)
                {
                        tokenInfo.Trigger |= TokenTriggers.MemberSelect;
                }
            }
            return foundToken;
        }
    }
}
```

## <a name="support-member-completion-in-the-parser"></a>分析程序中的支持成员完成

完成成员后， <xref:Microsoft.VisualStudio.Package.Source> 类会调用 <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A> 方法。 必须在派生自类的类中实现列表 <xref:Microsoft.VisualStudio.Package.Declarations> 。 有关 <xref:Microsoft.VisualStudio.Package.Declarations> 必须实现的方法的详细信息，请参阅类。

类型化成员 select 字符时，将使用[ParseReason 或 MemberSelect](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>)调用[分析器。](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>) 对象中指定的位置 <xref:Microsoft.VisualStudio.Package.ParseRequest> 紧跟在成员 select 字符之后。 分析器必须收集在源代码中该特定点可以出现在成员列表中的所有成员的名称。 然后，分析器必须分析当前行，以确定用户希望与成员 select 字符关联的范围。

此作用域基于在成员选择字符之前的标识符的类型。 例如，在 c # 中，假设 `languageService` 具有类型的成员变量 `LanguageService` ，则键入 **languageService。** 生成类的所有成员的列表 `LanguageService` 。 在 c # 中，键入 **此。** 生成当前范围内类的所有成员的列表。

### <a name="parser-example"></a>分析器示例

下面的示例演示了一种填充列表的方法 <xref:Microsoft.VisualStudio.Package.Declarations> 。 此代码假定分析器构造一个声明，并通过调用类的方法将其添加到列表中 `AddDeclaration` `TestAuthoringScope` 。

```csharp
using System.Collections;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    internal class TestDeclaration
    {
        public string Name;            // Name of declaration
        public int     TypeImageIndex; // Glyph index
        public string Description;     // Description of declaration

        public TestDeclaration(string name, int typeImageIndex, string description)
        {
            this.Name = name;
            this.TypeImageIndex = typeImageIndex;
            this.Description = description;
        }
    }

    //===================================================
    internal class TestDeclarations : Declarations
    {
        private ArrayList declarations;

        public TestDeclarations()
            : base()
        {
            declarations = new ArrayList();
        }

        public void AddDeclaration(TestDeclaration declaration)
        {
            declarations.Add(declaration);
        }

        //////////////////////////////////////////////////////////////////////
        // Declarations of class methods that must be implemented.
        public override int GetCount()
        {
            // Return the number of declarations to show.
            return declarations.Count;
        }

        public override string GetDescription(int index)
        {
            // Return the description of the specified item.
            string description = "";
            if (index >= 0 && index < declarations.Count)
            {
                description = ((TestDeclaration)declarations[index]).Description;
            }
            return description;
        }

        public override string GetDisplayText(int index)
        {
            // Determine what is displayed in the tool tip list.
            string text = null;
            if (index >= 0 && index < declarations.Count)
            {
                text = ((TestDeclaration)declarations[index]).Name;
            }
            return text;
        }

        public override int GetGlyph(int index)
        {
            // Return index of image to display next to the display text.
            int imageIndex = -1;
            if (index >= 0 && index < declarations.Count)
            {
                imageIndex = ((TestDeclaration)declarations[index]).TypeImageIndex;
            }
            return imageIndex;
        }

        public override string GetName(int index)
        {
            string name = null;
            if (index >= 0 && index < declarations.Count)
            {
                name = ((TestDeclaration)declarations[index]).Name;
            }
            return name;
        }
    }

    //===================================================
    public class TestAuthoringScope : AuthoringScope
    {
        private TestDeclarations declarationsList;

        public void AddDeclaration(TestDeclaration declaration)
        {
            if (declaration != null)
            {
                if (declarationsList == null)
                {
                    declarationsList = new TestDeclarations();
                }
                declarationsList.AddDeclaration(declaration);
            }
        }

        public override Declarations GetDeclarations(IVsTextView view,
                                                     int line,
                                                     int col,
                                                     TokenInfo info,
                                                     ParseReason reason)
        {
            return declarationsList;
        }

        /////////////////////////////////////////////////
        // Remainder of AuthoringScope methods not shown.
        /////////////////////////////////////////////////
    }

    //===================================================
    class TestLanguageService : LanguageService
    {
        public override AuthoringScope ParseSource(ParseRequest req)
        {
            TestAuthoringScope scope = new TestAuthoringScope();
            if (req.Reason == ParseReason.MemberSelect ||
                req.Reason == ParseReason.MemberSelectAndHighlightBraces)
            {
                // Gather list of declarations based on what the user
                // has typed so far. In this example, this list is an array of
                // MemberDeclaration objects (a helper class you might implement
                // to hold member declarations).
                // How this list is gathered is dependent on the parser
                // and is not shown here.
                MemberDeclarations memberDeclarations;
                memberDeclarations = GetDeclarationsForScope();

                // Now populate the Declarations list in the authoring scope.
                // GetImageIndexBasedOnType() is a helper method you
                // might implement to convert a member type to an index into
                // the image list returned from the language service.
                foreach (MemberDeclaration dec in memberDeclarations)
                {
                    scope.AddDeclaration(new TestDeclaration(
                                             dec.Name,
                                             GetImageIndexBasedOnType(dec.Type),
                                             dec.Description));
                }
            }
            return scope;
        }
    }
}
```
