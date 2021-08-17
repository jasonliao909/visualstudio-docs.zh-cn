---
title: 如何：使用Built-In可着色项|Microsoft Docs
description: 了解如何在语言服务的 IDE Visual Studio集成开发 (中) 可着色项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- colorable items
- language services, built-in colorable items
ms.assetid: 5e5f3436-6bad-4fd2-8823-6a30353ba648
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ea6982d854380b8722e395db11f2ac5099a9bc26dd972ea0730cfbfeef586303
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388664"
---
# <a name="how-to-use-built-in-colorable-items"></a>如何：使用内置可着色项
使用内置可着色项之前，必须先向集成开发环境 (IDE) 表明你未提供自己的自定义可着色项（本例中为 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> 对象）。 为此，可以设置语言服务的注册表项。

## <a name="to-use-built-in-colorable-items"></a>使用内置可着色项

1. 在HKEY_LOCAL_MACHINE\VisualStudio<**\\ X.Y>\Languages\Language Services<\\ Language \> Name** 下，其中 是 的版本，是语言的名称，创建名为 \<X.Y> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] \<Language Name> **RequestStockColors** 的 DWORD 注册表项值。

2. 将 **RequestStockColors** 注册表项值设置为 *1。*

    创建注册表项后，着色器的 方法可以使用 枚举的成员来填充颜色属性数组 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 供编辑器 <xref:Microsoft.VisualStudio.TextManager.Interop.DEFAULTITEMS> 使用。

   > [!NOTE]
   > 如果要提供自定义可着色项，请不要设置此注册表项。 有关详细信息，请参阅自定义 [可着色项](../../extensibility/internals/custom-colorable-items.md)。

## <a name="see-also"></a>请参阅
- [自定义编辑器中的语法着色](../../extensibility/syntax-coloring-in-custom-editors.md)
- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [实现语法着色](../../extensibility/internals/implementing-syntax-coloring.md)
- [自定义可着色项](../../extensibility/internals/custom-colorable-items.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service2.md)
