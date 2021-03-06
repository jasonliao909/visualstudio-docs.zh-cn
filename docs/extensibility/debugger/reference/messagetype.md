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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dd7b10217313be30dd795a8ff108c3c30e214490
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102222427"
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
 指示应将消息发送到 "输出" 窗口。 这与互斥 `MT_MESSAGEBOX` 。

 `MT_MESSAGEBOX`\
 指示消息应显示在消息框中。 这与互斥 `MT_OUTPUTSTRING` 。

 `MT_TYPE_MASK`\
 用于隔离消息目标的掩码值。

 `MT_REASON_EXCEPTION`\
 指示由于异常而显示的消息框。 这与互斥 `MT_REASON_TRACEPOINT` 。

 `MT_REASON_TRACEPOINT`\
 指示由于命中跟踪点而显示的消息框。 这与互斥 `MT_REASON_EXCEPTION` 。

 `MT_REASON_MASK`\
 用于隔离正在显示的消息原因的掩码值。

## <a name="remarks"></a>备注
 这些值从 [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md) 和 [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md) 方法返回。

 其中一个原因值可以使用按位与某个输出目标值相结合 `OR` 。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)
- [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md)
