---
title: 源代码管理集成概述|Microsoft Docs
description: 了解将源代码管理集成到 Visual Studio两种方法之间的差异：源代码管理插件和 VSPackage。
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
本部分比较了两种集成到源代码管理Visual Studio方法：源代码管理插件和 VSPackage，提供源代码管理解决方案并突出显示新的源代码管理功能。 Visual Studio允许在源代码管理 VSPackage 和源代码管理插件之间手动切换，以及基于解决方案的自动切换。

## <a name="source-control-integration"></a>源代码管理集成
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持两种类型的源代码管理集成选项。 在所有版本的 中，仍可以基于源代码管理插件 API (（以前也称为 MSSCCI API) ）集成插件，该插件在使用 Visual Studio 源代码管理用户界面 (UI) 时提供基本的源代码管理功能。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 另一方面，源代码管理 VSPackage 提供了适用于源代码管理集成的新深层集成路径，该路径要求源代码管理模型中高度复杂和 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 自治。

 ![源代码管理概述](../../extensibility/internals/media/sourcectnrloverview.gif "SourceCtnrlOverview")

## <a name="source-control-plug-in"></a>源代码管理插件
 所有版本的 Visual Studio都支持源代码管理插件 API 规范版本 1.2 作为集成路径。 源代码管理插件实现程序编写一个 DLL，该 DLL 实现源代码管理插件 API 函数，用于源代码管理集成和注册，如创建源代码管理 [插件中所述](../../extensibility/internals/creating-a-source-control-plug-in.md)。 在此方法中，集成开发环境 (IDE) 将 UI 用于对话框，例如签入、签出、工具/选项属性页、工具栏和源代码管理字形。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 严格遵循源代码管理插件 API 可确保轻松集成到 Visual Studio，并让用户获得无故障体验。 这意味着源代码管理插件必须实现 API 中详述的多数函数和回调。

 若要使用源代码管理插件 API 实现源代码管理插件，请执行以下步骤：

1. 创建一个 DLL，用于实现 [源代码管理插件 中指定的函数](../../extensibility/source-control-plug-ins.md)。

2. 按照如何：安装源代码管理插件 (中的说明创建相应的注册表项来注册 [DLL](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)) 。

3. 创建帮助程序 UI，在源代码管理适配器包提示时显示 (Visual Studio 组件，该组件通过源代码管理插件) 

   为了响应源代码管理命令，Visual Studio IDE 为基本操作提供标准 UI，然后通过源代码管理插件 API 中定义的函数将信息传递给源代码管理插件。 对于高级选项，可以调用源代码管理插件来显示自己的 UI，例如浏览源代码管理的项目。 这意味着在处理源代码管理时，用户可能会看到两种可能不同的 UI 样式：Visual Studio UI 和源代码管理插件呈现的 UI。 对于高级源代码管理操作，这一点最为明显。

### <a name="drawbacks-to-implementing-a-source-control-plug-in"></a>实现源代码管理插件的缺点

- 对于高级功能，用户可能会看到两种不同的接口样式，从而导致混淆。

- 源代码管理插件仅限于源代码管理插件 API 隐含的源代码管理模型。

- 对于某些源代码管理方案，源代码管理插件 API 可能过于严格。

### <a name="advantages-to-implementing-a-source-control-plug-in"></a>实现源代码管理插件的优点

- Visual Studio提供所有基本源代码管理操作的所有 UI，以便源代码管理插件无需实现可能复杂的 UI。

- 由于使用严格的 API，源代码管理插件可以随时与外部源代码管理程序交互，以提供更广泛的功能;Visual Studio对源代码管理功能的完成情况不太关心，只是它根据源代码管理插件 API 完成。

- 与源代码管理 VSPackage 相比，实现源代码管理插件更容易。

## <a name="source-control-vspackage"></a>源代码管理 VSPackage
 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]允许深度集成到Visual Studio完全控制源代码管理功能，并完全Visual Studio源代码管理用户界面。 源代码管理 VSPackage 向 Visual Studio，并提供源代码管理功能。 尽管多个源代码管理 VSPackage 可以注册到 Visual Studio，但其中只有一个可以在任何一次处于活动状态。 源代码管理 VSPackage 可以完全控制源代码管理功能及其在Visual Studio的外观。 可能在系统中注册的所有其他源代码管理 VSPackage 处于非活动状态，并且完全不显示任何 UI。

 实现源代码管理 VSPackage 需要"全部或无"策略。 源代码管理 VSPackage 的创建者必须投入大量精力来实现大量源代码管理接口和新的 UI 元素 (对话框、菜单和工具栏) 以涵盖整个源代码管理功能。 有关详细信息[，请参阅创建源代码管理 VSPackage。](../../extensibility/internals/creating-a-source-control-vspackage.md)

### <a name="drawbacks-to-implementing-a-source-control-vspackage"></a>实现源代码管理 VSPackage 的缺点

- VSPackage 必须实现许多复杂接口，以成功与 Visual Studio。

- VSPackage 必须提供源代码管理所需的全部 UI;Visual Studio不会提供此领域的帮助。

- 源代码管理 VSPackage 与 Visual Studio紧密关联，不能与独立程序一起运行，因此功能不能与源代码管理程序的外部版本轻松共享。

### <a name="advantages-to-implementing-a-source-control-vspackage"></a>实现源代码管理 VSPackage 的优点

- 由于 VSPackage 可以完全控制源代码管理 UI 和功能，因此会为用户提供一个无缝的源代码管理界面。

- VSPackage 并不局限于特定的源代码管理模型。

## <a name="see-also"></a>另请参阅
- [源代码管理](../../extensibility/internals/source-control.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)
- [源代码管理中的新增功能](../../extensibility/internals/what-s-new-in-source-control.md)
