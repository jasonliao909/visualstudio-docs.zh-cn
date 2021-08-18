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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9d124a1cd00f999c41bfc5259183658aada84696
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122132751"
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

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
