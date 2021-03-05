---
description: 获取正在调试此进程的会话的名称。
title: IDebugProcess2：： GetAttachedSessionName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetAttachedSessionName
helpviewer_keywords:
- IDebugProcess2::GetAttachedSessionName
ms.assetid: 7e5e116f-2c0c-4bc8-ad3f-e9fd2318a7e4
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 63d83a9d5f89ea06744454b790d988f1881c193b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102142539"
---
# <a name="idebugprocess2getattachedsessionname"></a>IDebugProcess2::GetAttachedSessionName
获取正在调试此进程的会话的名称。 IDE 可以向正在特定计算机上调试特定进程的用户显示此信息。

> [!NOTE]
> 此方法已弃用，其实现应总是返回 `E_NOTIMPL` 。

## <a name="syntax"></a>语法

```
HRESULT GetAttachedSessionName(
   BSTR* pbstrSessionName
);
```

## <a name="parameters"></a>参数
`pbstrSessionName`\

## <a name="return-value"></a>返回值
 此方法应总是返回 `E_NOTIMPL` 。

## <a name="see-also"></a>另请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
