---
title: 项目建模|Microsoft Docs
description: 了解创建新项目类型自动化所需的标准项目对象以及项目自动化遵循的路径。
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
ms.workload:
- vssdk
ms.openlocfilehash: b90271fcc43c627f2eb7dbb2f318427ad0d9839e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899675"
---
# <a name="project-modeling"></a>项目建模
为项目提供自动化的下一步是实现标准项目对象：和 集合、和 对象，以及实现 <xref:EnvDTE.Projects> `ProjectItems` 所特有的 `Project` <xref:EnvDTE.ProjectItem> 其余对象。 标准对象在 Dteinternal.h 文件中定义。 BscPrj 示例中提供了标准对象的实现。 可以使用这些类作为模型，创建自己的标准项目对象，这些对象与其他项目类型的项目对象并行。

 自动化使用者认为能够调用 ("和 () 其中 n 是获取解决方案中特定项目的 <xref:EnvDTE.Solution> `<UniqueProjName>")` <xref:EnvDTE.ProjectItems> `n` 索引号。 进行此自动化调用会导致环境在相应的项目层次结构上调用 ，将 VSITEMID_ROOT作为 ItemID 参数传递，VSHPROPID_ExtObject <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.GetProperty%2A> VSHPROPID 参数。 `IVsHierarchy::GetProperty` 返回 `IDispatch` 指向自动化对象的指针，该对象提供 `Project` 已实现的核心接口。

 下面是 的语法 `IVsHierarchy::GetProperty` 。

 `HRESULT GetProperty (`

 `VSITEMID` `itemid`,

 `VSHPROPID` `propid`,

 `VARIANT` `*pvar`

 `);`

 项目可以容纳嵌套，并使用集合创建项目项组。 层次结构如下所示。

```
Projects
  |- Project
      |- ProjectItems (a collection of ProjectItem)
          |- ProjectItem (single object) or ProjectItems (another collection)
```

 嵌套意味着对象 <xref:EnvDTE.ProjectItem> 可以同时 <xref:EnvDTE.ProjectItems> 被集合，因为 `ProjectItems` 集合可以包含嵌套对象。 基本项目示例不演示此嵌套。 通过实现 对象，你可以参与树状结构，该结构描述整个自动化 `Project` 模型的设计。

 项目自动化遵循下图中的路径。

 ![Visual Studio项目对象](../../extensibility/internals/media/projectobjects.gif "ProjectObjects") 项目自动化

 如果不实现 对象，则环境仍将返回仅包含项目名称 `Project` 的泛型 `Project` 对象。

## <a name="see-also"></a>另请参阅
- <xref:EnvDTE.Projects>
- <xref:EnvDTE.ProjectItem>
- <xref:EnvDTE.ProjectItems>
