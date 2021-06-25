---
title: 验证项目的子类型运行时|Microsoft Docs
description: 了解如何让 VSPackage 验证它所依赖的指定自定义项目子类型是否存在。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- project subtypes
- check subtypes
ms.assetid: b87780ec-36a3-4e9a-9ee2-7abdc26db739
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 621a40e1857d7c78ec4c5be08a3b7c3808a0d48b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905468"
---
# <a name="verify-subtypes-of-a-project-at-run-time"></a>运行时验证项目的子类型
依赖于自定义项目子类型的 VSPackage 应包含用于查找该子类型的逻辑，以便如果该子类型不存在，它可能会正常失败。 以下过程演示如何验证是否存在指定的子类型。

### <a name="to-verify-the-presence-of-a-subtype"></a>验证子类型是否存在

1. 通过将以下代码添加到 VSPackage，从项目和解决方案对象获取项目 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 层次结构作为 对象。

    ```csharp
    EnvDTE.DTE dte;
    dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));

    EnvDTE.Project project;
    project = dte.Solution.Projects.Item(1);

    IVsSolution solution;
    solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));

    IVsHierarchy hierarchy;
    hierarchy = solution.GetProjectOfUniqueName(project.UniqueName);

    ```

2. 将层次结构强制转换到 <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected> 接口。

    ```csharp
    IVsAggregatableProjectCorrected AP;
    AP = hierarchy as IVsAggregatableProjectCorrected;

    ```

3. 通过调用 获取项目类型 GUID 的列表 <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected.GetAggregateProjectTypeGuids%2A> 。

    ```csharp
    string projTypeGuids = AP.GetAggregateProjectTypeGuids().ToUpper();

    ```

4. 检查指定子类型的 GUID 列表。

    ```csharp
    // Replace the string "MyGUID" with the GUID of the subtype.
    string guidMySubtype = "MyGUID";
    if (projTypeGuids.IndexOf(guidMySubtype) > 0)
    {
        // The specified subtype is present.
    }
    ```

## <a name="see-also"></a>另请参阅
- [项目子类型](../extensibility/internals/project-subtypes.md)
- [项目子类型设计](../extensibility/internals/project-subtypes-design.md)
- [由项目子类型扩展的属性和方法](../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)
