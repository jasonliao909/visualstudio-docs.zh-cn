---
title: 支持旧版语言服务中的"自动"窗口
description: 了解如何实现对"自动"窗口的支持，该窗口在正在调试的程序暂停时显示范围内表达式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], Autos window
- Autos window, supporting in language services [managed package framework]
ms.assetid: 47d40aae-7a3c-41e1-a949-34989924aefb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6806f4ce6cbdc02ac716c5567af4ce2e6829e69dadd17cd7ff2c1631aee6b00a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432016"
---
# <a name="support-for-the-autos-window-in-a-legacy-language-service"></a>支持旧版语言服务中的"自动"窗口

当 **正在调试** 的程序因断点或异常而暂停时，"自动"窗口显示 (变量和参数等表达式) 。 表达式可以包括变量、局部变量或全局变量，以及局部范围中已更改的参数。 " **自动** "窗口还可以包括类、结构或其他类型的实例化。 表达式计算程序可以计算到的一切内容都可能显示在" **自动"窗口中** 。

 MPF (包) 不直接支持 **"自动"** 窗口。 但是，如果重写 方法，可以返回"自动" <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> 窗口中要呈现 **的表达式** 列表。

## <a name="implementing-support-for-the-autos-window"></a>实现对"自动"窗口的支持

 若要支持"自动" **窗口，只需** 在 类 <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> 中实现 <xref:Microsoft.VisualStudio.Package.LanguageService> 方法。 在给定源文件中的位置后，实现必须决定应在"自动"窗口中 **显示哪些** 表达式。 方法返回字符串列表，其中每个字符串表示单个表达式。 的返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 值指示列表包含表达式，而 指示 <xref:Microsoft.VisualStudio.VSConstants.S_FALSE> 没有要显示表达式。

 返回的实际表达式是出现在代码中该位置的变量或参数的名称。 这些名称将传递给表达式计算程序，以获取随后显示在"自动"窗口中 **的值和** 类型。

### <a name="example"></a>示例
 下面的示例演示 方法的实现，该方法使用分析原因 从 方法获取 <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 表达式列表 <xref:Microsoft.VisualStudio.Package.ParseReason> 。 每个表达式都包装为 `TestVsEnumBSTR` 实现 接口的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsEnumBSTR> 。

 请注意， `GetAutoExpressionsCount` 和 `GetAutoExpression` 方法是 对象上的自定义 `TestAuthoringSink` 方法，已添加以支持此示例。 它们表示一种方式，即分析器通过调用 方法添加到对象 (在分析器) 访问 `TestAuthoringSink` <xref:Microsoft.VisualStudio.Package.AuthoringSink.AutoExpression%2A> 表达式。

```csharp
using Microsoft.VisualStudio;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override int GetProximityExpressions(IVsTextBuffer buffer,
                                                    int line,
                                                    int col,
                                                    int cLines,
                                                    out IVsEnumBSTR ppEnum)
        {
            int retval = VSConstants.E_NOTIMPL;
            ppEnum = null;
            if (buffer != null)
            {
                IVsTextLines textLines = buffer as IVsTextLines;
                if (textLines != null)
                {
                    Source src = this.GetSource(textLines);
                    if (src != null)
                    {
                        TokenInfo tokenInfo = new TokenInfo();
                        string text = src.GetText();
                        ParseRequest req = CreateParseRequest(src,
                                                              line,
                                                              col,
                                                              tokenInfo,
                                                              text,
                                                              src.GetFilePath(),
                                                              ParseReason.Autos,
                                                              null);
                        req.Scope = this.ParseSource(req);
                        TestAuthoringSink sink = req.Sink as TestAuthoringSink;

                        retval = VSConstants.S_FALSE;
                        int spanCount = sink.GetAutoExpressionsCount();
                        if (spanCount > 0) {
                            TestVsEnumBSTR bstrList = new TestVsEnumBSTR();
                            for (int i = 0; i < spanCount; i++)
                            {
                                TextSpan span;
                                sink.GetAutoExpression(i, out span);
                                string expression = src.GetText(span.iStartLine,
                                                                span.iStartIndex,
                                                                span.iEndLine,
                                                                span.iEndIndex);
                                bstrList.AddString(expression);
                            }
                            ppEnum = bstrList;
                            retval = VSConstants.S_OK;
                        }
                    }
                }
            }
            return retval;
        }
    }
}
```
