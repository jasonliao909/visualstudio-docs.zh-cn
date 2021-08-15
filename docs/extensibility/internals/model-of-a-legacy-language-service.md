---
title: 旧版语言服务模型|Microsoft Docs
description: 使用此最小语言服务模型作为 Visual Studio 核心编辑器的指南，以创建自己的语言服务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, model
ms.assetid: d8ae1c0c-ee3d-4937-a581-ee78d0499793
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 02a1fd8316e3fcb048169fdbaf635116e677389e8f417fb47a3d2be5bd654f68
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432732"
---
# <a name="model-of-a-legacy-language-service"></a>旧版语言服务模型
语言服务定义特定语言的元素和功能，并用于向编辑器提供特定于该语言的信息。 例如，编辑器需要知道语言的元素和关键字，以支持语法着色。

 语言服务与编辑器管理的文本缓冲区和包含编辑器的视图紧密配合工作。 Microsoft IntelliSense **快速信息** 选项是语言服务提供的一项功能示例。

## <a name="a-minimal-language-service"></a>最小语言服务
 最基本的语言服务包含以下两个对象：

- *语言服务* 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> 接口。 语言服务包含有关语言的信息，包括其名称、文件扩展名、代码窗口管理器和着色器。

- 着色 *器* 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 接口。

  下面的概念图显示了基本语言服务的模型。

  ![语言服务模型图形](../../extensibility/media/vslanguageservicemodel.gif "vsLanguageServiceModel") 基本语言服务模型

  文档窗口承载编辑器 *的文档* 视图（本例中为 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 核心编辑器）。 文档视图和文本缓冲区由编辑器拥有。 这些对象通过 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 称为代码窗口 的专用文档 *窗口使用*。 代码窗口包含在由 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> IDE 创建和控制的对象中。

  加载具有给定扩展名的文件时，编辑器将查找与该扩展名关联的语言服务，并调用 方法将代码窗口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> 传递给它。 语言服务返回实现 *接口* 的代码窗口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> 管理器 。

  下表概述了模型中的对象。

| 组件 | 对象 | 函数 |
|------------------| - | - |
| 文本缓冲区 | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> | Unicode 读/写文本流。 文本可以使用其他编码。 |
| 代码窗口 | <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> | 包含一个或多个文本视图的文档窗口。 当 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 位于多文档接口 (MDI) 模式时，代码窗口是 MDI 子窗口。 |
| 文本视图 | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> | 允许用户使用键盘和鼠标导航和查看文本的窗口。 文本视图作为编辑器向用户显示。 可以在普通编辑器窗口、"输出"窗口和"即时"窗口中使用文本视图。 此外，还可以在代码窗口中配置一个或多个文本视图。 |
| 文本管理器 | 由服务 <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> 管理，从该服务获取 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager> 指针 | 一个 组件，它维护前面描述的所有组件共享的共同信息。 |
| 语言服务 | 实现相关;实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> | 一个对象，该对象为编辑器提供特定于语言的信息，例如语法突出显示、语句完成和大括号匹配。 |

## <a name="see-also"></a>另请参阅
- [自定义编辑器中的文档数据和文档视图](../../extensibility/document-data-and-document-view-in-custom-editors.md)
