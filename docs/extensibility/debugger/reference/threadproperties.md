---
description: 描述线程的属性。
title: THREADPROPERTIES |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTIES
helpviewer_keywords:
- THREADPROPERTIES structure
ms.assetid: 7d397207-db03-4ec0-9f79-3794056ed89f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 18da5073284255da66afcc8ae0ebe65eec9f52892bab726585d8c993f58a1bac
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414988"
---
# <a name="threadproperties"></a>THREADPROPERTIES
描述线程的属性。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagTHREADPROPERTIES { 
   THREADPROPERTY_FIELDS dwFields;
   DWORD                 dwThreadId;
   DWORD                 dwSuspendCount;
   DWORD                 dwThreadState;
   BSTR                  bstrPriority;
   BSTR                  bstrName;
   BSTR                  bstrLocation;
} THREADPROPERTIES;
```

```csharp
public struct THREADPROPERTIES { 
   public uint   dwFields;
   public uint   dwThreadId;
   public uint   dwSuspendCount;
   public uint   dwThreadState;
   public string bstrPriority;
   public string bstrName;
   public string bstrLocation;
};
```

## <a name="members"></a>成员
 `dwFields`\
 来自 THREADPROPERTY_FIELDS [标志的组合](../../../extensibility/debugger/reference/threadproperty-fields.md) ，描述此结构中哪些字段有效。

 `dwThreadId`\
 线程 ID。

 `dwSuspendCount`\
 线程挂起计数。

 `dwThreadState`\
 THREADSTATE [枚举](../../../extensibility/debugger/reference/threadstate.md) 中的一个值，指示操作线程的状态。

 `bstrPriority`\
 指定线程优先级的字符串;例如，"高于正常"、"正常"或"时间关键"。

 `bstName`\
 线程名称。

 `bstrLocation`\
 线程位置 (堆栈帧) ，通常表示为当前暂停执行的方法的名称。

## <a name="remarks"></a>备注
 通过调用 [GetThreadProperties 方法填充此](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md) 结构。 因此返回的信息通常用于填充"线程 **"** 窗口。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
- [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)
- [THREADSTATE](../../../extensibility/debugger/reference/threadstate.md)
