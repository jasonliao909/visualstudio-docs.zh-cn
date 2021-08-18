---
title: 使用 Project 工厂创建 Project 实例 |Microsoft Docs
description: 了解如何在 Visual Studio 集成开发环境中使用项目工厂创建项目类实例 (IDE) 。
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
ms.openlocfilehash: 1fc9fa9d4f10c59d4e17f2314cdbed80da26c3b5e24b115fb755c1fce9645b24
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448190"
---
# <a name="create-project-instances-by-using-project-factories"></a>使用项目工厂创建项目实例
中的 Project 类型 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使用 *项目工厂* 创建项目对象的实例。 项目工厂类似于 cocreatable COM 对象的标准类工厂。 但是，项目对象不是 cocreatable;它们只能通过使用项目工厂来创建。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]当用户加载现有项目或在中创建新项目时，IDE 将调用在 VSPackage 中实现的项目工厂 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 新的项目对象为 IDE 提供了足够的信息来填充 **解决方案资源管理器**。 新的项目对象还提供了所需的接口，以便支持 IDE 启动的所有相关 UI 操作。

 可以在项目的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> 类中实现接口。 通常，它驻留在其自己的模块中。

 支持由所有者聚合的项目必须在其项目文件中保存所有者密钥。 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> 具有所有者键的项目上调用方法时，拥有的项目会将其所有者密钥转换为项目工厂 GUID，然后调用 `CreateProject` 此项目工厂上的方法来执行实际的创建。

## <a name="create-an-owned-project"></a>创建拥有的项目
 所有者在两个阶段创建拥有的项目：

1. 通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.PreCreateForOwner%2A> 方法。 这为拥有的项目提供了根据输入控制创建聚合项目对象的机会 `IUnknown` 。 拥有的项目将内部 `IUnknown` 和聚合对象传递回所有者项目。 这为拥有的项目提供存储内部的机会 `IUnknown` 。

2. 通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A> 方法。 调用此方法时，拥有的项目将执行其所有实例化，而不是调用，这 `IVsProjectFactory::CreateProject` 种情况不会是所拥有的项目的情况。 输入 `VSOWNEDPROJECTOBJECT` 枚举通常是聚合的拥有项目。 所拥有的项目可以使用此变量来确定其项目对象是否已创建 (cookie 不等于 NULL) 或必须 (cookie 等于 NULL) 创建。

   Project 类型由唯一项目 GUID 标识，类似于 cocreatable COM 对象的 CLSID。 通常，一个项目工厂处理一个项目类型的实例，尽管可以让一个项目工厂处理多个项目类型 GUID。

   Project 类型与特定文件扩展名关联。 当用户尝试打开现有项目文件或尝试通过克隆模板来创建新项目时，IDE 将使用该文件的扩展名来确定相应的项目 GUID。

   IDE 一旦确定是否必须创建一个新项目或打开特定类型的现有项目，IDE 就会使用 **[HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Projects]** 下的系统注册表中的信息来查找哪些 VSPackage 实现了所需的项目工厂。 IDE 将加载此 VSPackage。 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 方法中，VSPackage 必须通过调用方法将其项目工厂注册到 IDE <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes.RegisterProjectType%2A> 。

   接口的主要方法 `IVsProjectFactory` 是 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> ，它应处理两个方案：打开现有项目并创建新项目。 大多数项目将其项目状态存储在项目文件中。 通常，通过复制传递到方法的模板文件 `CreateProject` ，然后打开副本来创建新项目。 通过直接打开传递给方法的项目文件来实例化现有项目 `CreateProject` 。 `CreateProject`方法可根据需要向用户显示其他 UI 功能。

   项目还可以不使用文件，而是将其项目状态存储在文件系统以外的存储机制中，如数据库或 Web 服务器。 在这种情况下，传递给方法的文件名参数 `CreateProject` 实际上不是文件系统路径，而是用于标识项目数据的唯一字符串（URL）。 不需要复制传递到的模板文件 `CreateProject` 来触发要执行的相应构造序列。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes>
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
