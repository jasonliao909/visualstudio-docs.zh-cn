---
title: 属性窗口概述|Microsoft Docs
description: 在此概述中，了解用于与 属性窗口 IDE Visual Studio交互的接口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Properties window
ms.assetid: 289ed4f2-02ac-4899-855e-42dfe57ee05f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 2377ee69458f3becb94ee79b8cd580fdbb92823d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122028938"
---
# <a name="properties-window-overview"></a>属性窗口概述
" **属性** "窗口用于显示在集成开发环境中可用的两种主要类型的窗口中选择的对象的属性，这些窗口 ([!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE) 。 这两种类型的窗口包括：

- 工具窗口，例如解决方案资源管理器、类视图和对象浏览器

- 包含窗体设计器、XML 编辑器和 HTML 编辑器等编辑器和设计器的文档窗口

## <a name="using-the-properties-window"></a>使用"属性"窗口
 " **属性** "窗口显示单个或多个选定项的属性。 如果选择了多个项，则显示所有选定对象的所有属性的交集。

 与窗体设计窗口或 HTML 编辑器（使用 COM+ 元数据）中的选定对象相关的事件将显示在" **属性"窗口中** 。 例如，可以选择一个按钮并显示其关联的事件，例如可以链接到该 `OnClick` 按钮的事件。

 "属性"窗口中 **显示** 的事件主要用于绑定到代码的对象。 如果编辑的文件格式与代码没有任何关系，则没有任何事件。 只有在运行的代码与特定对象关联的某些事件之间存在绑定时，事件才显示在"属性"窗口中。 例如，在激活选定对象时执行的选定对象后面的代码就是这种情况。

 下表列出了"属性"窗口使用 **的主要** 接口。

|接口名称|说明|
|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties>|提供"属性"窗口的 **类别列表** ，将每个属性映射到一个类别。|
|[IDispatch 接口](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)|向编程工具和支持自动化的其他应用程序公开对象的方法和属性。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder>|提供省略号 (...) 按钮，这些按钮称为 *生成器* ，用于打开由对象本身实现的模式对话框窗口。 当用户在文本字段中无法轻松键入值时使用。 例如，它可用于打开确定 RGB 值的颜色选取器。|
|<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>|提供对对象的访问权限，这些对象用于更新"属性"窗口中 **显示** 的信息。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 由 VSPackage 针对每个窗口实现，该窗口包含具有要显示的相关属性的可选择对象。|
|<xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo>|提供有关对象类型的信息，例如接口的方法和 结构的字段。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>|使 VSPackage 能够接收选择事件的通知，并检索有关当前项目层次结构、项、元素值和命令 UI 上下文的信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiItemSelect>|为环境提供对多个选择的访问权限。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>|用于在"属性"窗口中显示某些属性上提供 **本地化** 名称。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents>|通知已注册的 VSPackage 对当前所选内容、元素值或命令 UI 上下文的更改。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>|向环境通知当前选择中的更改，并提供对与新选择相关的层次结构和项信息的访问权限。|

 有关 的进一步 `IDispatch` 信息，请参阅 MSDN 库。

## <a name="see-also"></a>请参阅
- [扩展属性](../../extensibility/internals/extending-properties.md)
- [Properties Window Fields and Interfaces](../../extensibility/internals/properties-window-fields-and-interfaces.md)
