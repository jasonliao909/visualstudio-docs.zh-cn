---
title: 在运行时验证 Project 的子类型 |Microsoft Docs
description: 了解如何让 VSPackage 验证是否存在其依赖的指定自定义项目子类型。
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
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: fca9d6b7a85de4e9c63f459d1ace0e832143f182a664cad7b6186007dd703a27
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121387793"
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

## <a name="see-also"></a>请参阅
- [Project 子类型](../extensibility/internals/project-subtypes.md)
- [Project 子类型设计](../extensibility/internals/project-subtypes-design.md)
- [按项目子类型扩展的属性和方法](../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)
