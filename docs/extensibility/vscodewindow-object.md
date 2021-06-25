---
title: VSCodeWindow 对象|Microsoft Docs
description: 了解代码窗口，这是可包含一个或多个文本视图（通常为 VsTextView 对象）的专用文档窗口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VSCodeWindow
helpviewer_keywords:
- views [Visual Studio SDK], VSCodeWindow object
- VsCodeWindow object
ms.assetid: cf5fe926-e784-4098-bc01-cac49c7c55c6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9803132605ee81c67785c8c0154861b26730ca5f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905327"
---
# <a name="vscodewindow-object"></a>VSCodeWindow 对象
代码窗口是一个专用的文档窗口，可以包括一个或多个文本视图，通常是 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> 对象。

 从体系结构上来说，代码窗口是窗口框架中的文档窗口。 在功能上，代码窗口只是具有其他功能的文档窗口。 在多文档界面 (MDI) 模式下，代码窗口是 MDI 子框架。 有关详细信息，请参阅 [使用旧版 API 自定义代码窗口](/previous-versions/visualstudio/visual-studio-2015/extensibility/customizing-code-windows-by-using-the-legacy-api?preserve-view=true&view=vs-2015)。

 下表包含 对象中的 <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> 接口。

|方法|描述|
|------------|-----------------|
|<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>|提供通用访问机制，用于查找 GUID 标识的全局 (标识符) 的服务。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|表示包含一个或多个代码 (MDI) 的多个文档接口。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|填充窗口框架。|

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [图形编辑](https://www.microsoft.com/download/details.aspx?id=55984)