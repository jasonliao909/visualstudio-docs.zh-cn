---
title: 旧版语言服务分析器与扫描程序|Microsoft Docs
description: 了解旧版语言服务分析和扫描程序，这些分析器和扫描程序选择有关显示的代码的信息。
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
ms.openlocfilehash: 81b8df95ca4bdad98cb2fdceaae0c6178cefcbccc210e5a62b459bffa6481d21
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121447956"
---
# <a name="legacy-language-service-parser-and-scanner"></a>旧版语言服务分析器和扫描程序
分析器是语言服务的核心。 托管包框架 (MPF) 语言类需要语言分析器来选择有关所显示代码的信息。 分析器将文本分为词法标记，然后按类型和功能标识这些标记。

## <a name="discussion"></a>讨论区
 下面是一个 C# 方法。

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

 本示例中的标记是单词和标点符号。 标记类型如下。

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

 分析器的角色是标识令牌。 某些令牌可以具有多个类型。 分析器识别令牌后，语言服务可以使用信息提供有用的功能，例如语法突出显示、大括号匹配和 IntelliSense 操作。

## <a name="types-of-parsers"></a>分析器的类型
 语言服务分析器与用作编译器一部分的分析器不同。 但是，此类分析器需要同时使用扫描程序和分析器，其方式与编译器分析器相同。

- 扫描程序用于标识令牌类型。 此信息用于语法突出显示和快速标识可触发其他操作（例如括号匹配）的标记类型。 此扫描程序由 接口 <xref:Microsoft.VisualStudio.Package.IScanner> 表示。

- 分析器用于描述标记的函数和范围。 此信息在 IntelliSense 操作中用于标识语言元素（如方法、变量、参数和声明）以及根据上下文提供成员和方法签名的列表。 此分析器还用于查找匹配的语言元素对，如大括号和括号。 此分析器通过 类中的 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法 <xref:Microsoft.VisualStudio.Package.LanguageService> 访问。

  如何为语言服务实现扫描程序和分析器由你决定。 有几个资源可用于描述分析器如何工作以及如何编写自己的分析器。 此外，还有一些免费和商业产品可帮助创建分析器。

### <a name="the-parsesource-parser"></a>ParseSource 分析器
 与用作编译器 (的一部分（其中令牌转换为某种形式的可执行代码) ）的分析器不同，语言服务分析器可以出于许多不同的原因和许多不同的上下文调用。 如何在 类的 方法 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 中实现此方法 <xref:Microsoft.VisualStudio.Package.LanguageService> 由你决定。 必须记住，方法 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 可能在后台线程上调用。

> [!CAUTION]
> <xref:Microsoft.VisualStudio.Package.ParseRequest>结构包含对 对象的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 引用。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>此对象不能在后台线程中使用。 事实上，许多基本 MPF 类不能在后台线程中使用。 其中包括 <xref:Microsoft.VisualStudio.Package.Source> <xref:Microsoft.VisualStudio.Package.ViewFilter> <xref:Microsoft.VisualStudio.Package.CodeWindowManager> 、、 类以及直接或间接与视图通信的其他任何类。

 此分析器通常在首次调用时或给定 的分析原因值时分析 <xref:Microsoft.VisualStudio.Package.ParseReason> 整个源文件。 对 方法的后续调用将处理已分析代码的一小部分，并且可以使用上一个完整分析操作的结果 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 更快速地执行。 方法通过 和 对象传递 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 分析操作 <xref:Microsoft.VisualStudio.Package.AuthoringSink> <xref:Microsoft.VisualStudio.Package.AuthoringScope> 的结果。 对象用于收集特定分析原因的信息，例如，有关具有参数列表的匹配大括号或 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 方法签名的范围的信息。 提供声明和方法签名的集合，还支持"转到高级编辑"选项 ("转到定义"、"转到声明"和"转到引用 <xref:Microsoft.VisualStudio.Package.AuthoringScope> ") 。   

### <a name="the-iscanner-scanner"></a>IScanner 扫描程序
 还必须实现实现 的扫描程序 <xref:Microsoft.VisualStudio.Package.IScanner> 。 但是，由于此扫描程序通过 类以行方式运行，因此 <xref:Microsoft.VisualStudio.Package.Colorizer> 通常更容易实现。 在每行的开头，MPF 为 类提供一个值，该值用作传递给扫描程序的状态 <xref:Microsoft.VisualStudio.Package.Colorizer> 变量。 在每行末尾，扫描程序返回更新的状态变量。 MPF 会缓存每行的此状态信息，以便扫描程序可以从任何行开始分析，而无需从源文件的开头开始。 通过这种对单行的快速扫描，编辑器可以为用户提供快速反馈。

