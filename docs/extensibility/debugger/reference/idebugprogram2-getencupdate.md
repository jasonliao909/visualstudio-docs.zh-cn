---
description: 此方法获取此程序的 "编辑并继续" (ENC) update。
title: IDebugProgram2：： GetENCUpdate |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetENCUpdate
helpviewer_keywords:
- IDebugProgram2::GetENCUpdate
ms.assetid: 9832aac8-6320-4fd8-91dd-2a0852febb00
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 02446dba5450b89b769e773563f77cd6d8c1659f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102159895"
---
# <a name="idebugprogram2getencupdate"></a>IDebugProgram2::GetENCUpdate
此方法获取此程序的 "编辑并继续" (ENC) update。 自定义调试引擎总是返回 `E_NOTIMPL` 。

## <a name="syntax"></a>语法

```cpp
HRESULT GetENCUpdate( 
   IUnknown** ppUpdate
);
```

```csharp
int GetENCUpdate(
   out object ppUpdate
);
```

## <a name="parameters"></a>参数
`ppUpdate`\
弄返回一个可用于更新此程序的内部接口。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

> [!NOTE]
> 自定义调试引擎应总是返回 `E_NOTIMPL` 。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
