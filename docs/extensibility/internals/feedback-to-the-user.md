---
title: 向用户反馈|Microsoft Docs
description: 了解如何向用户提供有关 IDE Visual Studio集成开发环境中可用功能的 (反馈) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user model feedback
- environment, context
- IDE, context
- IDE, user feedback
ms.assetid: 2d472a24-3813-4f5f-9783-b491ad8a71ad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 1b4794dcf4293b340390695afa02bb49e552ada8918e9a3184c74f16b987432e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388729"
---
# <a name="feedback-to-the-user"></a>向用户反馈
在集成开发 (IDE) 中，有关可用功能的可视反馈基于用户的当前 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 选择和全局选择上下文。 下表列出了不同选择上下文中可用的功能。

|选择上下文|可用功能|
|-----------------------|-----------------------------|
|IDE|全球|
|当前产品集|特定于产品|
|活动层次结构|特定于层次结构类型|
|活动层次结构项|特定于层次结构项类型|
|活动文档|文档类型特定|
|MDI 窗口的最顶层多 () 界面|特定于窗口类型|
|当前选择上下文|特定于选择上下文|

 如果只显示用户所需的功能，并持续提供一致的选择和环境上下文反馈，则可以降低 IDE 的复杂性。 每当在 IDE 中打开窗口时，都会应用以下规则：

- 如果窗口更改其选择上下文，选择反馈会清楚地显示在窗口中，并且动态帮助窗口（如果显示）会更新以反映当前上下文。

- 如果窗口更改全局选择上下文，则所有上下文特定的菜单、活动层次结构窗口和应用程序标题栏将更新以反映当前上下文。

- 该窗口应在"属性"窗口中显示当前选择的属性，并且可以选择显示"属性页 **"对话框（** 如果显示）。

- 如果窗口未显示属性或更改全局选择上下文，则当该窗口不再是 IDE 中的活动窗口时，选择反馈不应保留在窗口中。

- 所有特定于文档的工具窗口都应持续反映活动文档。

- 菜单、工具栏和应用程序标题栏应反映 MDI 窗口 (文档) 界面。

  例如，打开 Web 应用程序项目中Web 窗体的 HTML Visual Basic用户选择标记时，将按以下方式 `<td>` 提供反馈：

- 所选内容在活动窗口中指示，并反映在"属性 **"** 窗口中。

- 特定于 **文档的工具箱已** 更新以反映活动文档。

- 将显示 **"** 编辑器 **"** 工具栏和"表"菜单，标题栏将更新以反映"Web 窗体"窗口。

- 活动层次结构窗口（通常 **解决方案资源管理器）及其** 标题栏更新以反映当前上下文和上下文相关的 Project **菜单命令** 现在应用于活动 Web 应用程序项目。

## <a name="see-also"></a>请参阅
- [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [选择上下文对象](../../extensibility/internals/selection-context-objects.md)
- [层次结构和选择](../../extensibility/internals/hierarchies-and-selection.md)
