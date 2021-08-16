---
title: 持久保存项目Project属性|Microsoft Docs
description: 了解如何通过将 属性存储在扩展项目类型的项目文件中来保留添加到项目项的属性。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: how-to
helpviewer_keywords:
- properties, adding to a project item
- project items, adding properties
ms.assetid: d7a0f2b0-d427-4d49-9536-54edfb37c0f3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: e201b60ea4634c6960d6e98c64214deadd62a6b7608cb73d15b71bf2a497254f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121305277"
---
# <a name="persist-the-property-of-a-project-item"></a>保留项目项的 属性
你可能想要保留添加到项目项的属性，例如源文件的作者。 为此，可以将 属性存储在项目文件中。

 在项目文件中保留属性的第一步是获取项目的层次结构作为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 接口。 可以使用自动化或 获取此接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> 。 获取接口后，可以使用它来确定当前选择的项目项。 获得项目项 ID 后，可以使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> 添加 属性。

 在下列过程，你将在项目文件中保留具有 值的 *VsPkg.cs* `Author` `Tom` 属性。

## <a name="to-obtain-the-project-hierarchy-with-the-dte-object"></a>使用 DTE 对象获取项目层次结构

1. 将以下代码添加到 VSPackage：

    ```csharp
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));
    EnvDTE.Project project = dte.Solution.Projects.Item(1);

    string uniqueName = project.UniqueName;
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));
    IVsHierarchy hierarchy;
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);
    ```

## <a name="to-persist-the-project-item-property-with-the-dte-object"></a>使用 DTE 对象保留项目项属性

1. 将以下代码添加到上一过程中 方法中给定的代码：

    ```csharp
    IVsBuildPropertyStorage buildPropertyStorage =
        hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        uint itemId;
        string fullPath = (string)project.ProjectItems.Item(
            "VsPkg.cs").Properties.Item("FullPath").Value;
        hierarchy.ParseCanonicalName(fullPath, out itemId);
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");
    }
    ```

## <a name="to-obtain-the-project-hierarchy-using-ivsmonitorselection"></a>使用 IVsMonitorSelection 获取项目层次结构

1. 将以下代码添加到 VSPackage：

    ```csharp
    IVsHierarchy hierarchy = null;
    IntPtr hierarchyPtr = IntPtr.Zero;
    IntPtr selectionContainer = IntPtr.Zero;
    uint itemid;

    // Retrieve shell interface in order to get current selection
    IVsMonitorSelection monitorSelection =     Package.GetGlobalService(typeof(SVsShellMonitorSelection)) as     IVsMonitorSelection;
    if (monitorSelection == null)
        throw new InvalidOperationException();

    try
    {
        // Get the current project hierarchy, project item, and selection container for the current selection
        // If the selection spans multiple hierachies, hierarchyPtr is Zero
        IVsMultiItemSelect multiItemSelect = null;
        ErrorHandler.ThrowOnFailure(
            monitorSelection.GetCurrentSelection(
                out hierarchyPtr, out itemid,
                out multiItemSelect, out selectionContainer));

        // We only care if there is only one node selected in the tree
        if (!(itemid == VSConstants.VSITEMID_NIL ||
            hierarchyPtr == IntPtr.Zero ||
            multiItemSelect != null ||
            itemid == VSConstants.VSITEMID_SELECTION))
        {
            hierarchy = Marshal.GetObjectForIUnknown(hierarchyPtr)
                as IVsHierarchy;
        }
    }
    finally
    {
        if (hierarchyPtr != IntPtr.Zero)
            Marshal.Release(hierarchyPtr);
        if (selectionContainer != IntPtr.Zero)
            Marshal.Release(selectionContainer);
    }
    ```

## <a name="to-persist-the-selected-project-item-property-given-the-project-hierarchy"></a>在给定项目层次结构后保留所选项目项属性

1. 将以下代码添加到上一过程中 方法中给定的代码：

    ```csharp
    IVsBuildPropertyStorage buildPropertyStorage =
        hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");
    }
    ```

## <a name="to-verify-that-the-property-is-persisted"></a>验证属性是否持久化

1. 启动 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ，然后打开或创建解决方案。

2. 选择项目中的项目项 VsPkg.cs **解决方案资源管理器。**

3. 使用断点或确定 VSPackage 已加载且 SetItemAttribute 是否运行。

   > [!NOTE]
   > 可以在 UI 上下文 中自动加载 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid> VSPackage。 有关详细信息，请参阅加载[VSPackage。](../extensibility/loading-vspackages.md)

4. 关闭 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 项目文件，然后在 记事本。 应会看到值为 Tom 的 \<Author> 标记，如下所示：

   ```xml
   <Compile Include="VsPkg.cs">
       <Author>Tom</Author>
   </Compile>
   ```

## <a name="see-also"></a>请参阅

- [自定义工具](../extensibility/internals/custom-tools.md)
