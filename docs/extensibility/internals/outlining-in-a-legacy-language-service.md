---
title: 旧版语言服务语言服务中的大纲|Microsoft Docs
description: 了解如何通过实现旧版语言服务中的隐藏区域来支持大纲显示。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- outlining
- language services [managed package framework], outlining
- outlining, supporting in language services [managed package framework]
ms.assetid: 7b5578b4-a20a-4b94-ad4c-98687ac133b9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 73b2adbc6dbaab22d5d1888b42db3c0256e31846dcd1633241c6faae7b74a3ce
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414631"
---
# <a name="outlining-in-a-legacy-language-service"></a>旧版语言服务中的大纲显示
大纲显示使复杂程序可以折叠到概述或大纲中。 例如，在 C# 中，所有方法都可以折叠为一行，只显示方法签名。 此外，可以折叠结构和类，以只显示结构和类的名称。 在单个方法中，可以通过只显示第一行语句（如 、 和 ）来折叠复杂逻辑以显示整体 `foreach` `if` 流 `while` 。

 旧版语言服务作为 VSPackage 的一部分实现，但实现语言服务功能的较新方式是使用 MEF 扩展。 若要了解更多信息，请参阅 [演练：大纲显示](../../extensibility/walkthrough-outlining.md)。

> [!NOTE]
> 建议尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并让你能够利用新的编辑器功能。

## <a name="enabling-support-for-outlining"></a>启用对大纲显示的支持
 注册表 `AutoOutlining` 项设置为 1 以启用自动大纲显示。 自动大纲显示在加载或更改文件时设置整个源分析，以便识别隐藏区域并显示大纲显示字形。 大纲显示也可以由用户手动控制。

 注册表项 `AutoOutlining` 的值可以通过 类上的 属性 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A> <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 获取。 注册表项可以使用属性的命名参数进行初始化， (注册 `AutoOutlining` <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> [旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md) 了解详细信息) 。

## <a name="the-hidden-region"></a>隐藏区域
 若要提供大纲显示，语言服务必须支持隐藏的区域。 这些是可展开或折叠的文本范围。 隐藏区域可以通过标准语言符号（如大括号）或自定义符号进行分隔。 例如，C# 具有 `#region` / `#endregion` 一个分隔隐藏区域对。

 隐藏区域由作为接口公开的隐藏区域管理器 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> 管理。

 大纲显示使用隐藏区域接口，并包含隐藏区域的范围、当前可见状态，以及折叠范围时要 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegion> 显示的横幅。

 语言服务分析器使用 方法添加具有隐藏区域默认行为的新隐藏区域，而 方法允许你自定义大纲的外观 <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A> <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A> 和行为。 将隐藏区域给定给隐藏区域会话后， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 管理语言服务的隐藏区域。

 如果需要确定何时销毁隐藏区域会话，则更改隐藏区域，或者需要确保特定隐藏区域可见;必须从 类派生类 <xref:Microsoft.VisualStudio.Package.Source> ，并分别重写相应的方法 、 <xref:Microsoft.VisualStudio.Package.Source.OnBeforeSessionEnd%2A> 和 <xref:Microsoft.VisualStudio.Package.Source.OnHiddenRegionChange%2A> <xref:Microsoft.VisualStudio.Package.Source.MakeBaseSpanVisible%2A> 。

### <a name="example"></a>示例
 下面是为大括号的所有对创建隐藏区域的简化示例。 假定语言提供大括号匹配，并且要匹配的大括号至少包括 {和 } ( ) 。 此方法仅用于说明目的。 完整实现将具有 中事例的完整处理 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 。 此示例还演示如何暂时 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A> 将首选项 `true` 设置为 。 一种替代方法是在 `AutoOutlining` 语言包的 属性 `ProvideLanguageServiceAttribute` 中指定命名参数。

 此示例假定注释、字符串和文本的 C# 规则。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace MyLanguagePackage
{

    public class MyLanguageService : LanguageService
    {
        private LanguagePreferences m_preferences;

        public override LanguagePreferences  GetLanguagePreferences()
        {
            if (m_preferences == null)
            {
                m_preferences = new LanguagePreferences(this.Site,
                                                        typeof(MyLanguageService).GUID,
                                                        Name);
                m_preferences.Init();
                // Temporarily enabled auto-outlining
                m_preferences.AutoOutlining = true;
            }
            return m_preferences;
        }

        public override AuthoringScope  ParseSource(ParseRequest req)
        {
            Source source = (Source) this.GetSource(req.FileName);
            switch (req.Reason)
            {
               case ParseReason.HighlightBraces:
               case ParseReason.MatchBraces:
               case ParseReason.MemberSelectAndHighlightBraces:
                  if (source.Braces != null)
                  {
                      foreach (TextSpan[] brace in source.Braces)
                      {
                         if (brace.Length == 2)
                         {
                             if (req.Sink.HiddenRegions == true
                                   && source.GetText(brace[0]).Equals("{")
                                   && source.GetText(brace[1]).Equals("}"))
                             {
                                //construct a TextSpan of everything between the braces
                                TextSpan hideSpan = new TextSpan();
                                hideSpan.iStartIndex = brace[0].iStartIndex;
                                hideSpan.iStartLine = brace[0].iStartLine;
                                hideSpan.iEndIndex = brace[1].iEndIndex;
                                hideSpan.iEndLine = brace[1].iEndLine;
                                req.Sink.ProcessHiddenRegions = true;
                                req.Sink.AddHiddenRegion(hideSpan);
                             }
                             req.Sink.MatchPair(brace[0], brace[1], 1);
                         }
                         else if (brace.Length >= 3)
                             req.Sink.MatchTriple(brace[0], brace[1], brace[2], 1);
                  }
        }
                   break;
               default:
                   break;
      }
            // Must always return a valid AuthoringScope object.
            return new MyAuthoringScope();
        }
    }
}
```

## <a name="see-also"></a>另请参阅
- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
