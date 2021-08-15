---
description: 此方法获取字段的类型。
title: IDebugField：： GetType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetType
helpviewer_keywords:
- IDebugField::GetType method
ms.assetid: b3cdec9f-ef7b-44d0-a775-d17ef7eae968
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 68bfc7654824285e6fe99d51e17dbf9f73e67c914786b3a03459cb9506b0b207
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417244"
---
# <a name="idebugfieldgettype"></a>IDebugField::GetType
此方法获取字段的类型。

## <a name="syntax"></a>语法

```cpp
HRESULT GetType( 
   IDebugField** ppType
);
```

```csharp
int GetType(
   out IDebugField ppType
);
```

## <a name="parameters"></a>参数
`ppType`\
弄返回作为另一个 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象的字段类型。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
