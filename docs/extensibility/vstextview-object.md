---
title: VSTextView 对象|Microsoft Docs
description: VSTextView 对象是一个窗口，允许用户查看和编辑文本缓冲区的 Unicode 文本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VSTextView
helpviewer_keywords:
- VSTextView object, reference
- views [Visual Studio SDK], reference
ms.assetid: 78272ddc-9718-4c65-a94e-a44a2e8d54f4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 7ef751a635d31bc43b2ae4eb32dae9917120a7b0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122144270"
---
# <a name="vstextview-object"></a>VSTextView 对象

文本视图是一个窗口，允许用户查看和编辑文本缓冲区的 Unicode 文本。 实质上，视图是大多数用户都称其为编辑器的视图。 由于视图由各种文本层（ (自动换行、大纲显示文本等）从缓冲区中) 因此不保证该视图是缓冲区中文本的确切表示形式。 有关文本视图详细信息，请参阅使用旧版 [API 访问文本视图](/previous-versions/visualstudio/visual-studio-2015/extensibility/accessing-thetext-view-by-using-the-legacy-api?preserve-view=true&view=vs-2015)。

下表显示了 对象中的 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> 接口。

|接口|说明|
|---------------|-----------------|
|[IDropSource](/windows/desktop/api/oleidl/nn-oleidl-idropsource)|标准 OLE 接口。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IDropTarget>|标准 OLE 接口。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite>|标准 OLE 接口。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|标准 OLE 接口。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|允许创建复合操作 (，即分组到单个撤消/重做单元中的) 。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|提供管理和访问视图的基本方法。 `IVsTextView` 不是线程安全的。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|创建和管理窗口窗格。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView>|与文本层交互。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsThreadSafeTextView>|从不同的线程对视图执行操作。|

## <a name="see-also"></a>请参阅

- [图形编辑](https://www.microsoft.com/download/details.aspx?id=55984)
- [VSTextBuffer 对象](../extensibility/vstextbuffer-object.md)