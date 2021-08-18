---
description: 返回允许构造可读错误消息的信息。
title: IDebugErrorEvent2：：GetErrorMessage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorEvent2::GetErrorMessage
helpviewer_keywords:
- IDebugErrorEvent2::GetErrorMessage
ms.assetid: 9e3b0d74-a2dd-4eaa-bd95-21b2f9c79409
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2cf7b18d84ae8279c5d15f9404a6d8d500d44d82
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122118900"
---
# <a name="idebugerrorevent2geterrormessage"></a>IDebugErrorEvent2::GetErrorMessage
返回允许构造可读错误消息的信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetErrorMessage(
   MESSAGETYPE* pMessageType,
   BSTR*        pbstrErrorFormat,
   HRESULT*     hrErrorReason,
   DWORD*       pdwType,
   BSTR*        pbstrHelpFileName,
   DWORD*       pdwHelpId
);
```

```csharp
int GetErrorMessage(
   out enum_MESSAGETYPE   pMessageType,
   out string             pbstrErrorFormat,
   out int                phrErrorReason,
   out uint               pdwType,
   out string             pbstrHelpFileName,
   out uint               pdwHelpId
);
```

## <a name="parameters"></a>参数
`pMessageType`\
[out]从 [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md) 枚举返回一个值，该值描述消息的类型。

`pbstrErrorFormat`\
[out]要详细了解详细信息，请参阅 ("备注"，了解向用户发送的最终) 。

`hrErrorReason`\
[out]消息所关于的错误代码。

`pdwType`\
[out]错误的严重性 (使用 MB_XXX `MessageBox` 常量;例如 `MB_EXCLAMATION` 或 `MB_WARNING`) 。

`pbstrHelpFileName`\
[out]如果没有帮助文件， (将帮助文件的路径设置为 null) 。

`pdwHelpId`\
[out]如果没有帮助主题，则显示帮助 (ID 设置为 0) 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 错误消息应采用 行的格式 `"What I was doing.  %1"` 。 然后，调用方将替换为从错误代码派生的错误消息， (`"%1"` 中返回 `hrErrorReason`) 。 `pMessageType`参数告知调用方最终错误消息的显示方式。

## <a name="see-also"></a>请参阅
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
- [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)
