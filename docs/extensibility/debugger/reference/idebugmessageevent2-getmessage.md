---
description: 获取要显示的消息。
title: IDebugMessageEvent2：： GetMessage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMessageEvent2::GetMessage
helpviewer_keywords:
- GetMessage method
- IDebugMessageEvent2::GetMessage method
ms.assetid: 9fca7285-f7f1-422d-8565-92bf0e0db60a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d1427478154f73b3031f733deda5b07281db2833
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153337"
---
# <a name="idebugmessageevent2getmessage"></a>IDebugMessageEvent2::GetMessage
获取要显示的消息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMessage( 
   MESSAGETYPE* pMessageType,
   BSTR*        pbstrMessage,
   DWORD*       pdwType,
   BSTR*        pbstrHelpFileName,
   DWORD*       pdwHelpId
);
```

```csharp
int GetMessage( 
   out enum_MESSAGETYPE pMessageType,
   out string           pbstrMessage,
   out uint             pdwType,
   out string           pbstrHelpFileName,
   out uint             dwHelpId
);
```

## <a name="parameters"></a>参数
`pMessageType`\
弄从用于描述消息类型的 [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md) 枚举返回一个值。

`pbstrMessage`\
弄返回消息。

`pdwType`\
弄使用 Win32 函数的约定返回消息类型 `MessageBox` 。 有关详细信息，请参阅 [AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox) 函数。

`pbstrHelpFileName`\
[in，out]返回帮助文件名。 如果没有帮助文件，则可以为 null (c + +) 或空 (c # ) 值。

`pdwHelpId`\
[in，out]返回帮助标识符。 如果没有与此消息关联的帮助，则可以为0。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)
- [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)
- [AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox)
