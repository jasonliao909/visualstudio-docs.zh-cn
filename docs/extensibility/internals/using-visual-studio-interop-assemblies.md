---
title: 使用Visual Studio互操作程序集|Microsoft Docs
description: 了解Visual Studio互操作程序集如何允许托管应用程序访问提供扩展性Visual Studio COM 接口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, interop assemblies
- interop assemblies, Visual Studio
- managed VSPackages, interop assemblies
ms.assetid: 1043eb95-4f0d-4861-be21-2a25395b3b3c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 108e2bf16cd109f954752207cb966c472241730e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122034586"
---
# <a name="using-visual-studio-interop-assemblies"></a>使用 Visual Studio 互操作程序集
Visual Studio互操作程序集允许托管应用程序访问提供扩展性Visual Studio COM 接口。 直接 COM 接口及其互操作版本之间存在一些差异。 例如，HRESULT 通常表示为 int 值，并且需要以与异常相同的方式进行处理，并且参数 (特别是 out 参数) 处理方式不同。

## <a name="handling-hresults-returned-to-managed-code-from-com"></a>处理从 COM 返回到托管代码的 HRESULT
 当从托管代码调用 COM 接口时，请检查 HRESULT 值并根据需要引发异常。 <xref:Microsoft.VisualStudio.ErrorHandler> 类包含 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 方法，该方法根据传递给它的 HRESULT 值引发 COM 异常。

 默认情况下，每次向 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 传递值小于零的 HRESULT 时，它都会引发异常。 如果此类 HRESULT 是可接受的值，不应引发异常，那么，应在测试完其他 HRESULT 的值后，将这些值传递给 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A>。 如果所测试的 HRESULT 与显式传递到 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 的任何 HRESULT 值匹配，则不会引发异常。

> [!NOTE]
> 类包含常见 HRESULTS 的常量，例如、 和 <xref:Microsoft.VisualStudio.VSConstants> <xref:Microsoft.VisualStudio.VSConstants.S_OK> <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] HRESULTS，例如 和 <xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA> <xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT> 。 <xref:Microsoft.VisualStudio.VSConstants> 还提供 <xref:Microsoft.VisualStudio.ErrorHandler.Succeeded%2A> 和 <xref:Microsoft.VisualStudio.ErrorHandler.Failed%2A> 方法，分别对应于 COM 中的 SUCCEEDED 宏和 FAILED 宏。

 例如，在以下函数调用中，<xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> 是可接受的返回值，而其他所有小于零的 HRESULT 均表示错误。

 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdkhresultinformation/vb/vssdkhresultinformationpackage.vb" id="Snippet1":::
 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdkhresultinformation/cs/vssdkhresultinformationpackage.cs" id="Snippet1":::

 如果有多个可接受的返回值，只需在调用 <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> 时将其他 HRESULT 值追加到列表中。

 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdkhresultinformation/vb/vssdkhresultinformationpackage.vb" id="Snippet2":::
 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdkhresultinformation/cs/vssdkhresultinformationpackage.cs" id="Snippet2":::

## <a name="returning-hresults-to-com-from-managed-code"></a>从托管代码将 HRESULT 返回到 COM
 如果没有发生异常，托管代码会向调用它的 COM 函数返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK>。 COM 互操作支持托管代码中强类型化的常见异常。 例如，收到不可接受的 `null` 参数的方法会引发 <xref:System.ArgumentNullException>。

 如果不确定要引发哪个异常，但知道要返回到 COM 的 HRESULT，则可以使用 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> 方法引发相应的异常。 即使是非标准错误（例如 <xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>），也同样可行。 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> 会尝试将传递给它的 HRESULT 映射到强类型化的异常。 如果无法映射，它会改为引发一般的 COM 异常。 最终结果是，从托管代码传递到 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> 的 HRESULT 返回到调用它的 COM 函数中。

> [!NOTE]
> 异常会降低性能，它用于指示程序的异常状况。 对于所发生的状况，通常应以内联方式处理，而不是引发异常。

