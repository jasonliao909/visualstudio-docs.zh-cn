---
title: 旧版语言服务中的语法着色|Microsoft Docs
description: 了解如何通过提供可标识词法元素或标记类型的分析器或扫描程序来支持旧版语言服务中的语法着色。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], syntax highlighting
- colorization, supporting in language services [managed package framework]
- syntax highlighting, supporting in language services [managed package framework]
- language services [managed package framework], colorization
ms.assetid: 1ca1736a-f554-42e4-a9c7-fe8c3c1717df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 906f144c6414d5af9483b046f49e3f911b30d0c4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122158835"
---
# <a name="syntax-colorizing-in-a-legacy-language-service"></a>旧版语言服务中的语法着色
语法着色是一项功能，它会导致编程语言的不同元素以不同的颜色和样式显示在源文件中。 若要支持此功能，需要提供一个分析器或扫描程序，用于标识文件中词法元素或标记的类型。 许多语言通过以不同方式 (关键字、分隔符（如括号或) ）和注释进行区分。

 旧版语言服务作为 VSPackage 的一部分实现，但实现语言服务功能的较新方式是使用 MEF 扩展。 若要了解更多信息，请参阅 [扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 建议尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并让你能够利用新的编辑器功能。

## <a name="implementation"></a>实现
 为了支持着色，MPF (包) 包括 实现 接口 <xref:Microsoft.VisualStudio.Package.Colorizer> 的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 类。 此类与 交互 <xref:Microsoft.VisualStudio.Package.IScanner> 以确定标记和颜色。 有关扫描程序详细信息，请参阅 [旧版语言服务分析器与扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)。 然后， 类使用颜色信息标记的每个字符，然后将该信息返回到显示 <xref:Microsoft.VisualStudio.Package.Colorizer> 源文件的编辑器。

 返回到编辑器的颜色信息是可着色项列表的索引。 每个可着色项指定一个颜色值和一组字体属性，例如粗体或删除线。 编辑器提供语言服务可以使用的一组默认可着色项。 只需为每个标记类型指定适当的颜色索引。 但是，可以提供一组自定义可着色项和为令牌提供的索引，并引用自己的可着色项列表而不是默认列表。 还必须将注册表项设置为 0 (或者完全不要指定该条目 `RequestStockColors` `RequestStockColors`) 自定义颜色。 可以将具有命名参数的注册表项设置为 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 用户定义属性。 有关注册语言服务和设置其选项的详细信息，请参阅 [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)。

## <a name="custom-colorable-items"></a>自定义可着色项
 若要提供自己的自定义可着色项，必须重写 <xref:Microsoft.VisualStudio.Package.LanguageService.GetItemCount%2A> 类上的 <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorableItem%2A> 和 <xref:Microsoft.VisualStudio.Package.LanguageService> 方法。 第一种方法返回语言服务支持的自定义可着色项数，第二种方法按索引获取自定义可着色项。 创建自定义可着色项的默认列表。 在语言服务的构造函数中，只需提供每个可着色项的名称。 Visual Studio自动处理用户选择一组不同的可着色项的情况。 此名称显示在"选项"对话框的"字体和颜色"属性页中 (可从 Visual Studio **工具** 菜单) 此名称确定用户已重写的颜色。 用户的选择存储在注册表的缓存中，并按颜色名称访问。 "**字体和颜色**"属性页按字母顺序列出所有颜色名称，因此可以通过在每个颜色名称前面添加语言名称来对自定义颜色进行分组;例如 **，"TestLanguage- Comment"** 和 **"TestLanguage- Keyword"。** 或者，可以按类型"注释 (**TestLanguage) "** 和 **"TestLanguage** (关键字"对可着色) 分组。 首选按语言名称分组。

> [!CAUTION]
> 强烈建议在可着色项名称中包括语言名称，以避免与现有的可着色项名称发生冲突。

> [!NOTE]
> 如果在开发过程中更改其中一种颜色的名称，则必须重置在首次访问颜色Visual Studio创建的缓存。 为此，可以运行"重置实验性 **Hive"** 命令，从 Visual Studio SDK 程序菜单。

 请注意，永远不会引用可着色项列表中的第一项。 Visual Studio始终为该项提供默认文本颜色和属性。 处理这种情况的最简单方法是提供占位符可着色项作为第一项。

### <a name="high-color-colorable-items"></a>高颜色可着色项
 可着色项还可通过 接口支持 24 位或高 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 颜色值。 MPF <xref:Microsoft.VisualStudio.Package.ColorableItem> 类支持 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 接口，24 位颜色与普通颜色一起在构造函数中指定。 有关更多详细信息，请参见 <xref:Microsoft.VisualStudio.Package.ColorableItem> 类。 下面的示例演示如何为关键字和注释设置 24 位颜色。 当用户的桌面上支持 24 位颜色时，使用 24 位颜色;否则，使用普通文本颜色。

 请记住，这些是语言的默认颜色;用户可以将这些颜色更改为所需的任何颜色。

