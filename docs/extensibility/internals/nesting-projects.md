---
title: 嵌套项目|Microsoft Docs
description: 了解嵌套项目，使使用 VSPackage 的应用程序开发人员能够将相似类型的项目组合到一Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project nesting
- nested projects
- projects [Visual Studio SDK], child projects
- projects [Visual Studio SDK], nesting
ms.assetid: 12cce037-9840-4761-845e-5abd5fb317b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 86998a5af95a8c8460bfe70c09bc456bde37701d06d1a382663c0c7d83f139ab
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121321319"
---
# <a name="nesting-projects"></a>嵌套项目
Enterprise VS 包的应用程序开发人员可以使用项目嵌套 在 中方便地将类似 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] *类型的项目组合在一起*。 例如，Enterprise模板项目使用嵌套项目将项目分组到类别中。 业务外观项目、Web UI 项目等在一个类别中组合在一起。

 在此方案中，开发人员可以嵌套在每个父项目下的项目数没有限制，尽管开发人员可以编程方式提供限制。 此类型的分组也可以成为递归的，在这种情况下，与子项目类型相同的项目可以嵌套在子级下，成为子项目的子项目，子项目是父级的子项目。

 Project嵌套不是 的固有部分 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 必须编写代码才能在子项目中启用嵌套和子项目嵌套。 父项目是一种特殊的 VSPackage 或项目类型，使用其自己的 GUID 创建和注册，其中包括实现项目嵌套所需的代码。

 可以在如何：实现嵌套项目 中查找如何 [嵌套项目的示例](../../extensibility/internals/how-to-implement-nested-projects.md)。

## <a name="nested-projects-example"></a>嵌套项目示例
 ![嵌套项目解决方案](../../extensibility/internals/media/vsnestedprojects.gif "vsNestedProjects") 嵌套项目示例

## <a name="see-also"></a>另请参阅
- [卸载和重新加载嵌套项目的注意事项](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [嵌套项目的向导支持](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [实现嵌套项目的命令处理](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [筛选嵌套项目的 AddItem 对话框](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [上下文参数](../../extensibility/internals/context-parameters.md)
- [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
