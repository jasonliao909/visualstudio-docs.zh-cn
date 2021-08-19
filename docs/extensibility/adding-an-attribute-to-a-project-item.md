---
title: 将属性添加到 Project 项 |Microsoft Docs
description: 了解如何使用 Shell 互操作方法 GetItemAttribute 和 SetItemAttribute 将属性添加到 Visual Studio 中的项目项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- attributes [Visual Studio], adding to a project item
ms.assetid: 404a71d5-cce5-44e7-9eaf-d747c794fedb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: df176c3e52407656b66a58ac65e733e7907e59e7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122133492"
---
# <a name="add-an-attribute-to-a-project-item"></a>向项目项添加特性
方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.GetItemAttribute%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> 获取和设置项目项的特性的值。 如果该属性不存在，SetItemAttribute 将创建该属性，并将其添加到项目项元数据中。

## <a name="add-an-attribute-to-a-project-item"></a>向项目项添加特性

- 下面的代码使用 <xref:EnvDTE.DTE> 自动化对象和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> 方法将特性添加到项目项。 项目项 ID 是从项目项名称 "program" 获取的。 将属性 "MyAttribute" 添加到此项目项，并为其指定值 "MyValue"。

    ```csharp
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));
    EnvDTE.Project project = dte.Solution.Projects.Item(1);

    string uniqueName = project.UniqueName;
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));
    IVsHierarchy hierarchy;
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);
    IVsBuildPropertyStorage buildPropertyStorage = hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        uint itemId;
        string fullPath = (string)project.ProjectItems.Item("Program.cs").Properties.Item("FullPath").Value;
        hierarchy.ParseCanonicalName(fullPath, out itemId);
        buildPropertyStorage.SetItemAttribute(itemId, "MyAttribute", "MyValue");
    }

    ```

## <a name="see-also"></a>请参阅
- [在 MSBuild 项目文件中保存数据](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)
