---
title: 确定哪个编辑器在文件中打开Project |Microsoft Docs
description: 了解注册表项和Visual Studio SDK 方法，Visual Studio确定哪个编辑器在项目中打开文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], determining which editor opens a file
- projects [Visual Studio SDK], determining which editor opens file
- project types, determining which editor opens a file
- persistence, determining which editor opens a file
ms.assetid: acbcf4d8-a53a-4727-9043-696a47369479
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6f8e5ba694e2a720291f55c969142c5e082ebc44
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122124602"
---
# <a name="determine-which-editor-opens-a-file-in-a-project"></a>确定哪个编辑器在项目中打开文件
当用户在项目中打开文件时，环境将经历轮询过程，最终打开该文件的适当编辑器或设计器。 环境使用的初始过程对于标准编辑器和自定义编辑器都是相同的。 在轮询用于打开文件的编辑器时，环境使用各种条件，并且 VSPackage 必须在此过程中与环境协调。

 例如，当用户从"文件"菜单中选择"打开"命令，然后选择 *filename.rtf* (或扩展名为 *.rtf*) 的其他任何文件时，环境将调用每个项目的实现，最终循环访问解决方案中的所有项目实例。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> 项目返回一组标志，这些标志按优先级标识文档上的声明。 环境使用最高优先级调用适当的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> 方法。 有关轮询过程的详细信息，请参阅 [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。

 杂项文件项目声明其他项目未声明的所有文件。 这样，自定义编辑器就可以在标准编辑器打开文档之前打开文档。 如果杂项文件项目声明文件，则环境将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 方法，以使用标准编辑器打开该文件。 环境检查其内部已注册编辑器列表，以检查其是否处理 *.rtf* 文件。 此列表位于注册表中的以下项：

 **HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\ \<version> \编辑器 \\ \<editor factory guid> \Extensions**

 环境还会检查具有子项 **DocObject****的任何** HKEY_CLASSES_ROOT\CLSID键中的类标识符。 如果在那里找到文件扩展名，则应用程序的嵌入版本（如 Microsoft Word）将就地创建Visual Studio。 这些文档对象必须是实现 接口的复合文件 <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage> ，或者对象必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 接口。

 如果注册表中没有 *.rtf* 文件的编辑器工厂，则环境将在 **\\ .rtf** HKEY_CLASSES_ROOT中查找，并打开该注册表中指定的编辑器。 如果在 文件中找不到文件扩展HKEY_CLASSES_ROOT，则环境将使用 Visual Studio核心文本编辑器打开文件（如果它是文本文件）。

 如果核心文本编辑器失败（如果文件不是文本文件，则会发生此情况，则环境会使用文件的二进制编辑器）。

 如果环境在其注册表中找到了 *.rtf* 扩展的编辑器，它将加载实现此编辑器工厂的 VSPackage。 环境对新的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> VSPackage 调用 方法。 VSPackage 调用 `QueryService` `SID_SVsRegistorEditor` ，使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A> 方法将编辑器工厂注册到环境。

 环境现在重新检查其已注册编辑器的内部列表，以查找 *.rtf* 文件的新注册编辑器工厂。 环境调用 方法的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 实现，并传递要创建的文件名和视图类型。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>
- <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>
