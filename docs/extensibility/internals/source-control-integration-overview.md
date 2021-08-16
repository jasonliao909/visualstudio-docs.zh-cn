---
title: 源代码管理集成概述 |Microsoft Docs
description: 了解将源代码管理集成到 Visual Studio 的两种方法之间的差异：源代码管理插件和 VSPackage。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], about source control
ms.assetid: 3a46e4eb-e677-49c3-8647-d927d035a19a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 12968e24159dec5a4709ea14452feede1f8cf8ff36cd7ef9d73dba4bc679d2fb
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414412"
---
# <a name="source-control-integration-overview"></a>源代码管理集成概述
本部分比较了两种集成到 Visual Studio 源代码管理的方法;源代码管理插件和 VSPackage，它提供源代码管理解决方案并突出显示新的源代码管理功能。 Visual Studio 允许在源控件 vspackage 和源代码管理插件之间手动切换，以及基于解决方案的自动切换。

## <a name="source-control-integration"></a>源代码管理集成
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持两种类型的源代码管理集成选项。 在的所有版本中 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，你仍然可以基于源代码管理插件 API 集成插件 (以前也称为 MSSCCI api) ，它提供基本的源代码管理功能，同时 Visual Studio (UI) 使用源代码管理用户界面。 另一方面，源代码管理提供了一个适用于源代码管理集成的新的深度集成 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 路径，该路径需要在其源代码管理模型中提供高级别的复杂和自治。

 ![源代码管理概述](../../extensibility/internals/media/sourcectnrloverview.gif "SourceCtnrlOverview")

## <a name="source-control-plug-in"></a>源代码管理插件
 所有版本的 Visual Studio 都支持源代码管理插件 API 规范版本1.2 作为集成路径。 源代码管理插件实施者编写一个 DLL，该 DLL 实现源代码管理插件 API 函数以进行源代码管理集成和注册，如 [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)中所述。 在此方法中，集成开发环境 (IDE) 使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] UI 作为对话框，如 "签入"、"签出"、"工具"/"选项" 属性页、工具栏和源控件标志符号。 严格遵守源代码管理插件 API 可确保轻松地集成到 Visual Studio，并为用户提供无故障的体验。 这意味着源代码管理插件必须实现 API 中详细介绍的大部分函数和回调。

 若要使用源代码管理插件 API 实现源代码管理插件，请执行以下步骤：

1. 创建一个 DLL，该 DLL 实现 [源代码管理插件](../../extensibility/source-control-plug-ins.md)中指定的函数。

2. 通过 [执行如何：安装源代码管理插件](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)) 中所述的相应注册表项来注册 DLL (。

3. 创建帮助器 UI，并在由源代码管理适配器包提示 (通过源代码管理插件处理源代码管理功能的 Visual Studio 组件时显示) 

   作为源代码管理命令的响应，Visual Studio IDE 为基本操作提供标准 UI，然后通过源代码管理插件 API 中定义的函数将信息传递给源代码管理插件。 对于高级选项，可以在上调用源代码管理插件来提供自己的 UI，例如，浏览源代码管理的项目。 这意味着，在处理源代码管理时，用户可能会看到两个可能不同的 UI 样式： Visual Studio 提供的 ui 和源代码管理插件提供的 ui。 这对于高级源代码管理操作最明显。

### <a name="drawbacks-to-implementing-a-source-control-plug-in"></a>实现源代码管理插件的缺点

- 对于高级功能，用户可能会看到两种不同的接口样式，这可能会导致混淆。

- 源代码管理插件限制为源代码管理插件 API 隐含的源代码管理模型。

- 对于某些源代码管理方案，源代码管理插件 API 可能过于严格。

### <a name="advantages-to-implementing-a-source-control-plug-in"></a>实现源代码管理插件的优点

- Visual Studio 提供所有基本源代码管理操作的所有 UI，使源代码管理插件不必实现可能的复杂 UI。

- 由于存在严格的 API，源代码管理插件可以轻松地与外部源代码管理程序交互，以提供更广泛的功能;Visual Studio 并不关心源代码管理功能的实现方式，而只是根据源代码管理插件 API 完成此操作。

- 实现源代码管理插件比源代码管理 VSPackage 更容易。

## <a name="source-control-vspackage"></a>源代码管理 VSPackage
 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]允许深度集成到 Visual Studio，并完全控制源代码管理功能并完成 Visual Studio 提供的源代码管理用户界面的替换。 源代码管理 VSPackage 注册到 Visual Studio 并提供源代码管理功能。 尽管可以向 Visual Studio 中注册多个源代码管理 vspackage，但其中一次只能有一个处于活动状态。 源代码管理 VSPackage 可以完全控制源代码管理功能，并可在处于活动状态时 Visual Studio。 可能在系统中注册的所有其他源代码管理 Vspackage 都处于非活动状态，并且不会显示任何 UI。

 实现源代码管理 VSPackage 需要 "全部或无" 策略。 源代码管理 VSPackage 的创建者必须投入大量精力来实现一些源代码管理接口和新的 UI 元素 (对话框、菜单和工具栏) ，以涵盖整个源代码管理功能。 有关更多详细信息，请参阅 [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md) 。

### <a name="drawbacks-to-implementing-a-source-control-vspackage"></a>实现源代码管理的缺点 VSPackage

- VSPackage 必须实现多个复杂接口，才能成功地与 Visual Studio 集成。

- VSPackage 必须提供源控件所需的所有 UI;Visual Studio 不会在此区域提供帮助。

- 源代码管理 VSPackage 是它紧密绑定到 Visual Studio 的，并且不能与独立程序一起操作，因此功能不能与源代码管理程序的外部版本轻松共享。

### <a name="advantages-to-implementing-a-source-control-vspackage"></a>实现源代码管理的优点 VSPackage

- 由于 VSPackage 对源代码管理 UI 和功能具有完全控制，因此向用户提供了一个无缝接口用于源代码管理。

- VSPackage 不限于特定的源代码管理模型。

## <a name="see-also"></a>请参阅
- [源代码管理](../../extensibility/internals/source-control.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)
- [源代码管理中的新增功能](../../extensibility/internals/what-s-new-in-source-control.md)
