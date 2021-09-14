---
title: 旧版语言服务分析器和扫描程序 |Microsoft Docs
description: 了解用于选择要显示的代码信息的旧版语言服务分析器和扫描程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- parsers, language services [managed package framework]
- language services [managed package framework], Parsers
ms.assetid: 1ac3de27-a23b-438d-9593-389e45839cfa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6ac6c0a4a0facc68496a2d51b23b6979ba8d9359
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664357"
---
# <a name="legacy-language-service-parser-and-scanner"></a>旧版语言服务分析器和扫描程序
分析器是语言服务的核心。 托管包框架 (MPF) 语言类需要语言分析器来选择要显示的代码的相关信息。 分析器将文本分为词法标记，然后按类型和功能标识这些标记。

## <a name="discussion"></a>讨论 (Discussion)
 下面是一个 c # 方法。

```csharp
namespace MyNamespace
{
    class MyClass
    {
        public void MyFunction(int arg1)
        {
            int var1 = arg1;
        }
    }
}
```

 在此示例中，标记是单词和标点符号。 标记的种类如下所示。

|令牌名称|令牌类型|
|----------------|----------------|
|namespace、class、public、void、int|关键字 (keyword)|
|=|operator|
|{ } ( ) ;|delimiter|
|MyNamespace、MyClass、MyFunction、arg1、var1|标识符|
|MyNamespace|命名空间|
|MyClass|class|
|MyFunction|method|
|arg1|参数 (parameter)|
|var1|局部变量 (local variable)|

 分析器的作用是标识令牌。 某些标记可以有多种类型。 在分析器识别了标记后，语言服务可以使用这些信息来提供有用的功能，如语法突出显示、大括号匹配和 IntelliSense 操作。

## <a name="types-of-parsers"></a>分析器的类型
 语言服务分析器与作为编译器的一部分使用的分析器不同。 但是，这种分析器需要使用扫描器和分析器，其方式与编译器分析器的方式相同。

- 扫描器用于标识令牌的类型。 此信息用于语法突出显示和快速标识可触发其他操作（例如括号匹配）的标记类型。 此扫描程序由接口表示 <xref:Microsoft.VisualStudio.Package.IScanner> 。

- 分析器用于描述标记的功能和范围。 IntelliSense 操作中使用此信息来标识语言元素（例如方法、变量、参数和声明），并根据上下文提供成员和方法签名的列表。 此分析器还用于查找匹配的语言元素对，如大括号和圆括号。 此分析器通过 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 类中的方法访问 <xref:Microsoft.VisualStudio.Package.LanguageService> 。

  如何为语言服务实现扫描程序和分析器是由您来实现的。 提供了多个资源，这些资源说明分析器的工作方式以及如何编写您自己的分析器。 另外，还提供了几个免费和商业产品，有助于创建分析器。

### <a name="the-parsesource-parser"></a>ParseSource 分析器
 与用作编译器一部分的分析器 (，其中的标记转换为某种形式的可执行代码) ，可以出于多种不同的原因和在许多不同的上下文中调用语言服务分析器。 在类的方法中实现此方法的方式 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> 取决于你。 请务必记住，可以 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 在后台线程上调用方法。

