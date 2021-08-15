---
title: 演练：将功能添加到自定义编辑器|Microsoft Docs
description: 了解如何在使用本演练创建编辑器后向自定义编辑器添加更多功能。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], custom - add features
ms.assetid: bfe083b6-3e35-4b9c-ad4f-b30b9ff412a5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 155906d5dfa35a66cd85053cac3c66c2a11a9b45ea94c7fc4f850e8656d5bf4c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121335012"
---
# <a name="walkthrough-add-features-to-a-custom-editor"></a>演练：向自定义编辑器添加功能
创建自定义编辑器后，可以添加更多功能。

## <a name="to-create-an-editor-for-a-vspackage"></a>为 VSPackage 创建编辑器

1. 使用"包"项目模板Visual Studio编辑器。

     有关详细信息，请参阅 [演练：创建自定义编辑器](../extensibility/walkthrough-creating-a-custom-editor.md)。

2. 确定是希望编辑器支持单个视图还是多个视图。

     支持"新建窗口" **命令** 或具有窗体视图和代码视图的编辑器需要单独的文档数据对象和文档视图对象。 在仅支持单个视图的编辑器中，文档数据对象和文档视图对象可以在同一对象上实现。

     有关多个视图的示例，请参阅 [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)。

3. 通过设置 接口实现编辑器 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> 工厂。

     有关详细信息，请参阅编辑器 [工厂](/previous-versions/visualstudio/visual-studio-2015/extensibility/editor-factories?preserve-view=true&view=vs-2015)。

4. 确定是希望编辑器使用就地激活还是简化嵌入来管理文档视图对象窗口。

     简化的嵌入编辑器窗口承载标准文档视图，而就地激活编辑器窗口承载ActiveX控件或其他活动对象作为文档视图。 有关详细信息，请参阅[简化的嵌入](../extensibility/simplified-embedding.md)[和就地激活](/previous-versions/visualstudio/visual-studio-2015/misc/in-place-activation?preserve-view=true&view=vs-2015)。

5. 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口以处理命令。

6. 提供文档持久性和响应外部文件更改：

    1. 若要保留文件，请对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 编辑器的文档数据对象实现 和 。

    2. 若要响应外部文件更改，请对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl> 编辑器的文档数据对象实现 和 。

        > [!NOTE]
        > 调用 `QueryService` 以 <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx> 获取指向 的指针 `IVsFileChangeEx` 。

7. 使用源代码管理协调文档编辑事件。 按照以下步骤操作：

    1. 通过调用 获取指向 `IVsQueryEditQuerySave2` 的 `QueryService` 指针 <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> 。

    2. 发生第一个编辑事件时，调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 方法。

         此方法会提示用户签出文件（如果尚未签出）。请务必处理"文件未签出"条件以避免错误。

    3. 同样，在保存文件之前，请调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A> 方法。

         如果文件尚未保存，或者自上次保存后更改，此方法将提示用户保存该文件。

8. 启用" **属性** "窗口以显示编辑器中所选文本的属性。 按照以下步骤操作：

    1. 每次 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> 文本选择更改时调用 ，并传递 的实现 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 。

    2. 在 `QueryService` 服务 <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> 上调用 以获取指向 的指针 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> 。

9. 使用户能够在编辑器和工具箱之间或外部编辑器之间拖放项 (如Microsoft Word) 工具箱 **。** 按照以下步骤操作：

    1. 在 `IDropTarget` 编辑器上实现 ，以提醒 IDE 你的编辑器是放置目标。

    2. 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser> 视图上实现 接口，以便编辑器可以启用和禁用工具箱 中的 **项**。

    3. 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.ResetDefaults%2A> 服务 `QueryService` 上 <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox> 实现 和 调用以获取指向 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> 接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> 的指针。

         通过这些步骤，VSPackage 可以将新项 **添加到工具箱**。

