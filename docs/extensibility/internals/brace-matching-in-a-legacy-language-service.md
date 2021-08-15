---
title: 旧版语言服务中的大括号匹配|Microsoft Docs
description: 了解旧版语言服务中的大括号匹配，这有助于跟踪必须一起出现的语言元素，如括号和大括号。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- brace matching
- language services [managed package framework], brace matching
ms.assetid: 4e3d0a70-f22f-49dd-92d8-edf48ab62b52
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a172a62e993539f990bf1281095725c8d34b2fc727e4f86fc252ebe3a5191283
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121275692"
---
# <a name="brace-matching-in-a-legacy-language-service"></a>旧版语言服务中的大括号匹配
大括号匹配可帮助开发人员跟踪需要一起出现的语言元素，如括号和大括号。 当开发人员输入右大括号时，左大括号将突出显示。

 可以匹配两个或三个共发生元素，称为对和三元组。 三元组是三个共发生元素的集。 例如，在 C# 中， `foreach` 语句形成三个 `foreach()` ：、 `{` 和 `}` 。 键入右大括号时，将突出显示所有三个元素。

 旧版语言服务作为 VSPackage 的一部分实现，但实现语言服务功能的较新方式是使用 MEF 扩展。 若要详细了解实现大括号匹配的新方法，请参阅 [演练：显示匹配的大括号](../../extensibility/walkthrough-displaying-matching-braces.md)。

> [!NOTE]
> 建议尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并让你能够利用新的编辑器功能。

 类 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 支持 和 方法的对和 <xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchPair%2A> 三 <xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchTriple%2A> 元组。

## <a name="implementation"></a>实现
 语言服务需要标识语言中所有匹配的元素，然后找到所有匹配的对。 这通常是通过实现 来检测匹配的语言，然后使用 方法来 <xref:Microsoft.VisualStudio.Package.IScanner> <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 匹配元素来实现的。

 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>方法调用扫描程序以标记该行，并返回标记之前正要标记的标记。 扫描程序通过在当前令牌上将 标记触发器值设置为 来指示 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 已找到语言元素对。 方法调用 方法，该方法又使用 分析原因值 调用 方法， <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> <xref:Microsoft.VisualStudio.Package.LanguageService.BeginParse%2A> <xref:Microsoft.VisualStudio.Package.ParseReason> 以查找匹配的语言元素。 找到匹配的语言元素时，将突出显示这两个元素。

 有关键入大括号如何触发大括号突出显示的完整说明，请参阅旧版语言服务分析器与扫描程序一文的示例分析[操作部分](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)。

## <a name="enable-support-for-brace-matching"></a>启用对大括号匹配的支持
 属性 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 可以设置 **MatchBraces、MatchBracesAtCaret** 和 **ShowMatchingBrace** 注册表项，用于设置类的相应 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 属性。 用户还可以设置语言首选项属性。

|注册表项|属性|说明|
|--------------------|--------------|-----------------|
|MatchBraces|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBraces%2A>|启用大括号匹配。|
|MatchBracesAtCaret|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBracesAtCaret%2A>|在光标移动时启用大括号匹配。|
|ShowMatchingBrace|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>|突出显示匹配的大括号。|

## <a name="match-conditional-statements"></a>匹配条件语句
 可以使用与匹配分隔符相同的方式匹配条件语句，如 、 和 、 或 、 `if` `else if` `else` `#if` `#elif` `#else` `#endif` 。 你可以对 类进行子类化，并提供一个方法，该方法可以将文本范围以及分隔符添加到匹配 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 元素的内部数组。

## <a name="set-the-trigger"></a>设置触发器
 下面的示例演示如何检测匹配的括号、大括号和方括号，以及如何在扫描程序中设置触发器。 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>类上的 方法检测触发器并调用分析器以查找匹配对 (请参阅本文中的查找匹配部分 <xref:Microsoft.VisualStudio.Package.Source>) 。  此示例仅用于说明目的。 它假定扫描程序包含一个 `GetNextToken` 方法，该方法标识并返回文本行中的标记。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private const string braces = "()[]{}";
        private Lexer lex;

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false;
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char firstChar = token[0];
                if (Char.IsPunctuation(firstChar) && token.Length > 0)
                {
                    if (braces.IndexOf(firstChar) != -1)
                    {
                        tokenInfo.Trigger = TokenTriggers.MatchBraces;
                    }
                }
            }
            return foundToken;
        }
```

## <a name="match-the-braces"></a>匹配大括号
 下面是一个简化的示例，用于匹配语言元素 `{ }` 、 `( )` 和 ，并 `[ ]` 添加其范围到 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 对象。 此方法不是分析源代码的推荐方法;它仅用于说明目的。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class Parser
    {
         private IList<TextSpan[]> m_braces;
         public IList<TextSpan[]> Braces
         {
             get { return m_braces; }
         }
         private void AddMatchingBraces(TextSpan braceSpan1, TextSpan braceSpan2)
         {
             if IsMatch(braceSpan1, braceSpan2)
                 m_braces.Add(new TextSpan[] { braceSpan1, braceSpan2 });
         }

         private bool IsMatch(TextSpan braceSpan1, TextSpan braceSpan2)
         {
             //definition for matching here
          }
    }

    public class TestLanguageService : LanguageService
    {
         Parser parser = new Parser();
         Source source = (Source) this.GetSource(req.FileName);

         private AuthoringScope ParseSource(ParseRequest req)
         {
             if (req.Sink.BraceMatching)
             {
                 if (req.Reason==ParseReason.MatchBraces)
                 {
                     foreach (TextSpan[] brace in parser.Braces)
                     {
                         req.Sink.MatchPair(brace[0], brace[1], 1);
                     }
                 }
             }
             return new TestAuthoringScope();
         }
    }
}
```

## <a name="see-also"></a>另请参阅
- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
- [旧版语言服务分析器与扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