> [!CAUTION]
> <xref:Microsoft.VisualStudio.Package.ParseRequest>结构包含对对象的引用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。 此 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 对象不能在后台线程中使用。 事实上，许多基本 MPF 类不能在后台线程中使用。 其中包括 <xref:Microsoft.VisualStudio.Package.Source> 、 <xref:Microsoft.VisualStudio.Package.ViewFilter> 、类以及 <xref:Microsoft.VisualStudio.Package.CodeWindowManager> 直接或间接与视图通信的任何其他类。

 此分析器通常在第一次调用时或在给定的分析原因值时，分析整个源文件 <xref:Microsoft.VisualStudio.Package.ParseReason> 。 对方法的后续调用将 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 处理一小部分分析的代码，并使用上一次完全分析操作的结果可以更快地执行。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法通过和对象传达分析操作的结果 <xref:Microsoft.VisualStudio.Package.AuthoringSink> <xref:Microsoft.VisualStudio.Package.AuthoringScope> 。 <xref:Microsoft.VisualStudio.Package.AuthoringSink>对象用于收集特定分析原因的信息，例如，有关包含参数列表的匹配大括号或方法签名的范围的信息。 <xref:Microsoft.VisualStudio.Package.AuthoringScope>提供声明和方法签名的集合，还支持 "跳到高级" 编辑选项 ("跳到 **定义**"、"**开始到声明**"、"**引用**) "。

### <a name="the-iscanner-scanner"></a>IScanner 扫描仪
 还必须实现实现的扫描程序 <xref:Microsoft.VisualStudio.Package.IScanner> 。 但是，因为此扫描程序通过类逐行操作 <xref:Microsoft.VisualStudio.Package.Colorizer> ，所以通常更容易实现。 在每行的开头，MPF 为 <xref:Microsoft.VisualStudio.Package.Colorizer> 类提供了一个值，用作传递给扫描器的状态变量。 每行结束时，扫描程序返回更新的状态变量。 MPF 将缓存每行的此状态信息，以便扫描程序可以从任何行开始分析，而无需从源文件的开头开始进行分析。 此快速扫描一条线路允许编辑器向用户提供快速反馈。

## <a name="parsing-for-matching-braces"></a>分析匹配的大括号
 此示例演示了用于匹配用户已键入的右大括号的控制流。 在此过程中，用于着色的扫描程序还用于确定令牌类型，以及令牌是否可以触发匹配大括号操作。 如果找到了触发器，则 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 调用方法来查找匹配的大括号。 最后，突出显示两个大括号。

 即使在触发器的名称和分析原因中使用了大括号，此过程也不会限制为实际的大括号。 支持指定为匹配对的任何字符对。 示例包括 ( 和 ) 、 \< and > 和 [和]。

 假定语言服务支持匹配的大括号。

1. 用户键入 (} ) 的右大括号。

2. 将在光标所在的源文件中插入大括号，并将光标前进一。

3. <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>类中的方法 <xref:Microsoft.VisualStudio.Package.Source> 将与键入的右大括号一起调用。

4. <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>方法调用 <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> 类中的方法 <xref:Microsoft.VisualStudio.Package.Source> ，以获取紧靠当前游标位置之前位置的标记。 此标记对应于键入的右大括号) 。

    1. <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>方法对对象调用 <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> 方法 <xref:Microsoft.VisualStudio.Package.Colorizer> 以获取当前行上的所有标记。

    2. <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>方法 <xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A> <xref:Microsoft.VisualStudio.Package.IScanner> 通过当前行的文本调用对象上的方法。

    3. <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>方法对对象重复调用 <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A> 方法 <xref:Microsoft.VisualStudio.Package.IScanner> ，以从当前行中收集所有标记。

    4. <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>方法调用类中的私有方法 <xref:Microsoft.VisualStudio.Package.Source> 来获取包含所需位置的标记，并传入从方法获取的标记的列表 <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> 。

5. <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>方法 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 在从方法返回的令牌上查找标记触发器标志， <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> 即，表示) 的右大括号的标记。

6. 如果找到的触发器标志 <xref:Microsoft.VisualStudio.Package.TokenTriggers> ，则 <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> 调用类中的方法 <xref:Microsoft.VisualStudio.Package.Source> 。

7. <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A>方法使用分析原因值开始分析操作 <xref:Microsoft.VisualStudio.Package.ParseReason> 。 此操作最终对 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 类调用方法 <xref:Microsoft.VisualStudio.Package.LanguageService> 。 如果启用了异步分析，则对方法的此调用将 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 在后台线程上发生。

8. 分析操作完成后，内部完成处理程序 (也称为回调方法) `HandleMatchBracesResponse` 在类中调用 <xref:Microsoft.VisualStudio.Package.Source> 。 此调用由基类自动进行 <xref:Microsoft.VisualStudio.Package.LanguageService> ，而不是由分析器进行。

9. `HandleMatchBracesResponse`方法从 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 存储在对象中的对象获取范围列表 <xref:Microsoft.VisualStudio.Package.ParseRequest> 。 范围 (是一个 <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan> 结构，它指定源文件中的行和字符范围。 ) 此范围列表通常包含两个范围，每个范围分别用于左大括号和右大括号。

10. `HandleBracesResponse`方法对 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 存储在对象中的对象调用方法 <xref:Microsoft.VisualStudio.Package.ParseRequest> 。 这将突出显示给定范围。

11. 如果该 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 属性已 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> 启用，则该 `HandleBracesResponse` 方法将获取匹配范围包含的文本，并在状态栏中显示该范围内的前80个字符。 如果该 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法包含匹配对随附的 language 元素，则这种方法的效果最佳。 有关更多信息，请参见 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> 属性。

12. 完成。

