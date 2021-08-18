---
title: Project建模 |Microsoft Docs
description: 了解为你的新项目类型和项目自动化遵循的路径创建自动化所需的标准项目对象。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- automation [Visual Studio SDK], implementing project objects
- project models, automation
ms.assetid: c8db8fdb-88c1-4b12-86fe-f3c30a18f9ee
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 20db69ce89fcc2f4137682e46c04f0efb9f557c9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122057208"
---
# <a name="project-modeling"></a>项目建模
为项目提供自动化的下一步是实现标准项目对象： <xref:EnvDTE.Projects> 和 `ProjectItems` 集合; 和 `Project` <xref:EnvDTE.ProjectItem> 对象; 以及对实现唯一的剩余对象。 这些标准对象在 Dteinternal 文件中定义。 BscPrj 示例中提供了标准对象的实现。 您可以使用这些类作为模型来创建自己的标准项目对象，这些对象与其他项目类型的项目对象并行。

 自动化使用者假定能够调用 <xref:EnvDTE.Solution> ( " `<UniqueProjName>")` 和 <xref:EnvDTE.ProjectItems> (`n`) 其中 n 是用于获取解决方案中特定项目的索引号。 进行此自动化调用将导致环境 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.GetProperty%2A> 在适当的项目层次结构上调用，同时将 VSITEMID_ROOT 作为 ItemID 参数传递，并将其 VSHPROPID_ExtObject 为 VSHPROPID 参数。 `IVsHierarchy::GetProperty` 返回一个 `IDispatch` 指针，该指针指向提供 `Project` 已实现的核心接口的自动化对象。

 下面是的语法 `IVsHierarchy::GetProperty` 。

 `HRESULT GetProperty (`

 `VSITEMID` `itemid`,

 `VSHPROPID` `propid`,

 `VARIANT` `*pvar`

 `);`

 项目可容纳嵌套并使用集合来创建项目项组。 层次结构如下所示。

```
Projects
  |- Project
      |- ProjectItems (a collection of ProjectItem)
          |- ProjectItem (single object) or ProjectItems (another collection)
```

 嵌套意味着 <xref:EnvDTE.ProjectItem> 对象可以 <xref:EnvDTE.ProjectItems> 同时集合，因为 `ProjectItems` 集合可以包含嵌套的对象。 基本 Project 示例不演示此嵌套。 通过实现该 `Project` 对象，您可以参与类似于树的结构，该结构反映了总体自动化模型的设计。

 项目自动化遵循下图中的路径。

 Project 自动化![Visual Studio Project 对象](../../extensibility/internals/media/projectobjects.gif "ProjectObjects")

 如果未实现 `Project` 对象，环境仍将返回 `Project` 仅包含项目名称的泛型对象。

## <a name="see-also"></a>请参阅
- <xref:EnvDTE.Projects>
- <xref:EnvDTE.ProjectItem>
- <xref:EnvDTE.ProjectItems>
