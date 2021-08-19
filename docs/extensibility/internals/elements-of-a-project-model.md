---
title: 模型Project的元素|Microsoft Docs
description: 了解项目模型的元素，以及项目中所有项目的接口和实现Visual Studio基本结构。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], implementation considerations
- project models
- projects [Visual Studio SDK], elements
ms.assetid: a1dbe0dc-68da-45d7-8704-5b43ff7e4fc4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a3e967466bef5feabaa4e6760dfc73c2927e7b35
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110574"
---
# <a name="elements-of-a-project-model"></a>项目模型的元素
中所有项目的接口和实现共享一个基本 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 结构：项目类型的项目模型。 在项目模型（即正在开发的 VSPackage）中，创建符合设计决策的对象，并配合 IDE 提供的全局功能协同工作。 例如，虽然可以控制项目项的持久化方法，但无法控制必须持久保存文件的通知。 当用户将焦点放在打开的项目项上并选择菜单栏上"文件"菜单上的"保存"时，项目类型代码必须截获 IDE 中的 命令，保留文件，并将通知发回到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE，告知该文件不再更改。

 VSPackage 通过提供 IDE 接口访问权限的服务与 IDE 交互。 例如，通过特定服务，可以监视和路由命令，并为项目中的选择提供上下文信息。 VSPackage 所需的所有全局 IDE 功能都由服务提供。 有关服务详细信息，请参阅 [如何：获取服务](../../extensibility/how-to-get-a-service.md)。

 其他实现注意事项：

- 单个项目模型可以包含多个项目类型。

- Project类型和项目工厂独立注册到 GUID。

- 当用户通过 UI 创建新项目时，每个项目必须具有模板文件或向导来初始化 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 新项目文件。 例如， [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 模板初始化最终成为 .vcproj 文件的内容。

  下图显示了构成典型项目实现的主要接口、服务和对象。 可以使用应用程序帮助程序 `HierUtil7` 创建基础对象和其他编程样本。 有关应用程序帮助 `HierUtil7` 程序的信息，请参阅使用 [HierUtil7 ](/previous-versions/bb166212(v=vs.100))项目类通过 C++ (实现) 。

  ![Visual Studio项目模型图形Project](../../extensibility/internals/media/vsprojectmodel.gif "vsProjectModel")模型

  有关上图中列出的接口和服务以及关系图中未包含的其他可选接口的信息，请参阅 Project[模型核心组件](../../extensibility/internals/project-model-core-components.md)。

  项目可以支持命令，因此必须实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口才能通过命令上下文 GUID 参与命令路由。

## <a name="see-also"></a>请参阅
- [清单：创建新项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [使用 HierUtil7 项目类通过 C++ (实现) ](/previous-versions/bb166212(v=vs.100))
- [Project模型核心组件](../../extensibility/internals/project-model-core-components.md)
- [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
- [如何：获取服务](../../extensibility/how-to-get-a-service.md)
- [创建项目类型](../../extensibility/internals/creating-project-types.md)