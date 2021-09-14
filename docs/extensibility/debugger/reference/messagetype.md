---
description: 指定消息类型和原因。
title: MESSAGETYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MESSAGETYPE
helpviewer_keywords:
- MESSAGETYPE enumeration
ms.assetid: 800cc77d-3c27-4763-a9df-552a9384bd49
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3172188d878d40d3957ea56ff3c6f57ca561a1be
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602397"
---
# <a name="messagetype"></a>MESSAGETYPE
指定消息类型和原因。

## <a name="syntax"></a>语法

```cpp
enum enum_MESSAGETYPE { 
   MT_OUTPUTSTRING      = 0x0000001,
   MT_MESSAGEBOX        = 0x00000002,
   MT_TYPE_MASK         = 0x000000FF,
   MT_REASON_EXCEPTION  = 0x00000100,
   MT_REASON_TRACEPOINT = 0x00000200,
   MT_REASON_MASK       = 0x0000FF00
};
typedef DWORD MESSAGETYPE;
```

```csharp
public enum enum_MESSAGETYPE { 
   MT_OUTPUTSTRING      = 0x0000001,
   MT_MESSAGEBOX        = 0x00000002,
   MT_TYPE_MASK         = 0x000000FF,
   MT_REASON_EXCEPTION  = 0x00000100,
   MT_REASON_TRACEPOINT = 0x00000200,
   MT_REASON_MASK       = 0x0000FF00
};
```

## <a name="fields"></a>字段
 `MT_OUTPUTSTRING`\
 指示消息应发送到输出窗口。 这与 互斥 `MT_MESSAGEBOX` 。

 `MT_MESSAGEBOX`\
 指示消息应显示在消息框中。 这与 互斥 `MT_OUTPUTSTRING` 。

 `MT_TYPE_MASK`\
 一个掩码值，用于隔离消息的目标。

 `MT_REASON_EXCEPTION`\
 指示消息框显示为异常的结果。 这与 互斥 `MT_REASON_TRACEPOINT` 。

 `MT_REASON_TRACEPOINT`\
 指示消息框显示为命中跟踪点的结果。 这与 互斥 `MT_REASON_EXCEPTION` 。

 `MT_REASON_MASK`\
 一个掩码值，用于隔离显示消息的原因。

## <a name="remarks"></a>备注
 这些值从 [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md) 和 [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md) 方法返回。

 其中一个原因值可以使用位 与输出目标值之一结合使用 `OR` 。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)
- [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md)
