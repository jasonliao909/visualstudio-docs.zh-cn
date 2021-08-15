---
title: 字形控件 (源代码管理 VSPackage) |Microsoft Docs
description: 了解如何在源代码管理 VSPackage 中显示自定义标志符号，以便可以使用自己的图标来指示源代码管理下项的状态。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- glyphs, source control packages
- source control packages, glyphs
ms.assetid: b9413b08-b3c3-4fc3-a6e0-3dc0db3652d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 840ea85abfa995d9fc8df9e417ab13e78b25423e29d12684b3628760b5a61228
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121337963"
---
# <a name="glyph-control-source-control-vspackage"></a>字形控件 (源代码管理 VSPackage) 
源代码管理 VSPackages 可用的深度集成的一部分是能够显示自己的标志符号，以指示源代码管理下项的状态。

## <a name="levels-of-glyph-control"></a>字形控件的级别
 状态标志符号是一个图标，指示项在显示时的当前状态，例如，在 解决方案资源管理器 **或****类视图。** 源代码管理 VSPackage 可以执行两个级别的字形控制。 它可以将字形的选择限制为 IDE 提供的预定义字形集，也可以定义要显示的自定义字形 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集。

### <a name="default-set-of-glyphs"></a>默认字形集
 若要确定与 解决方案资源管理器 项关联的状态字形，项目使用 从源代码管理请求状态字形 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.GetSccGlyph%2A> 。 源代码管理 VSPackage 可能会决定将字形的选择限制为 IDE 提供的预定义字形。 在这种情况下，VSPackage 将传递回表示 *vsshell.idl* 中定义的字形枚举的值数组。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>。 这是 IDE 设置的预定义标志符号集，例如签入标志符号的挂锁和已签出标志符号的复数标记。

### <a name="custom-set-of-glyphs"></a>自定义字形集
 源代码管理 VSPackage 可以使用自己的字形，在安装时提供独特的外观。 当新的源代码管理 VSPackage 处于活动状态时，它应该能够开始使用自己的字形，即使以前的源代码管理 VSPackage 仍处于加载状态但处于非活动状态。 在此模式下，源代码管理 VSPackage 仍可以使用现有图标，以便保持与 的一致外观（ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 如果已选择）。

 该服务 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> 支持接口 ，VSPackage 可以选择实现接口，IDE 会要求它 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs> 。 当 IDE 提出请求时， 将尝试从当前注册的源代码管理 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage 获取此接口。 如果已注册的 VSPackage 中存在接口，则 IDE 对自定义字形的请求会成功;否则 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，IDE 使用其默认字形集。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs.GetCustomGlyphList%2A>方法用于获取显示 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 各种源代码管理状态的图像列表。 源代码管理 VSPackage 将自定义字形的图像列表句柄返回到 IDE。 此时，IDE 会创建图像列表的副本，稍后再使用它来选择要显示字形。 如果不支持新接口或 方法返回 ，则 IDE 会从 提供的默认字形 `IVsSccGlyphs::GetCustomGlyphList` `E_NOTIMPL` 列表中获取其字形 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>
- <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>
