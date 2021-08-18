---
title: 应用程序交互Visual Studio |Microsoft Docs
description: 了解在生成新特性时可使用的常见交互模式库Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 05/13/2020
ms.topic: reference
ms.assetid: a3643792-b0df-481c-bc35-576f948e04cf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 5bc1d93d4b99b99a2a833d3301f32a5005d6dda3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122152037"
---
# <a name="interaction-patterns-for-visual-studio"></a>Visual Studio 的交互模式
## <a name="overview"></a>概述
 一般而言，设计模式是设计的核心，可在特定情况下应用，以解决类似约束集的问题。 特性和系统设计器使用这些设计模式作为起点，然后可以适应其特定情况。

 Visual Studio一个常用交互模式库，在生成新功能时，应考虑这些模式。 设计模式有两个核心上下文：Visual Studio 客户端 (devenv) 和 GitHub Codespaces (之前Visual Studio Online) 。 对于一些设计问题，存在一种在所有情况下都效果良好的通用模式。 但是，在许多情况下，对于浏览器内呈现的 UI 和托管在客户端应用程序上的 UI，解决方案可能有所不同。

### <a name="visual-studio-client-pattern-types"></a>Visual Studio客户端模式类型

|模式类型|说明|示例|
|------------------|-----------------|--------------|
|**应用程序级模式**|应用程序通用的高级模式，确定或显示应用程序上下文，并包含复合和控件模式|- 工具窗口<br />- 文档窗口|
|**复合模式**|可能跨应用程序模式的常见模式，或由不同配置中的多个控件所识别的模式|- 视图切换<br />- 列出生成器<br />- 显示数据<br />- 通知<br />- 验证<br />- 选择模型|
|**控件模式**|有关低级别控件的行为方式的具体信息|- 树视图<br />- 在网格控件中编辑|

## <a name="application-patterns"></a>应用程序模式
 从较高层面来说，Visual Studio界面由单个 IDE 中的多个窗口、对话框、命令和工具栏组成。 层次结构Visual Studio上下文和驱动器菜单。 IDE 用户界面中的关键集成点是文档窗口、工具窗口、项目、命令结构、文本编辑器、工具箱、属性窗口 和工具>选项。

 IDE 用户界面中每个关键集成点都有基本的使用模式：

- [Visual Studio 的菜单和命令](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)

- [Visual Studio 的应用程序模式](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)

  - [窗口交互](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_WindowInteractions)

  - [工具窗口](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_ToolWindows)

  - [文档编辑器约定](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_DocumentEditorConventions)

  - [对话框](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)

  - [项目](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Projects)

## <a name="common-control-patterns"></a>常见控件模式
 控件模式主要与各个控件的行为方式有关。 这是一致性最重要的一方面。

 Visual Studio中的最常见控件应遵循桌面Windows指南。 我们的指南仅包括需要通过特定于 Visual Studio 的交互来增强常见约定的区域，或我们完全取代准则的位置，以便定制 Visual Studio 以满足复杂用户的需求。

- [Visual Studio 的公共控件模式](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md)

  - [常见控件](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CommonControls)

  - [文本控件](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

  - [按钮和超链接](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

## <a name="composite-patterns"></a>复合模式
 用户期望通过多种方式完成任务。 在可能的情况下，功能应设计为使用这些模式进行交互和视觉设计。

 尽管许多复合模式Visual Studio，但一致性最重要的一些模式是：

- [Visual Studio 的复合模式](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md)

  - [对象上 UI 和速览](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_OnObjectUI)

  - [选择模型](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_SelectionModels)

  - [持久性和保存设置](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_PersistenceAndSavingSettings)

  - [触摸输入](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_TouchInput)
