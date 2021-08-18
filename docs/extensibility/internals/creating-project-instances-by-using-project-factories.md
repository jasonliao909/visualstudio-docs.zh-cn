---
title: 使用 Project 工厂创建Project实例|Microsoft Docs
description: 了解如何使用 IDE 集成开发环境中的项目工厂创建Visual Studio类 (实例) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project factories
- projects [Visual Studio SDK], project factories
ms.assetid: 94c90012-8669-459c-af8e-307ac242c8c4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 9c733308203cae49a79f722db4b6b1eec37f6a7e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122086672"
---
# <a name="create-project-instances-by-using-project-factories"></a>使用项目工厂创建项目实例
Project使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目工厂创建项目对象的实例。 项目工厂类似于可共同创建 COM 对象的标准类工厂。 但是，项目对象不可创建;它们只能使用项目工厂创建。

 当用户加载现有项目或在 中创建新项目时 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，IDE 调用 VSPackage 中实现的项目工厂 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 新项目对象为 IDE 提供了足够的信息来填充 **解决方案资源管理器。** 新项目对象还提供了所需的接口，用于支持由 IDE 启动的所有相关 UI 操作。

 可以在项目中的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> 类中实现 接口。 通常，它驻留在其自己的模块中。

 支持由所有者聚合的项目必须在其项目文件中保留所有者密钥。 使用所有者密钥对项目调用 方法时，拥有的项目将其所有者密钥转换为项目工厂 GUID，然后调用此项目工厂上的 方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> `CreateProject` 以执行实际创建。

## <a name="create-an-owned-project"></a>创建拥有的项目
 所有者分两个阶段创建一个拥有的项目：

1. 通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.PreCreateForOwner%2A> 方法。 这为拥有的项目提供了一个基于控制 的输入创建聚合项目对象的机会 `IUnknown` 。 拥有的项目将内部对象 `IUnknown` 和聚合对象传递回所有者项目。 这样，拥有的项目就有机会存储内部 `IUnknown` 。

2. 通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A> 方法。 当调用此方法时，拥有的项目将执行所有实例化，而不是像非拥有的项目一样 `IVsProjectFactory::CreateProject` 调用 。 输入 `VSOWNEDPROJECTOBJECT` 枚举通常是聚合拥有的项目。 拥有的项目可以使用此变量来确定其项目对象是否已创建 (cookie 不等于 NULL) 或者必须创建 (等于 NULL) 。

   Project类型由唯一项目 GUID 标识，类似于可创建 COM 对象的 CLSID。 通常，一个项目工厂会处理单个项目类型的实例的创建，但可能让一个项目工厂处理多个项目类型 GUID。

   Project类型与特定文件扩展名相关联。 当用户尝试打开现有项目文件或尝试通过克隆模板创建新项目时，IDE 将使用文件上的 扩展名来确定相应的项目 GUID。

   一旦 IDE 确定它必须创建新项目还是打开特定类型的现有项目，IDE 就会使用 **[HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Projects]** 下的系统注册表中的信息来查找哪些 VSPackage 实现了所需的项目工厂。 IDE 加载此 VSPackage。 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 方法中，VSPackage 必须通过调用 方法将其项目工厂注册到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes.RegisterProjectType%2A> IDE。

   接口的主要方法是 ，它应处理两种方案： `IVsProjectFactory` <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> 打开现有项目和创建新项目。 大多数项目将项目状态存储在项目文件中。 通常，通过创建传递给 方法的模板文件的副本，然后打开副本 `CreateProject` 来创建新项目。 通过直接打开传递给 方法的项目文件来实例化现有 `CreateProject` 项目。 `CreateProject`方法可在必要时向用户显示其他 UI 功能。

   项目还可以不使用文件，而是将项目状态存储在文件系统（如数据库或 Web 服务器）等存储机制中。 在这种情况下，传递给 方法的文件名参数实际上不是文件系统路径，而是用于标识项目数据的唯一字符串 `CreateProject` （URL）。 无需复制传递给 的模板文件， `CreateProject` 以触发要执行的适当构造序列。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes>
- [清单：创建新项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
