---
description: 指定要检索的线程相关信息。
title: THREADPROPERTY_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTY_FIELDS
helpviewer_keywords:
- THREADPROPERTY_FIELDS enumeration
ms.assetid: 5b88acb9-03ea-4c29-a788-f0087dccbe23
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c70e331de05b3288e1105832616acb1d3359b049
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602382"
---
# <a name="threadproperty_fields"></a>THREADPROPERTY_FIELDS
指定要检索的线程相关信息。

## <a name="syntax"></a>语法

```cpp
enum enum_THREADPROPERTY_FIELDS { 
   TPF_ID           = 0x0001,
   TPF_SUSPENDCOUNT = 0x0002,
   TPF_STATE        = 0x0004,
   TPF_PRIORITY     = 0x0008,
   TPF_NAME         = 0x0010,
   TPF_LOCATION     = 0x0020,
   TPF_ALLFIELDS    = 0xffffffff
};
typedef DWORD THREADPROPERTY_FIELDS;
```

```csharp
public enum enum_THREADPROPERTY_FIELDS { 
   TPF_ID           = 0x0001,
   TPF_SUSPENDCOUNT = 0x0002,
   TPF_STATE        = 0x0004,
   TPF_PRIORITY     = 0x0008,
   TPF_NAME         = 0x0010,
   TPF_LOCATION     = 0x0020,
   TPF_ALLFIELDS    = 0xffffffff
};
```

## <a name="fields"></a>字段
 `TPF_ID`\
 初始化/使用 `dwThreadId` [THREADPROPERTIES 结构的](../../../extensibility/debugger/reference/threadproperties.md) 字段。

 `TPF_SUSPENDCOUNT`\
 初始化/使用 `dwSuspendCount` S 结构的 `THREADPROPERTIE` 字段。

 `TPF_STATE`\
 初始化/使用 `dwThreadState` S 结构的 `THREADPROPERTIE` 字段。

 `TPF_PRIORITY`\
 初始化/使用 `bstrPriority` S 结构的 `THREADPROPERTIE` 字段。

 `TPF_NAME`\
 初始化/使用 `bstrName` S 结构的 `THREADPROPERTIE` 字段。

 `TPF_LOCATION`\
 初始化/使用 `bstrLocation` S 结构的 `THREADPROPERTIE` 字段。

 `TPF_ALLFIELDS`\
 指定所有字段。

## <a name="remarks"></a>备注
 这些值作为参数传递给 [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md) 方法，以指示要初始化 [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md) 结构的哪些字段。

 这些值还用于 `dwFields` 结构的成员 `THREADPROPERTIES` ，以指示哪些字段已使用且有效。

 这些标志可以与位 合并 `OR` 。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
