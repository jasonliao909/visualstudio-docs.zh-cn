---
title: 子Project初始化序列|Microsoft Docs
description: 了解由多个项目子Visual Studio聚合的项目系统的初始化序列。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, initialization sequence
ms.assetid: f657f8c3-5e68-4308-9971-e81e3099ba29
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 1d4624649cb972c78d8c9cd9bfa8bf3a3ef9f984af3ece0f99e1ae354901467a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388599"
---
# <a name="initialization-sequence-of-project-subtypes"></a>项目子类型的初始化序列
环境通过调用 的基本项目工厂实现来构造项目 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> 。 当环境确定项目文件扩展的项目类型 GUID 列表不为空时，将开始构造项目子类型。 项目文件扩展名和项目 GUID 指定项目是 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 还是 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 项目类型。 例如，.vbproj 扩展和 {F184B08F-C81C-45F6-A57F-5ABD9991F28F} 标识 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目。

## <a name="environments-initialization-of-project-subtypes"></a>子类型Project初始化
 以下过程详细说明了由多个项目子类型聚合的项目系统的初始化序列。

1. 环境调用基本项目的 ，当项目分析其项目文件时，它会发现聚合 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> 项目类型 GUID 列表不是 `null` 。 项目将停止直接创建其项目。

2. 项目对 `QueryService` 服务调用 ，以使用 环境的 方法实现 <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> 创建项目子 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> 类型。 在此方法中，环境在访问项目类型 GUID 的列表（从最外层项目子类型开始）时，对 和 方法的实现进行递归 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> 函数调用。

     下面详细介绍了初始化步骤。

    1. 环境的 方法实现通过以下函数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> `HrCreateInnerProj` 声明调用 方法：

         \<CodeContentPlaceHolder>0</CodeContentPlaceHolder>

         首次调用此函数时，即对于最外层项目子类型，参数 和 作为 传入，函数将最外层的项目 `pOuter` `pOwner` `null` 子类型 `IUnknown` 设置为 `pOuter` 。

    2. 接下来，环境调用 `HrCreateInnerProj` 列表中具有第二个项目类型 GUID 的函数。 此 GUID 对应于第二个内部项目子类型，该子类型单步执行到聚合序列中的基项目。

    3. 现在指向最外层项目子类型的 ，并调用 的实现，然后 `pOuter` `IUnknown` 调用 `HrCreateInnerProj` <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> 的实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> 。 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> 方法中，传递最 `IUnknown` 外层项目子类型的控制 `pOuter` 。 拥有的项目 (内部项目子) 需要在此处创建其聚合项目对象。 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> 方法实现中，传递指向正在聚合的内部 `IUnknown` 项目的 的指针。 这两种方法创建聚合对象，实现需要遵循 COM 聚合规则，以确保项目子类型最终不会将引用计数控制在自身。

    4. `HrCreateInnerProj` 调用 的实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> 。 在此方法中，项目子类型执行其初始化工作。 例如，可以在 中注册解决方案事件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> 。

    5. `HrCreateInnerProj` 以递归调用 ，直到到达 (基项目) 最后一个 GUID。 对于上述每个调用，将重复步骤 c 到 d。 `pOuter` 指向每个聚合级别最 `IUnknown` 外层的项目子类型。

## <a name="example"></a>示例

以下示例详细介绍了由环境实现的方法的近似表示 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> 形式中的编程过程。 代码只是一个示例;它不应进行编译，为清楚起见，删除了所有错误检查。

```cpp
HRESULT CreateAggregateProject
(
    LPCOLESTR lpstrGuids,
    LPCOLESTR pszFilename,
    LPCOLESTR pszLocation,
    LPCOLESTR pszName,
    VSCREATEPROJFLAGS grfCreateFlags,
    REFIID iidProject,
    void **ppvProject)
{
    HRESULT hr = NOERROR;
    CComPtr<IUnknown> srpunkProj;
    CComPtr<IVsAggregatableProject> srpAggProject;
    CComBSTR bstrGuids = lpstrGuids;
    BOOL fCanceled = FALSE;
    *ppvProject = NULL;

    HrCreateInnerProj(
         bstrGuids, NULL, NULL, pszFilename, pszLocation,
         pszName, grfCreateFlags, &srpunkProj, &fCanceled);
    srpunkProj->QueryInterface(
        IID_IVsAggregatableProject, (void **)&srpAggProject));
    srpAggProject->OnAggregationComplete();
    srpunkProj->QueryInterface(iidProject, ppvProject);
}

HRESULT HrCreateInnerProj
(
    WCHAR *pwszGuids,
    IUnknown *pOuter,
    IVsAggregatableProject *pOwner,
    LPCOLESTR pszFilename,
    LPCOLESTR pszLocation,
    LPCOLESTR pszName,
    VSCREATEPROJFLAGS grfCreateFlags,
    IUnknown **ppInner,
    BOOL *pfCanceled
)
{
    HRESULT hr = NOERROR;
    CComPtr<IUnknown> srpInner;
    CComPtr<IVsAggregatableProject> srpAggInner;
    CComPtr<IVsProjectFactory> srpProjectFactory;
    CComPtr<IVsAggregatableProjectFactory> srpAggPF;
    GUID guid = GUID_NULL;
    WCHAR *pwszNextGuids = wcschr(pwszGuids, L';');
    WCHAR wszText[_MAX_PATH+150] = L"";

    if (pwszNextGuids)
    {
        *pwszNextGuids++ = 0;
    }

    CLSIDFromString(pwszGuids, &guid);
    GetProjectTypeMgr()->HrGetProjectFactoryOfGuid(
        guid, &srpProjectFactory);
    srpProjectFactory->QueryInterface(
        IID_IVsAggregatableProjectFactory,
        (void **)&srpAggPF);
    srpAggPF->PreCreateForOuter(pOuter, &srpInner);
    srpInner->QueryInterface(
        IID_IVsAggregatableProject, (void **)&srpAggInner);

    if (pOwner)
    {
        IfFailGo(pOwner->SetInnerProject(srpInner));
    }

    if (pwszNextGuids)
    {
        CComPtr<IUnknown> srpNextInner;
        HrCreateInnerProj(
            pwszNextGuids, pOuter ? pOuter : srpInner,
            srpAggInner, pszFilename, pszLocation, pszName,
            grfCreateFlags, &srpNextInner, pfCanceled);
    }

    return srpAggInner->InitializeForOuter(
        pszFilename, pszLocation, pszName, grfCreateFlags,
        IID_IUnknown, (void **)ppInner, pfCanceled);
}
```

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Flavor>
- [项目子类型](../../extensibility/internals/project-subtypes.md)
