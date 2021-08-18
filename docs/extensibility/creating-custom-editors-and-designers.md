---
title: 创建自定义编辑器和设计器|Microsoft Docs
description: 了解由 IDE 托管的不同类型的编辑器：Visual Studio编辑器、自定义编辑器、外部编辑器和设计器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- designers [Visual Studio SDK]
- editors [Visual Studio SDK], custom
ms.assetid: b6a5e8b2-0ae1-4fc3-812d-09d40051b435
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 9510626a5e884a63e6237ffa6dd3d68a47b61047
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122043682"
---
# <a name="create-custom-editors-and-designers"></a>创建自定义编辑器和设计器

IDE Visual Studio集成开发 (环境) 可以托管不同类型的编辑器：

- Visual Studio核心编辑器

- 自定义编辑器

- 外部编辑器

- 设计器

以下信息可帮助你选择所需的编辑器类型。

## <a name="types-of-editor"></a>编辑器类型

有关核心编辑器Visual Studio，请参阅[扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)。

### <a name="custom-editors"></a>自定义编辑器
 自定义编辑器是一种旨在在专用环境中工作的编辑器。 例如，可以创建一个编辑器，其函数用于读取数据以及将数据写入特定存储库，例如 Microsoft Exchange服务器。 如果希望一个仅与项目类型一同工作的编辑器，或者希望一个只有几个特定命令的编辑器，请选择自定义编辑器。 但请注意，用户将不能使用自定义编辑器来编辑标准 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 项目。

 自定义编辑器可以使用编辑器工厂，并可以将有关编辑器的信息添加到注册表。 但是，与自定义编辑器关联的项目类型可以通过其他方式实例化自定义编辑器。

 自定义编辑器可以使用就地激活或简化的嵌入来实现视图。

### <a name="external-editors"></a>外部编辑器
 外部编辑器是未集成到Visual Studio编辑器，例如 Microsoft Word、记事本 或 Microsoft FrontPage。 例如，如果从 VSPackage 向编辑器传递文本，可以调用此类编辑器。 外部编辑器自行注册，可在外部Visual Studio。 调用外部编辑器时，它可以嵌入到主机窗口中，然后它将显示在 IDE 中的窗口中。 如果没有，则 IDE 会为它创建单独的窗口。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>方法使用 枚举设置文档 <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> 优先级。 如果 `DP_External` 指定了 值，则外部编辑器可以打开该文件。

## <a name="editor-design-decisions"></a>编辑器设计决策
 以下设计问题将帮助你选择最适合应用程序的编辑器类型：

- 应用程序是否将其数据保存在文件中？ 如果它将其数据保存在文件中，它们采用自定义格式还是标准格式？

   如果使用标准文件格式，除项目外的其他项目类型将能够打开和读取/写入数据。 但是，如果使用自定义文件格式，则只有项目类型才能打开和读取/写入数据。

   如果项目使用文件，则应该自定义标准编辑器。 如果项目不使用文件，而是使用数据库或其他存储库中的项，则应该创建自定义编辑器。

- 编辑器是否需要托管ActiveX控件？

   如果编辑器托管ActiveX，请实现就地激活编辑器，如就地[激活 中概述。](/previous-versions/visualstudio/visual-studio-2015/misc/in-place-activation?preserve-view=true&view=vs-2015) 如果它未托管ActiveX，请使用简化的嵌入编辑器，或自定义 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 默认编辑器。

- 编辑器会支持多个视图吗？ 如果希望编辑器视图与默认编辑器同时可见，则必须支持多个视图。

   如果编辑器需要支持多个视图，则编辑器的文档数据和文档视图对象必须是单独的对象。 有关详细信息，请参阅 [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)。

   如果编辑器支持多个视图，你是否计划将核心编辑器的文本缓冲区实现用于 (对象) [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 对象？ 也就是说，是否要支持与核心编辑器并行的编辑器 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 视图？ 这样做是窗体设计器的基础。

- 如果需要托管外部编辑器 ，编辑器是否可嵌入 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 到 内？

   如果可以嵌入，应为外部编辑器创建宿主窗口，然后调用 方法，然后将 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> 枚举值设置为 `DP_External` 。 如果无法嵌入编辑器，IDE 将自动为编辑器创建单独的窗口。

## <a name="in-this-section"></a>本节内容

[演练：创建自定义编辑器](../extensibility/walkthrough-creating-a-custom-editor.md)\
说明如何创建自定义编辑器。

[演练：向自定义编辑器添加功能](../extensibility/walkthrough-adding-features-to-a-custom-editor.md)\
说明如何向自定义编辑器添加功能。

[设计器初始化和元数据配置](../extensibility/designer-initialization-and-metadata-configuration.md)\
说明如何初始化设计器。

[为设计器提供撤消支持](../extensibility/supplying-undo-support-to-designers.md)\
说明如何为设计器提供撤消支持。

[自定义编辑器中的语法着色](../extensibility/syntax-coloring-in-custom-editors.md)\
说明核心编辑器和自定义编辑器中的语法着色的区别。

[自定义编辑器中的文档数据和文档视图](../extensibility/document-data-and-document-view-in-custom-editors.md)\
说明如何在自定义编辑器中实现文档数据和文档视图。

## <a name="related-sections"></a>相关章节

[编辑器中的旧接口](/previous-versions/visualstudio/visual-studio-2015/extensibility/legacy-interfaces-in-the-editor?preserve-view=true&view=vs-2015)\
说明如何通过旧 API 访问核心编辑器。

[开发旧版语言服务](../extensibility/internals/developing-a-legacy-language-service.md)\
说明如何实现语言服务。

[扩展其他部分Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)\
说明如何创建与 的其余部分匹配的 UI 元素 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>
