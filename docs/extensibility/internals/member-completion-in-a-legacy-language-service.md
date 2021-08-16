---
title: 旧版语言服务中的成员完成|Microsoft Docs
description: 了解 IntelliSense 成员完成工具提示在旧版语言服务中的工作原理，以及 MPF (包框架) 。
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

IntelliSense 成员完成是一种工具提示，用于显示特定范围（如类、结构、枚举或命名空间）的可能成员的列表。 例如，在 C# 中，如果用户在后跟一个时间段后类型"this"，则当前作用域内类或结构的所有成员的列表将呈现在用户可以从中选择的列表中。

MPF (包) 为工具提示和管理工具提示中的列表提供支持;所需的就是分析器提供列表中显示的数据。

旧版语言服务作为 VSPackage 的一部分实现，但实现语言服务功能的较新方式是使用 MEF 扩展。 若要了解更多信息，请参阅 [扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 建议尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并让你能够利用新的编辑器功能。

## <a name="how-it-works"></a>工作原理

以下是使用 MPF 类显示成员列表的两种方式：

- 将符号定位在标识符上或成员完成字符之后，然后从 **IntelliSense** 菜单中选择"列出成员"。

- 扫描 <xref:Microsoft.VisualStudio.Package.IScanner> 程序检测成员完成字符，并为此字符设置 [TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>) 的标记触发器。

成员完成字符指示类、结构或枚举的成员将跟随。 例如，在 C# 或 Visual Basic成员完成字符是 ，而在 C++ 中，字符是 `.` `.` 或 `->` 。 在扫描成员选择字符时设置触发器值。

### <a name="the-intellisense-member-list-command"></a>IntelliSense 成员列表命令

该命令启动对 类的 方法的调用，而 方法又调用方法分析器，其分析原因为 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> <xref:Microsoft.VisualStudio.Package.Source> <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> [ParseReason.DisplayMemberList](<xref:Microsoft.VisualStudio.Package.ParseReason.DisplayMemberList>)。

分析器确定当前位置的上下文，以及当前位置下或紧接位置前的标记。 根据此令牌，将显示声明列表。 例如，在 C# 中，如果将 caret 定位在类成员上并选择"列出成员"，则获取类的所有成员的列表。 如果将符号定位在对象变量后的一个时间段之后，则获取对象表示的类的所有成员的列表。 请注意，如果在显示成员列表时，将 caret 定位在成员上，则从列表中选择一个成员会用列表中的一个成员替换该 caret 位于的成员上。

### <a name="the-token-trigger"></a>令牌触发器

[TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)触发器启动对 类的 方法的调用，而 方法又调用分析器，分析原因为 <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> <xref:Microsoft.VisualStudio.Package.Source> <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> [ParseReason.MemberSelect](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>)。 如果令牌触发器还包括 [TokenTriggers.MatchBraces](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MatchBraces>) 标志，则分析原因为 [ParseReason.MemberSelectAndHighlightBraces，](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>)它将成员选择和大括号突出显示组合在一起。

分析器确定当前位置的上下文，以及成员选择字符之前键入的上下文。 分析器根据此信息创建所请求作用域的所有成员的列表。 此声明列表存储在从 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 方法返回的 对象 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 中。 如果返回了任何声明，则会显示成员完成工具提示。 工具提示由 类的实例 <xref:Microsoft.VisualStudio.Package.CompletionSet> 管理。

## <a name="enable-support-for-member-completion"></a>启用对成员完成的支持

必须将注册表项 `CodeSense` 设置为 1，以支持任何 IntelliSense 操作。 可以使用传递给与语言包关联的用户属性的命名参数 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 来设置此注册表项。 语言服务类从 类的 属性中读取 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> 此注册表项 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 的值。

如果扫描程序返回 [TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)的令牌触发器，并且分析器返回声明列表，则会显示成员完成列表。

## <a name="support-member-completion-in-the-scanner"></a>支持扫描程序中的成员完成

分析该字符时，扫描程序必须能够检测成员完成字符并设置 [TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>) 的标记触发器。

### <a name="scanner-example"></a>扫描程序示例

下面是检测成员完成字符并设置相应标志的简化 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 示例。 此示例仅用于说明目的。 它假定扫描程序包含一个 `GetNextToken` 方法，该方法标识并返回文本行中的标记。 示例代码只需设置触发器，只要它看到正确的字符类型。

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

## <a name="support-member-completion-in-the-parser"></a>在分析器中支持成员完成

对于成员完成， <xref:Microsoft.VisualStudio.Package.Source> 类调用 <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A> 方法。 必须在派生自 类的类中实现 <xref:Microsoft.VisualStudio.Package.Declarations> 列表。 有关 <xref:Microsoft.VisualStudio.Package.Declarations> 必须实现的方法的详细信息，请参阅 类。

键入成员选择字符时，使用 [ParseReason.MemberSelect](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>) 或 [ParseReason.MemberSelectAndHighlightBraces](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>) 调用分析器。 对象中给定 <xref:Microsoft.VisualStudio.Package.ParseRequest> 的位置紧接在成员选择字符之后。 分析器必须收集可在源代码中该特定点出现在成员列表中的所有成员的名称。 然后，分析器必须分析当前行，以确定用户希望与成员选择字符关联的范围。

此范围基于成员选择字符之前标识符的类型。 例如，在 C# 中，给定类型为 的成员变量 `languageService` `LanguageService` ，键入 **languageService。** 生成 类的所有成员 `LanguageService` 的列表。 同样在 C# 中，键入 **此内容。** 生成当前作用域中 类的所有成员的列表。

### <a name="parser-example"></a>分析器示例

以下示例演示填充列表的一 <xref:Microsoft.VisualStudio.Package.Declarations> 种方法。 此代码假定分析器构造声明，并调用 类上的 方法，将声明 `AddDeclaration` 添加到 `TestAuthoringScope` 列表中。

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
