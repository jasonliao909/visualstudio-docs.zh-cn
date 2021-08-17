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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 65fa413d5538d0290afc85cea8d42f389098e5082cf064a57d09a51cc2c3b43e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121416321"
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

## <a name="see-also"></a>请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