### <a name="example"></a>示例
 此示例演示了一种使用 类声明和填充自定义可着色项数组 <xref:Microsoft.VisualStudio.Package.ColorableItem> 的方法。 此示例使用 24 位颜色设置关键字和注释颜色。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private ColorableItem[] m_colorableItems;

        TestLanguageService() : base()
        {
            m_colorableItems = new ColorableItem[] {
                new ColorableItem("TestLanguage - Text",
                                  "Text",
                                  COLORINDEX.CI_SYSPLAINTEXT_FG,
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,
                                  System.Drawing.Color.Empty,
                                  System.Drawing.Color.Empty,
                                  FONTFLAGS.FF_DEFAULT),
                new ColorableItem("TestLanguage - Keyword",
                                  "Keyword",
                                  COLORINDEX.CI_MAROON,
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,
                                  System.Drawing.Color.FromArgb(192,32,32),
                                  System.Drawing.Color.Empty,
                                  FONTFLAGS.FF_BOLD),
                new ColorableItem("TestLanguage - Comment",
                                  "Comment",
                                  COLORINDEX.CI_DARKGREEN,
                                  COLORINDEX.CI_LIGHTGRAY,
                                  System.Drawing.Color.FromArgb(32,128,32),
                                  System.Drawing.Color.Empty,
                                  FONTFLAGS.FF_DEFAULT)
                // ...
                // Add as many colorable items as you want to support.
            };
        }
    }
}
```

## <a name="the-colorizer-class-and-the-scanner"></a>Colorizer 类和扫描程序
 基 <xref:Microsoft.VisualStudio.Package.LanguageService> 类具有 <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorizer%2A> 实例化类 <xref:Microsoft.VisualStudio.Package.Colorizer> 的方法。 从 方法返回的 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 扫描程序将传递给 <xref:Microsoft.VisualStudio.Package.Colorizer> 类构造函数。

 必须在自己的 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 类版本中实现 <xref:Microsoft.VisualStudio.Package.LanguageService> 方法。 类 <xref:Microsoft.VisualStudio.Package.Colorizer> 使用扫描程序获取所有标记颜色信息。

 扫描程序需要为找到 <xref:Microsoft.VisualStudio.Package.TokenInfo> 的每一个令牌填充 结构。 此结构包含令牌占用的范围、使用的颜色索引、令牌的类型以及令牌触发器 (请参阅 <xref:Microsoft.VisualStudio.Package.TokenTriggers>) 。 类的着色只需要范围和颜色 <xref:Microsoft.VisualStudio.Package.Colorizer> 索引。

 存储在 结构中的颜色索引通常是 来自 枚举的值，该枚举提供与各种语言元素（如关键字和运算符）对应的许多命名 <xref:Microsoft.VisualStudio.Package.TokenInfo> <xref:Microsoft.VisualStudio.Package.TokenColor> 索引。 如果自定义可着色项列表与枚举中呈现的项匹配，则只需使用 枚举 <xref:Microsoft.VisualStudio.Package.TokenColor> 作为每个标记的颜色。 但是，如果你有其他可着色项，或者不想按该顺序使用现有值，可以排列自定义可着色项列表以满足需求，并返回相应索引到该列表。 只需确保在 结构中存储索引时将其强制转换到 <xref:Microsoft.VisualStudio.Package.TokenColor> <xref:Microsoft.VisualStudio.Package.TokenInfo> ; [!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)] 只查看索引。

### <a name="example"></a>示例
 以下示例演示扫描程序如何识别三种标记类型：数字、标点和标识符 (不是数字或标点符号) 。 此示例仅用于说明目的，不表示全面的分析和扫描程序实现。 它假定有一个 `Lexer` 类，该类 `GetNextToken()` 具有返回字符串的方法。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    private Lexer lex;

    public class TestScanner : IScanner
    {
        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false;
            string token = lex.GetNextToken();
            if (token != null)
            {
                char firstChar = token[0];
                if (Char.IsPunctuation(firstChar))
                {
                    tokenInfo.Type = TokenType.Operator;
                    tokenInfo.Color = TokenColor.Keyword;
                }
                else if (Char.IsNumber(firstChar))
                {
                    tokenInfo.Type = TokenType.Literal;
                    tokenInfo.Color = TokenColor.Number;
                }
                else
                {
                    tokenInfo.Type = TokenType.Identifier;
                    tokenInfo.Color = TokenColor.Identifier;
                }
            }
            return foundToken;
        }
```

## <a name="see-also"></a>请参阅
- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
- [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
