---
title: 语言服务筛选器的重要|Microsoft Docs
description: 了解在 Visual Studio 中创建功能齐全的语言服务筛选器时应支持的重要Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- language services, filters
- language services, commands to support
ms.assetid: 4948c494-3d4d-4f50-b3f9-959e73f90e4d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 995cc17117f695500115a918ed24efc447855340dcb37e6b1dff8f9efa23638e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388625"
---
# <a name="important-commands-for-language-service-filters"></a>语言服务筛选器的重要命令
如果要创建功能齐全的语言服务筛选器，请考虑处理以下命令。 命令标识符的完整列表在托管代码的 枚举中定义，在非托管代码的 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> Stdidcmd.h 头文件中 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 定义。 可以在 SDK 安装路径\VisualStudioIntegration\Common\Inc Visual Studio Stdidcmd.h 文件。

## <a name="commands-to-handle"></a>要处理的命令

> [!NOTE]
> 并非必须针对下表中的每个命令进行筛选。

|命令|说明|
|-------------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户右单击时发送。 此命令指示是时候提供快捷菜单了。 如果不处理此命令，文本编辑器会提供不带任何特定于语言的命令的默认快捷菜单。 若要在此菜单上包含自己的命令，请自行处理命令并显示快捷菜单。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|通常在用户输入 CTRL+J 时发送。 对 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> 调用 方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 以显示语句完成框。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户输入字符时发送。 监视此命令以确定何时键入触发器字符，并提供语句完成、方法提示和文本标记，例如语法着色、大括号匹配和错误标记。 对 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> for 语句 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 完成调用 方法，对 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> 方法提示 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> 调用 方法。 若要支持文本标记，请监视此命令以确定要键入的字符是否需要更新标记。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户输入 Enter 键时发送。 通过调用 上的 方法，监视此命令以确定何时关闭 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> 方法提示窗口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> 。 默认情况下，文本视图处理此命令。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户输入 Backspace 键时发送。 通过调用 上的 方法，监视 以确定何时关闭 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> 方法提示窗口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> 。 默认情况下，文本视图处理此命令。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|从菜单或快捷键发送。 在 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> 上调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 方法，使用参数信息更新提示窗口。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户将鼠标悬停在变量上或将光标定位在变量上，然后从"编辑"菜单中 **的 IntelliSense** 中选择"快速信息 **"时** 发送。 通过调用 上的 方法返回提示中 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> 变量的类型 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。 如果调试处于活动状态，提示还应显示变量的值。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|通常在用户输入 CTRL+空格键时发送。 此命令告知语言服务调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> 上的 方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID><br /><br /> <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|从菜单发送，通常是"编辑"菜单中的"注释选择"或"取消注释""高级 **选择**"。  <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> 指示用户想要注释掉所选文本; <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> 指示用户想要取消注释所选文本。 这些命令只能由语言服务实现。|

## <a name="see-also"></a>另请参阅
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
