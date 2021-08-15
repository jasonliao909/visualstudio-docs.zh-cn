---
description: 尝试确定自动附加失败的原因。
title: IDebugCoreServer3：:D iagnoseWebDebuggingError |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::DiagnoseWebDebuggingError
helpviewer_keywords:
- IDebugCoreServer3::DiagnoseWebDebuggingError
ms.assetid: 8c4570ca-ae55-42f2-bbaa-8d8e75d2fa19
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2ec4af56afce3568577279fb1cefc09da0be22c974eb9acf1dd7d364e7c272d1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417517"
---
# <a name="idebugcoreserver3diagnosewebdebuggingerror"></a>IDebugCoreServer3::DiagnoseWebDebuggingError
尝试确定自动附加失败的原因。

## <a name="syntax"></a>语法

```cpp
HRESULT DiagnoseWebDebuggingError(
   LPCWSTR pszUrl
);
```

```csharp
int DiagnoseWebDebuggingError(
   string pszUrl
);
```

## <a name="parameters"></a>参数
`pszUrl`\
中当前未使用;应始终设置为 null 值。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 下面是其他典型的返回代码：

|代码|说明|
|----------|-----------------|
|`S_WEBDBG_UNABLE_TO_DIAGNOSE`|无法确定远程服务器启动调试失败的原因。|
|`S_WEBDBG_DEBUG_VERB_BLOCKED`|无法在远程服务器上进行调试，可能是由于权限不足或没有启用调试谓词。|
|`E_WEBDBG_DEBUG_VERB_BLOCKED`|Web 服务器已被锁定，并阻止调试谓词，这是启用调试所必需的。|

## <a name="see-also"></a>另请参阅
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
