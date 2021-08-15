---
title: 对旧版语言服务中的代码进行注释|Microsoft Docs
description: 了解托管包框架 (MPF) 类，这些类在 Visual Studio 中提供对代码注释的支持。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- comments, supporting in language services [managed package framework]
- language services [managed package framework], commenting code
ms.assetid: 9600d6f0-e2b6-4fe0-b935-fb32affb97a4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: d01cb64696e4f440ad0c92125dab0411c722371f2d86f478c5553f0f02f9e013
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121321202"
---
# <a name="comment-code-in-a-legacy-language-service"></a>旧版语言服务中的注释代码
编程语言通常提供对代码进行批注或注释的方式。 注释是文本的一部分，提供有关代码的其他信息，但在编译或解释过程中将被忽略。

 MPF (类) 包框架支持对所选文本进行注释和取消注释。

## <a name="comment-styles"></a>注释样式
注释有两种常规样式：

1. 行注释，其中注释位于单个行上。

2. 阻止注释，其中注释可以包含多个行。

行注释通常具有起始字符 (字符或) 字符，而块注释同时具有开始字符和结束字符。 例如，在 C# 中，行注释以 开头 `//` ，块注释以 开头 `/*` ，以 结尾 `*/` 。

当用户从"编辑高级"菜单中选择命令"**注释** 选择"时，该命令将路由  >  到 <xref:Microsoft.VisualStudio.Package.Source.CommentSpan%2A> 类上的 <xref:Microsoft.VisualStudio.Package.Source> 方法。 当用户选择"取消注释选择 **"** 命令时，该命令将路由到 <xref:Microsoft.VisualStudio.Package.Source.UncommentSpan%2A> 方法。

## <a name="support-code-comments"></a>支持代码注释
 可以通过 的命名参数，使语言服务 `EnableCommenting` 支持代码注释 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 。 这将设置 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCommenting%2A> 类的 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 属性。 有关设置语言服务功能的信息，请参阅 [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)。

 还必须重写 <xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A> 方法以返回具有 <xref:Microsoft.VisualStudio.Package.CommentInfo> 语言注释字符的结构。 C# 样式的行注释字符是默认值。

### <a name="example"></a>示例
 下面是 方法的示例 <xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A> 实现。

```csharp
using Microsoft.VisualStudio.Package;

namespace MyLanguagePackage
{
    class MySource : Source
    {
        public override CommentInfo GetCommentFormat() {
            CommentInfo info = new CommentInfo();
            info.LineStart       = "//";
            info.BlockStart      = "/*";
            info.BlockEnd        = "*/";
            info.UseLineComments = true;
            return info;
        }
    }
}
```

## <a name="see-also"></a>另请参阅
- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