## <a name="parsing-for-matching-braces"></a>分析匹配大括号
 此示例显示控件流，用于匹配用户键入的右大括号。 在此进程中，用于着色的扫描程序还用于确定标记的类型以及标记是否可以触发匹配大括号操作。 如果找到触发器，则调用 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法来查找匹配的大括号。 最后，突出显示两个大括号。

 即使括号用于触发器的名称和分析原因，此过程并不局限于实际大括号。 支持任何指定为匹配对的字符对。 示例包括 ( 和 ) 、 和 \< and > [ 和 ]。

 假设语言服务支持匹配的大括号。

1. 用户从"}"中 (右大括号) 。

2. 大括号插入到源文件中的光标处，光标以 1 为高级。

3. <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>使用键入 <xref:Microsoft.VisualStudio.Package.Source> 的右大括号调用 类中的 方法。

4. <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>方法调用 类中的 方法，以获取当前游标位置之前位置 <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> <xref:Microsoft.VisualStudio.Package.Source> 的标记。 此标记对应于键入的右大括号) 。

    1. <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>方法对 <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> 对象调用 <xref:Microsoft.VisualStudio.Package.Colorizer> 方法，以获取当前行上的所有标记。

    2. <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>方法使用 <xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A> 当前行 <xref:Microsoft.VisualStudio.Package.IScanner> 的文本对 对象调用 方法。

    3. <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>方法重复调用 <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A> 对象上的 <xref:Microsoft.VisualStudio.Package.IScanner> 方法，以收集当前行的所有标记。

    4. 方法调用 类中的私有方法以获取包含所需位置的令牌，并传递从 方法获取 <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> <xref:Microsoft.VisualStudio.Package.Source> 的令牌 <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> 列表。

5. 方法在从 方法返回的令牌上查找 的令牌触发器标志;即表示右大括号的 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> <xref:Microsoft.VisualStudio.Package.TokenTriggers> <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>) 。

6. 如果找到 的触发器 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 标志， <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> 则调用 <xref:Microsoft.VisualStudio.Package.Source> 类中的 方法。

7. <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A>方法使用 分析原因值 启动分析操作 <xref:Microsoft.VisualStudio.Package.ParseReason> 。 此操作最终对 类 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 调用 <xref:Microsoft.VisualStudio.Package.LanguageService> 方法。 如果启用了异步分析，则对 方法的此调用 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 将在后台线程上发生。

8. 分析操作完成后，在 类中 (调用名为) 回调方法的内部 `HandleMatchBracesResponse` 完成 <xref:Microsoft.VisualStudio.Package.Source> 处理程序。 此调用由基类 <xref:Microsoft.VisualStudio.Package.LanguageService> 自动进行，而不是由分析器自动进行。

9. `HandleMatchBracesResponse`方法从对象中存储的对象 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 获取范围 <xref:Microsoft.VisualStudio.Package.ParseRequest> 列表。  (范围是一个结构，它指定源文件中的一系列行和字符。) 此范围列表通常包含两个范围，分别用于左大括号和右大括号。 <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan>

10. `HandleBracesResponse`方法对存储在 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 对象中的 对象调用 <xref:Microsoft.VisualStudio.Package.ParseRequest> 方法。 这会突出显示给定的范围。

11. 如果启用了 属性，则 方法将获取匹配范围包含的文本，并显示状态栏中该范围前 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> `HandleBracesResponse` 80 个字符。 如果方法包含匹配对随附 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 的语言元素，则此方法效果最佳。 有关更多信息，请参见 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> 属性。

12. 完成。

### <a name="summary"></a>摘要
 匹配大括号操作通常仅限于简单的语言元素对。 更复杂的元素（如匹配三 ("、" 和 "， 或 "， " " 和 `if(...)` `{` `}` `else` `{` `}` ") ）可以在单词完成操作中突出显示。 例如，当"else"一词完成后，可以突出显示匹配的 `if` ""语句。 如果有一系列语句，则可以通过使用与匹配大括号相同的机制来 `if` / `else if` 突出显示所有这些语句。 基类已支持此操作，如下所示：扫描程序必须返回令牌触发器值与游标位置之前标记 <xref:Microsoft.VisualStudio.Package.Source> <xref:Microsoft.VisualStudio.Package.TokenTriggers> <xref:Microsoft.VisualStudio.Package.TokenTriggers> 的触发器值组合在一起。

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
