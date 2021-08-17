---
title: 清单：创建旧版语言服务|Microsoft Docs
description: 了解为核心编辑器创建旧版语言服务Visual Studio步骤。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services
- language services, native code
ms.assetid: 8b73b341-a33a-4ab5-9390-178c9e563d2d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 87ebb7ebbacbf03dcbf3275fc809ec26bffbada80c2786df10260aa1eab4a075
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359762"
---
# <a name="checklist-create-a-legacy-language-service"></a>清单：创建旧版语言服务
以下清单总结了为核心编辑器创建语言服务必须执行的基本 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 步骤。 若要将语言服务集成到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中，必须创建调试表达式计算程序。 有关详细信息，请参阅在调试器扩展性 中编写[CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md) Visual Studio[计算器](../../extensibility/debugger/visual-studio-debugger-extensibility.md)。

## <a name="steps-to-create-a-language-service"></a>创建语言服务的步骤

1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> 接口。

    - 在 VSPackage 中，实现 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 接口以提供语言服务。

    - 使语言服务可用于实现中的集成 (IDE) 环境 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 。

2. 在 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> 主语言服务类中实现 接口。

     <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>接口是核心编辑器与语言服务之间交互的起点。

### <a name="optional-features"></a>可选功能
 以下功能是可选的，可以按任意顺序实现。 这些功能增加了语言服务的功能。

- 语法着色

  实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 接口。 此接口的实现应包含分析器信息，以返回相应的颜色信息。

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>方法返回 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 接口。 将针对每个文本缓冲区创建单独的着色器实例，因此应单独 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 实现 接口。 有关详细信息，请参阅 [旧版语言服务 中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)。

- 代码窗口

  实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> 接口，使语言服务能够接收有关何时创建新代码窗口的通知。

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A>方法返回 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> 接口。 然后，语言服务可以将特殊 UI 添加到 中的代码窗口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A> 。 语言服务还可以执行任何特殊处理，例如，在 中添加文本视图筛选器 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.OnNewView%2A> 。

- 文本视图筛选器

  若要在语言服务中提供 IntelliSense 语句完成，必须截获文本视图将处理的一些命令。 若要截获这些命令，请完成以下步骤：

  - 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 以参与命令链并处理编辑器命令。

  - 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> 方法并传递实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。

  - 从 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.RemoveCommandFilter%2A> 视图中分离时调用 方法，以便这些命令不再传递给你。

  必须处理的命令取决于提供的服务。 有关详细信息，请参阅语言 [服务筛选器 的重要命令](../../extensibility/internals/important-commands-for-language-service-filters.md)。

  > [!NOTE]
  > <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>接口必须在接口的同一对象上 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 实现。

- 语句结束

  实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> 接口。

  支持语句完成 (，即) 并调用 接口中的 方法， <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 并传递 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> 接口。 有关详细信息，请参阅旧版 [语言服务 中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)。

- 方法提示

  实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> 接口，为方法提示窗口提供数据。

  安装文本视图筛选器以适当处理命令，以便知道何时显示方法数据提示窗口。 有关详细信息，请参阅 [旧版语言服务 中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)。

- 错误标记

  实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 接口。

  创建实现 接口的错误标记 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 对象并调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> 方法，并 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 传递错误标记对象的 接口。

  通常，每个错误标记管理任务列表窗口中的项。

- 任务列表项

  实现提供 接口的任务项 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskItem> 类。

  实现提供 接口和 接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider> 的任务提供程序 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider2> 类。

  实现提供 接口的任务枚举器 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumTaskItems> 类。

  使用任务列表的 方法注册任务 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RegisterTaskProvider%2A> 提供程序。

  通过使用服务 GUID 调用语言服务的服务 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> 提供程序来获取 接口 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> 。

  创建任务项对象，当有新的或更新的任务时，在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RefreshTasks%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> 接口中调用 方法。

- 注释任务项

  使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo> 接口和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens> 接口获取注释任务标记。

  从 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo> 服务获取 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> 接口。

  从 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens> 方法获取 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo.EnumTokens%2A> 接口。

  实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskListEvents> 接口以侦听令牌列表中的更改。

- 大纲显示

  有几个选项支持大纲显示。 例如，可以支持" **折叠到定义"** 命令、提供编辑器控制的大纲区域或支持客户端控制的区域。 有关详细信息，请参阅 [如何：在旧版语言服务 中提供扩展的大纲显示支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)。

- 语言服务注册

  若要详细了解如何注册语言服务，请参阅注册[旧版语言服务和](../../extensibility/internals/registering-a-legacy-language-service2.md)[管理 VSPackage。](../../extensibility/managing-vspackages.md)

- 上下文相关帮助

  通过下列方式之一向编辑器提供上下文：

  - 通过实现 接口为文本标记提供 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> 上下文。

  - 通过实现 接口提供所有用户 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> 上下文。

## <a name="see-also"></a>请参阅
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
- [编写 CLR 表达式计算程序](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
