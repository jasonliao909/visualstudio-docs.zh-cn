---
description: 获取跨进程边界的指定接口。
title: IDebugProviderProgramNode2：：UnmarshalDebuggeeInterface |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
helpviewer_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
ms.assetid: 2e4653c5-10f1-493c-9973-f31d266c5d48
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 585f05969f0bf987abd6db67fae826ba00e916a6eb279989042087a499b757b5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121402371"
---
# <a name="idebugproviderprogramnode2unmarshaldebuggeeinterface"></a>IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
获取跨进程边界的指定接口。

## <a name="syntax"></a>语法

```cpp
HRESULT UnmarshalDebuggeeInterface(
   REFIID riid,
   void** ppvObject
);
```

```csharp
int UnmarshalDebuggeeInterface(
   ref Guid   riid,
   out IntPtr ppvObject
);
```

## <a name="parameters"></a>参数
`riid`\
[in]要获取的接口的 GUID。

`ppvObject`\
[out]返回实现所需接口的对象。 [C++] 这可以直接强制转换到所需的接口类型。 [C#] <xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A> 使用 方法获取所需的接口。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 当调试引擎在进程空间中运行并且正在调试的程序在其自己的进程空间中运行时， [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 使用此方法。

## <a name="see-also"></a>请参阅
- [IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)
