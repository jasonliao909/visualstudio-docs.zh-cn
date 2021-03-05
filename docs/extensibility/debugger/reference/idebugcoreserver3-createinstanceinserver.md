---
description: 在服务器上创建调试引擎的实例。
title: IDebugCoreServer3：： CreateInstanceInServer |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::CreateInstanceInServer
helpviewer_keywords:
- IDebugCoreServer3::CreateInstanceInServer
ms.assetid: 76f36bae-f6ab-413c-a8a9-8808bfeba05b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dc3a24e28c378bda34034822aedf4d35e5a6313e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102154673"
---
# <a name="idebugcoreserver3createinstanceinserver"></a>IDebugCoreServer3::CreateInstanceInServer
在服务器上创建调试引擎的实例。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateInstanceInServer(
   LPCWSTR  szDll,
   WORD     wLangId,
   REFCLSID clsidObject,
   REFIID   riid,
   void**   ppvObject
);
```

```csharp
int CreateInstanceInServer(
   string     szDll,
   ushort     wLangID,
   ref Guid   clsidObject,
   ref Guid   riid,
   out IntPtr ppvObject
);
```

## <a name="parameters"></a>参数
`szDll`\
中用于实现参数中指定的 CLSID 的 dll 的路径 `clsidObject` 。 如果是 `NULL` ，则调用 COM 的 `CoCreateInstance` 函数。

`wLangId`\
中调试引擎的区域设置。 如果不应调用 [SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md) 方法，则这可能为0。

`clsidObject`\
中要创建的调试引擎的 CLSID。

`riid`\
中要从类对象中检索的特定接口的接口 ID。

`ppvObject`\
[out] `IUnknown` 实例化对象的接口。 将此对象强制转换或封送到所需的接口。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
- [SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)
