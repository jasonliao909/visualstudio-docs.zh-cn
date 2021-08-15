---
description: 此接口使表达式 (企业版) 以所需的任何格式显示属性值。
title: IDebugCustomViewer |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomViewer
helpviewer_keywords:
- IDebugCustomViewer interface
ms.assetid: 7aca27d3-c7b8-470f-b42c-d1e9d9115edd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 45ddf6c4d2c017e397e13c8f98dd4aa60a4f233aa24afb85ea03d19912f9b659
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121402969"
---
# <a name="idebugcustomviewer"></a>IDebugCustomViewer
此接口使表达式 (企业版) 以所需的任何格式显示属性值。

## <a name="syntax"></a>语法

```
IDebugCustomViewer : IUknown
```

## <a name="notes-for-implementers"></a>实现者说明
一企业版实现此接口，以自定义格式显示属性的值。

## <a name="notes-for-callers"></a>调用方说明
对 COM 函数的 `CoCreateInstance` 调用实例化此接口。 `CLSID`传递到 `CoCreateInstance` 的 从注册表获取。 调用 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) 可获取注册表中的位置。 有关详细信息以及示例，请参阅备注。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)|执行显示给定值所需的任何操作。|

## <a name="remarks"></a>备注
当无法通过正常方式显示属性的值（例如，使用数据表或其他复杂属性类型）时，会使用此接口。 由 接口表示的自定义查看器不同于类型可视化工具，它是一个外部程序，用于显示特定类型的数据 `IDebugCustomViewer` ，而不考虑企业版。 该企业版实现特定于该查看器的自定义企业版。 用户选择使用哪种类型的可视化工具，是类型可视化工具还是自定义查看器。 有关 [此过程的详细信息，请参阅可视化](../../../extensibility/debugger/visualizing-and-viewing-data.md) 和查看数据。

自定义查看器的注册方式与企业版，因此需要语言 GUID 和供应商 GUID。 只有 (知道) 名称或注册表项名称企业版。 此指标在 [DEBUG_CUSTOM_VIEWER结构中返回](../../../extensibility/debugger/reference/debug-custom-viewer.md) ，而该结构又通过调用 [GetCustomViewerList 返回](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)。 存储在指标中的值是传递给 COM 函数的 `CLSID` `CoCreateInstance` ， (示例) 。

[用于调试函数 的 SDK](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)帮助程序 `SetEEMetric` 可用于注册自定义查看器。 有关自定义查看器所需的特定注册表项，请参阅 的"表达式评估程序" `Debugging SDK Helpers` 注册表部分。 请注意，自定义查看器只需要一个指标 (由 企业版 实现者定义) 而表达式评估器需要多个预定义指标。

通常，自定义查看器提供数据的只读视图，因为提供给[DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)的[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口除了作为字符串之外，没有用于更改属性值的方法。 为了支持更改任意数据块，企业版实现 接口的同一对象上实现自定义 `IDebugProperty3` 接口。 然后，此自定义接口将提供更改任意数据块所需的方法。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>示例
此示例演示如何从属性获取第一个自定义查看器（如果该属性具有任何自定义查看器）。

```cpp
IDebugCustomViewer *GetFirstCustomViewer(IDebugProperty2 *pProperty)
{
    // This string is typically defined globally.  For this example, it
    // is defined here.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";
    IDebugCustomViewer *pViewer = NULL;
    if (pProperty != NULL) {
        CComQIPtr<IDebugProperty3> pProperty3(pProperty);
        if (pProperty3 != NULL) {
            HRESULT hr;
            ULONG viewerCount = 0;
            hr = pProperty3->GetCustomViewerCount(&viewerCount);
            if (viewerCount > 0) {
                ULONG viewersFetched = 0;
                DEBUG_CUSTOM_VIEWER viewerInfo = { 0 };
                hr = pProperty3->GetCustomViewerList(0,
                                                     1,
                                                     &viewerInfo,
                                                     &viewersFetched);
                if (viewersFetched == 1) {
                    CLSID clsidViewer = { 0 };
                    CComPtr<IDebugCustomViewer> spCustomViewer;
                    // Get the viewer's CLSID from the registry.
                    ::GetEEMetric(viewerInfo.guidLang,
                                  viewerInfo.guidVendor,
                                  viewerInfo.bstrMetric,
                                  &clsidViewer,
                                  strRegistrationRoot);
                    if (!IsEqualGUID(clsidViewer,GUID_NULL)) {
                        // Instantiate the custom viewer.
                        spCustomViewer.CoCreateInstance(clsidViewer);
                        if (spCustomViewer != NULL) {
                            pViewer = spCustomViewer.Detach();
                        }
                    }
                }
            }
        }
    }
    return(pViewer);
}
```

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