### <a name="summary"></a>总结
 匹配大括号操作通常仅限于简单的语言元素对。 更复杂的元素（例如匹配的三元组 ( ""、""、""、""、""、"" `if(...)` `{` `}` `else` `{` 和 ") "） `}` 可在单词完成操作中突出显示。 例如，当"else"一词完成后，可以突出显示匹配的 `if` ""语句。 如果有一系列语句，则可以通过使用与匹配大括号相同的机制来 `if` / `else if` 突出显示所有这些语句。 基类已支持此操作，如下所示：扫描程序必须返回令牌触发器值与游标位置之前标记 <xref:Microsoft.VisualStudio.Package.Source> <xref:Microsoft.VisualStudio.Package.TokenTriggers> <xref:Microsoft.VisualStudio.Package.TokenTriggers> 的触发器值组合在一起。

 有关详细信息，请参阅 [旧版语言服务 中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)。

## <a name="parsing-for-colorization"></a>着色分析
 对源代码进行着色非常简单，只需标识令牌类型并返回有关该类型的颜色信息。 类 <xref:Microsoft.VisualStudio.Package.Colorizer> 充当编辑器和扫描程序之间的中介，提供有关每个标记的颜色信息。 <xref:Microsoft.VisualStudio.Package.Colorizer>类使用 对象来帮助为行着色，以及收集源文件中所有 <xref:Microsoft.VisualStudio.Package.IScanner> 行的状态信息。 在 MPF 语言服务类中，类无需重写，因为它仅通过 接口 <xref:Microsoft.VisualStudio.Package.Colorizer> 与扫描程序 <xref:Microsoft.VisualStudio.Package.IScanner> 通信。 通过重写 类上的 <xref:Microsoft.VisualStudio.Package.IScanner> 方法，提供 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 实现 接口 <xref:Microsoft.VisualStudio.Package.LanguageService> 的 对象。

 <xref:Microsoft.VisualStudio.Package.IScanner>扫描程序通过 方法获得一行 <xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A> 源代码。 重复对 方法的调用以获取行中的下一个标记，直到该行 <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A> 用完令牌。 对于着色，MPF 将所有源代码视为一系列行。 因此，扫描程序必须能够处理以线条表示的源。 此外，任何行都随时都可以传递到扫描程序，唯一的保证是扫描程序在扫描行之前从行接收状态变量。

 <xref:Microsoft.VisualStudio.Package.Colorizer>类还用于标识令牌触发器。 这些触发器告知 MPF 特定标记可以启动更复杂的操作，例如单词完成或匹配大括号。 由于识别此类触发器必须快速且必须出现在任何位置，因此扫描程序最适合此任务。

 有关详细信息，请参阅 [旧版语言服务 中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)。

## <a name="parsing-for-functionality-and-scope"></a>功能和范围分析
 分析功能和范围比识别遇到的令牌类型需要更多的工作量。 分析器不仅必须标识令牌的类型，还必须标识令牌使用的功能。 例如，标识符只是一个名称，但在语言中，标识符可以是类、命名空间、方法或变量的名称，具体取决于上下文。 令牌的一般类型可能是标识符，但该标识符也可能具有其他含义，具体取决于它的定义和定义位置。 此标识要求分析器对正在分析的语言有更广泛的了解。 这是 类 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 的进入位置。 类收集有关标识符、方法、匹配语言对 (（如大括号和括号) ）以及语言三元组 (（类似于语言对）的信息，只不过有三个部分，例如"" 和 <xref:Microsoft.VisualStudio.Package.AuthoringSink> `foreach()` `{` `}` ") " 。 此外，可以重写 类以支持代码标识（用于早期验证断点，以便无需加载调试器）和"自动调试"窗口，该窗口在调试程序时自动显示局部变量和参数，并且要求分析器识别适当的局部变量和参数以及调试器提供的参数。 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 

 对象作为 对象的一部分传递给分析器，并且每次创建一个新的 对象时都会 <xref:Microsoft.VisualStudio.Package.AuthoringSink> <xref:Microsoft.VisualStudio.Package.ParseRequest> <xref:Microsoft.VisualStudio.Package.AuthoringSink> 创建一个新的 <xref:Microsoft.VisualStudio.Package.ParseRequest> 对象。 此外， <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法必须返回 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 对象，该对象用于处理各种 IntelliSense 操作。 对象维护声明的列表和方法的列表，其中任一方法都填充，具体取决于 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 分析原因。 <xref:Microsoft.VisualStudio.Package.AuthoringScope>必须实现 类。

## <a name="see-also"></a>另请参阅
- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [旧版语言服务概述](../../extensibility/internals/legacy-language-service-overview.md)
- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)
- [旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)
