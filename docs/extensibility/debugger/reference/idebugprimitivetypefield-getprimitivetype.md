---
description: 检索与此字段关联的基元类型。
title: IDebugPrimitiveTypeField：：GetPrimitiveType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetPrimitiveType
- IDebugPrimitiveTypeField::GetPrimitiveType
ms.assetid: a186c922-bbfe-478c-a744-b21eb4672d8f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d5256165db724dbfc06399aa4bedeb6c59df249d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122050791"
---
# <a name="idebugprimitivetypefieldgetprimitivetype"></a>IDebugPrimitiveTypeField::GetPrimitiveType
检索与此字段关联的基元类型。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPrimitiveType (
   DWORD* pdwType
);
```

```csharp
int GetPrimitiveType (
   out uint pdwType
);
```

## <a name="parameters"></a>参数
`pdwType`\
[out]表示基 [元类型的 CorElementType](/dotnet/framework/unmanaged-api/metadata/corelementtype-enumeration) 枚举中的值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回 `S_FALSE` 。

## <a name="see-also"></a>请参阅
- [IDebugPrimitiveTypeField](../../../extensibility/debugger/reference/idebugprimitivetypefield.md)
