---
title: 向导|Microsoft Docs
description: 了解如何在向导的可用向导和模板之间列出Visual Studio以及向导在 IDE 中必须满足的要求。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], providing wizard support
ms.assetid: 59d9a77f-ee80-474b-a14f-90f477ab717b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: e2169f58b7933557057618bc112834cd3a58b0a9
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139550073"
---
# <a name="wizards"></a>向导
创建向导后 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，通常需要将其添加到 IDE (集成开发) 以便其他人可以使用它。 然后，添加的向导会显示在"添加新 **Project或****"添加新项"** 对话框中。 若要 **查看"添加新** Project"或"添加新项"对话框，请右键单击 解决方案资源管理器 中的打开解决方案 **，** 指向"添加"，然后单击"新建Project"或 **"新建****项"**。

 可以在 中实现向导，让用户在打开"添加新项 **Project"** 对话框或"添加新项"对话框或右键单击 解决方案资源管理器 中的项时，从可用 **值的树视图中选择。**[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]

 在向导中，可以提供本地化新项目或项的名称的选项，并且可以确定用户在选择向导时将看到的图标。 还可以控制新项相对于其他可用项的显示顺序;项不一定按字母顺序组织。

 还可以根据打开向导时传递给向导的自定义参数，提供以不同方式启动的向导。

 本节中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的主题讨论为导致"添加新 Project"和"添加新项"对话框而实现的文件，以列出可用向导和模板中的向导，以及向导在 IDE 中正常运行必须满足的要求。

## <a name="in-this-section"></a>本节内容
- [模板目录说明 (.Vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)

 概述哪些模板目录说明文件，并说明它们在 IDE 中如何显示与对话框中的项目关联的文件夹、向导 .vsz 文件和模板文件。

- [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)

 说明 IDE 如何启动向导并列出 .vsz 文件的三个部分。

- [向导界面 (IDTWizard)](../../extensibility/internals/wizard-interface-idtwizard.md)

 `IDTWizard`描述向导必须实现以在 IDE 中工作的接口。

- [上下文参数](../../extensibility/internals/context-parameters.md)

 说明如何实现向导，以及当 IDE 将上下文参数传递给实现时发生的情况。

- [自定义参数](../../extensibility/internals/custom-parameters.md)

 说明如何在向导启动后使用自定义参数来控制向导的操作。

## <a name="related-sections"></a>相关章节
- [项目类型](../../extensibility/internals/project-types.md)

 提供指向其他主题的链接，这些主题提供有关如何设计新项目类型的信息。

- [扩展项目](../../extensibility/extending-projects.md)

 介绍如何使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目和解决方案来组织代码文件和资源文件，以及如何实现源代码管理。
