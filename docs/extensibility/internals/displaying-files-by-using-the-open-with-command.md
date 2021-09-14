---
title: 使用"打开方式"命令显示|Microsoft Docs
description: 了解项目如何在集成开发环境中调用 Open With 命令Visual Studio IDE (IDE) 显示文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, supporting Open With command
- Open With command
- persistence, supporting Open With command
ms.assetid: 53794bc3-1b73-4d40-954e-cfade1abddcf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 1930f643ee609ad101c13a7103a2c7253e7588b2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664394"
---
# <a name="display-files-by-using-the-open-with-command"></a>使用"打开方式"命令显示文件
项目可以要求 IDE 显示" **打开方式"** 对话框。 此请求会提示用户打开具有所选标准编辑器的文件。 以下步骤描述了此过程：

1. 项目调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> ，为 参数 `OSE_UseOpenWithDialog` 指定值 `OSEOpenDocEditor` 。

2. 根据文档的文件扩展名，IDE 确定注册表中列出的哪些编辑器可以打开指定的文档，并会在"打开时 **"对话框中显示** 此信息。

    > [!NOTE]
    > 具有内部编辑器（必须包含在"打开时"对话框中）的项目必须注册每个此类编辑器的编辑器工厂。 内部编辑器仅与特定的项目类型一起运行，这是在 方法的实现中 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 强制执行的。 IDE 具有用于核心文本编辑器和二进制编辑器的内置编辑器工厂。 IDE 还代表每个已注册的文件关联创建Windows实例。 此类文件的一个示例是Microsoft Word。

3. 用户从"打开方式"对话框中选择项后，IDE 就会通过调用 方法打开 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 文档。 有关详细信息，请参阅 [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)。

## <a name="see-also"></a>另请参阅
- [打开并保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)
- [使用"打开文件"命令显示文件](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)
- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)
