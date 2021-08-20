---
title: 设计器初始化和元数据配置|Microsoft Docs
description: 了解 Visual Studio SDK 如何促进 VSPackage 控制设计器或设计器组件的初始化及其元数据。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK], initializing
- designers [Visual Studio SDK], configuring metadata
ms.assetid: f7fe9a7e-f669-4642-ad5d-186b2e6e6ec9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 2954d551b1a35c2de5e951111e746227aa9987a5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122159537"
---
# <a name="designer-initialization-and-metadata-configuration"></a>设计器初始化和元数据配置

与设计器或设计器组件关联的元数据和筛选器属性的操作为应用程序提供了一种机制，用于定义特定设计器使用哪些工具来处理不同的对象 (如数据结构、类或图形实体) 、何时设计器可用，以及如何配置 Visual Studio IDE 以支持设计器 (（例如，工具箱类别或选项卡可用的) ）。 <xref:System.Type> 

提供了多种机制，有助于控制设计器或设计器组件的初始化以及 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] VSPackage 对元数据的操作。

## <a name="initialize-metadata-and-configuration-information"></a>初始化元数据和配置信息
 由于它们按需加载，因此在实例化设计器之前，Visual Studio环境可能尚未加载 VSPackage。 因此，VSPackage 不能在创建时（即处理事件）使用标准机制配置设计器或设计器 <xref:System.ComponentModel.Design.IDesignerEventService.DesignerCreated> 组件。 相反，VSPackage 实现 接口的实例并注册自身以提供自定义项，称为 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> 设计图面扩展。

### <a name="customize-initialization"></a>自定义初始化

自定义设计器、组件或设计器图面涉及：

1. 修改设计器元数据并有效地更改访问 <xref:System.Type> 或转换特定内容。

    这通常通过 或 <xref:System.Drawing.Design.UITypeEditor> 机制 <xref:System.ComponentModel.TypeConverter> 完成。

    例如，初始化基于 的设计器时，Visual Studio 环境会修改与设计器一起使用的对象的 ，以使用资源管理器获取位图而不是 <xref:System.Windows.Forms> <xref:System.Drawing.Design.UITypeEditor> <xref:System.Web.UI.WebControls.Image> 文件系统。

2. 例如，通过订阅事件或获取项目配置信息来与环境集成。 可以通过获取 接口来获取项目配置信息并订阅 <xref:System.ComponentModel.Design.ITypeResolutionService> 事件。

3. 通过激活适当的工具箱类别，或者通过向设计器应用 类的实例来限制设计器的适用性，来修改 <xref:System.ComponentModel.ToolboxItemFilterAttribute> 用户环境。

### <a name="designer-initialization-by-a-vspackage"></a>VSPackage 的设计器初始化

VSPackage 应处理设计器初始化，其操作包括：

1. 创建实现 类 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> 的对象。

   > [!NOTE]
   > <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>类永远不应在类的同一对象上 <xref:Microsoft.VisualStudio.Shell.Package> 实现。

2. 注册实现 为 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> 的类，为 VSPackage 的设计器扩展提供支持。 通过向提供 VSPackage 的 实现的 类应用 、 和 的实例来  <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute> <xref:Microsoft.VisualStudio.Shell.ProvideObjectAttribute> 注册 <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> 类 <xref:Microsoft.VisualStudio.Shell.Package> 。

每当创建设计器或设计器组件时，Visual Studio环境：

- 访问每个已注册的设计图面扩展提供程序。

- 实例化并初始化每个设计图面扩展提供程序的 对象 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> 的实例。

- 根据情况调用每个设计图面扩展提供程序 (<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnDesignerCreated%2A> <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnComponentCreated%2A> 方法) 。

将 对象作为 VSPackage 的成员实现时 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> ，必须了解：

- 此Visual Studio环境不提供对特定提供程序修改的元数据或其他配置 `DesignSurfaceExtension` 设置的任何控制。 两个或多个提供程序可能会以冲突的方式修改同一设计器功能，最终 `DesignSurfaceExtension` 修改是明确的。 不确定上次应用的修改。

- 通过向特定设计器应用 的实例，可以显式限制对象的 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> <xref:System.ComponentModel.ToolboxItemFilterAttribute> 实现。 有关工具箱项 **筛选** 的详细信息，请参阅 和 <xref:System.ComponentModel.ToolboxItemFilterAttribute> <xref:System.ComponentModel.ToolboxItemFilterType> 。

## <a name="additional-metadata-provisioning"></a>其他元数据预配

VSPackage 可以在设计时更改设计器或设计器组件的配置。

<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>类可以编程方式使用，也可以应用于提供设计器的 VSPackage。

类的实例 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> 用于修改在设计图面上创建的组件的元数据。 例如，可以替换对象使用的默认属性 <xref:System.Windows.Forms.CommonDialog> 浏览器和自定义属性浏览器。

应用于 VSPackage 的 实现的实例提供的修改 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> <xref:Microsoft.VisualStudio.Shell.Package> 可以有两个范围之一：

- 全局 - 适用于给定组件的所有新实例

- 本地 -- 仅适用于在当前 VSPackage 提供的设计图面上创建的 组件的实例。

应用于 VSPackage 的 实现的实例的 属性 `IsGlobal` <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> <xref:Microsoft.VisualStudio.Shell.Package> 确定此范围。

将 属性应用于 的实现，将 对象的 属性设置为 ，如下所示，将更改整个 Visual Studio <xref:Microsoft.VisualStudio.Shell.Package> <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute.IsGlobal%2A> <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> `true` 环境的浏览器：

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=true`  `)]`

`internal class MyPackage : Package {}`

如果全局标志设置为 `false` ，则元数据更改是当前 VSPackage 支持的当前设计器的本地更改：

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=false`  `)]`

`internal class MyPackage : Package {}`

> [!NOTE]
> 设计图面仅支持创建组件，因此只有组件才能具有本地元数据。 在以上示例中，我们尝试修改 属性，例如 `Color` 对象的 属性。 如果 `false` 为全局标志传入 ，则 永远不会出现，因为 `CustomBrowser` 设计器实际上从未创建 的实例 `Color` 。 对于控件、计时器和对话框等组件，将全局标志 `false` 设置为 很有用。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>
- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>
- <xref:System.ComponentModel.ToolboxItemFilterType>
- [扩展设计时支持](/previous-versions/37899azc(v=vs.140))