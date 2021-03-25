---
title: 在运行时验证项目的子类型 |Microsoft Docs
description: 了解如何让 VSPackage 验证是否存在其依赖的指定自定义项目子类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes
- check subtypes
ms.assetid: b87780ec-36a3-4e9a-9ee2-7abdc26db739
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c52d3297ce4903cb8f8e7cb2f9ab5169d21ac94e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062598"
---
# <a name="verify-subtypes-of-a-project-at-run-time"></a>在运行时验证项目的子类型
依赖于自定义项目子类型的 VSPackage 应该包含用于查找子类型的逻辑，以便在子类型不存在时可以正常失败。 下面的过程演示如何验证是否存在指定的子类型。

### <a name="to-verify-the-presence-of-a-subtype"></a>验证子类型是否存在

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>通过将以下代码添加到 VSPackage，以对象的形式从项目和解决方案对象获取项目层次结构。

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

2. 将层次结构强制转换为 <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected> 接口。

    ```csharp
    IVsAggregatableProjectCorrected AP;
    AP = hierarchy as IVsAggregatableProjectCorrected;

    ```

3. 通过调用获取项目类型 Guid 的列表 <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected.GetAggregateProjectTypeGuids%2A> 。

    ```csharp
    string projTypeGuids = AP.GetAggregateProjectTypeGuids().ToUpper();

    ```

4. 检查列表中是否有指定子类型的 GUID。

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
- [按项目子类型扩展的属性和方法](../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)