10. 确定是否需要编辑器的其他任何可选功能。

    - 如果希望编辑器支持查找和替换命令，请实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget> 。

    - 如果要在编辑器中使用文档大纲工具窗口，请实现 `IVsDocOutlineProvider` 。

    - 如果要在编辑器中使用状态栏，请实现 并 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> 调用 `QueryService` 获取指向 <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> 的指针 `IVsStatusBar` 。

         例如，编辑器可以显示行/列信息、选择模式 (流/框) 以及插入/ (插入/) 。

    - 如果希望编辑器支持 命令，则建议 `Undo` 的方法是使用 OLE 撤消管理器模型。 作为替代方法，你可以使编辑器直接处理 `Undo` 命令。

11. 创建注册表信息，包括 VSPackage 的 GUID、菜单、编辑器和其他功能。

     下面是一个通用代码示例，你将该代码放入 *.rgs* 文件脚本中，以演示如何正确注册编辑器。

    ```csharp
    NoRemove Editors
    {
          ForceRemove {...guidEditor...} = s 'RTF Editor'
          {
             val Package = s '{...guidVsPackage...}'
             ForceRemove Extensions
             {
                val rtf = d 50
             }
          }
    }
    NoRemove Menus
    {
          val {...guidVsPackage...} = s ',203,11'
    }
    ```

12. 实现上下文相关的帮助支持。

     此步骤允许你为编辑器中的项提供 F1 帮助和动态帮助窗口支持。 有关详细信息，请参阅 [如何：为编辑器 提供上下文](/previous-versions/visualstudio/visual-studio-2015/extensibility/how-to-provide-context-for-editors?preserve-view=true&view=vs-2015)。

13. 通过实现 接口，从编辑器公开自动化对象 `IDispatch` 模型。

     有关详细信息，请参阅 [Contributing to the Automation Model](../extensibility/internals/contributing-to-the-automation-model.md)。

## <a name="robust-programming"></a>可靠编程

- 当 IDE 调用 方法时，将创建编辑器 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 实例。 如果编辑器支持多个视图， `CreateEditorInstance` 则 同时创建文档数据和文档视图对象。 如果文档数据对象已打开，则非 null `punkDocDataExisting` 值将传递给 `IVsEditorFactory::CreateEditorInstance` 。 编辑器工厂实现必须通过查询现有文档数据对象上的相应接口来确定该对象是否兼容。 有关详细信息，请参阅 [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)。

- 如果使用简化的嵌入方法，请实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> 接口。

- 如果决定使用就地激活，请实现以下接口：

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleObject>

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleInPlaceActiveObject>

   <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>

  > [!NOTE]
  > `IOleInPlaceComponent`接口用于避免 OLE 2 菜单合并。

   实现 `IOleCommandTarget` 处理剪切、**复制和** 粘贴 **等命令**。 实现 时 `IOleCommandTarget` ，确定编辑器是否需要自己的 *.vsct* 文件来定义自己的命令菜单结构，或者是否可以实现 定义的标准命令 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 通常，编辑器使用和扩展 IDE 的菜单，并定义自己的工具栏。 但是，除了使用 IDE 的标准命令集外，编辑器通常还有必要定义自己的特定命令。 编辑器必须声明它使用的标准命令，然后在 *.vsct* 文件中定义任何新命令、上下文菜单、顶级菜单和工具栏。 如果创建就地激活编辑器，请实现和定义 .vsct 文件中编辑器的菜单和工具栏，而不是使用 <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> OLE 2菜单合并。

- 若要防止 UI 中的菜单命令拥集，应在设计新命令之前使用 IDE 中的现有命令。 共享命令在 *SharedCmdDef.vsct* 和 *ShellCmdDef.vsct 中定义*。 默认情况下，这些文件安装在安装的 VisualStudioIntegration\Common\Inc 子 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] 目录中。

- `ISelectionContainer` 可以表示单选和多选。 每个选定的对象都作为对象 `IDispatch` 实现。

- IDE 将 `IOleUndoManager` 实现为可从 访问的服务，或者实现为可通过 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> 实例化的对象 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> 。 编辑器实现 `IOleUndoUnit` 每个操作的 `Undo` 接口。

- 自定义编辑器可以在两处公开自动化对象：

  - `Document.Object`

  - `Window.Object`

## <a name="see-also"></a>另请参阅

- [参与自动化模型](../extensibility/internals/contributing-to-the-automation-model.md)