## <a name="iunknown-parameters-passed-as-type-void"></a>作为类型 void 传递的 IUnknown 参数**
 查找在 COM 接口中定义为类型，但在互操作程序集方法原型中定义为 `void **` 类型的 [out] `[``iid_is``]` [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 参数。

 有时，COM 接口生成 `IUnknown` 对象，然后 COM 接口将该对象作为类型 传递 `void **` 。 这些接口尤其重要，因为如果在 IDL 中将变量定义为 [out]，则对象使用 方法进行 `IUnknown` 引用 `AddRef` 计数。 如果对象未正确处理，则会发生内存泄漏。

> [!NOTE]
> 由 `IUnknown` COM 接口创建且在 [out] 变量中返回的对象在未显式释放时会导致内存泄漏。

 处理此类对象的托管方法应视为指向对象的指针，并 <xref:System.IntPtr> `IUnknown` 调用 <xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A> 方法来获取对象。 然后，调用方应将返回值强制转换到任何适当的类型。 不再需要对象时，调用 <xref:System.Runtime.InteropServices.Marshal.Release%2A> 以释放它。

 下面是调用 方法并 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A> 正确处理 对象 `IUnknown` 的示例：

```
MyClass myclass;
Object object;
IntPtr pObj;
Guid iid = Typeof(MyClass).Guid;
int hr = windowFrame.QueryViewInterface(ref iid, out pObj);
if (NativeMethods.Succeeded(hr))
{
    try
    {
        object = Marshal.GetObjectForIUnknown(pObj);
        myclass = object;
    }
    finally
    {
        Marshal.Release(pObj);
    }
}
else
{
    // error calling QueryViewInterface
}
```

> [!NOTE]
> 已知以下方法将 `IUnknown` 对象指针作为类型 传递 <xref:System.IntPtr> 。 请根据本部分中所述处理它们。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.CreateProject%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>

## <a name="optional-out-parameters"></a>可选 [out] 参数
 查找在 COM 接口中定义为 [out] 数据类型 (、 等) 的参数，但在互操作程序集方法原型中定义为相同数据类型的 `int` `object` [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 数组的参数。

 某些 COM 接口（如 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A> ）将 [out] 参数视为可选参数。 如果不需要对象，这些 COM 接口将指针返回为该参数的值，而不是 `null` 创建 [out] 对象。 这是设计的结果。 对于这些接口，假定指针是 VSPackage 正确行为的一部分， `null` 并且不会返回任何错误。

 由于 CLR 不允许 [out] 参数的值为 ，因此这些接口的设计行为的一部分不能 `null` 直接在托管代码中使用。 受影响的接口的互操作程序集方法通过将相关参数定义为数组来解决此问题，因为 CLR 允许传递 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] `null` 数组。

 这些方法的托管实现应在没有返回任何项时将数组 `null` 放入 参数中。 否则，请创建一个类型正确的单元素数组，将返回值放入数组中。

 从具有可选 [out] 参数的接口接收信息的托管方法以数组方式接收参数。 只需检查数组的第一个元素的值。 如果不是 ， `null` 则将第一个元素视为原始参数。

## <a name="passing-constants-in-pointer-parameters"></a>在指针参数中传递常量
 查找在 COM 接口中定义为 [in] 指针，但在互操作程序集方法原型中定义为类型的 <xref:System.IntPtr> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 参数。

 当 COM 接口传递特殊值（如 0、-1 或 -2）而不是对象指针时，会出现类似问题。 与 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 不同，CLR 不允许将常量强制转换为 对象。 互 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 操作程序集将参数定义为 <xref:System.IntPtr> 类型。

 这些方法的托管实现应利用这样一个事实：类同时具有 和 构造函数，以根据情况从对象或整数 <xref:System.IntPtr> `int` `void *` <xref:System.IntPtr> 常量创建 。

 接收此 <xref:System.IntPtr> 类型的参数的托管方法应该使用 <xref:System.IntPtr> 类型转换运算符来处理结果。 首先将 <xref:System.IntPtr> 转换为 `int` ，然后根据相关的整数常量测试它。 如果没有值匹配，请将其转换为所需类型的对象并继续。

 有关这种情况的示例，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A> 。

## <a name="ole-return-values-passed-as-out-parameters"></a>作为 [out] 参数传递的 OLE 返回值
 查找在 COM 接口中具有返回值，但在互操作程序集方法原型中具有返回值和附加 `retval` `int` [out] 数组 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 参数的方法。 应该清楚，这些方法需要特殊处理，因为互操作程序集方法原型具有的参数比 COM 接口 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 方法多一个。

 处理 OLE 活动的许多 COM 接口将有关 OLE 状态的信息发送回存储在接口的返回值 `retval` 中的调用程序。 相应的互操作程序集方法将信息发送回存储在 [out] 数组参数中的调用程序，而不是 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使用返回值。

 这些方法的托管实现应创建与 [out] 参数类型相同的单元素数组，并放入 参数中。 数组元素的值应与相应的 COM 相同 `retval` 。

 调用此类型的接口的托管方法应从 [out] 数组中拉取第一个元素。 可以将此元素视为相应 COM 接口 `retval` 的返回值。

## <a name="see-also"></a>请参阅
- [与非托管代码交互操作](/dotnet/framework/interop/index)
