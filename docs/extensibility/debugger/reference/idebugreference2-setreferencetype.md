---
description: 设置引用类型。
title: IDebugReference2：： SetReferenceType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::SetReferenceType
helpviewer_keywords:
- IDebugReference2::SetReferenceType
ms.assetid: 5854a172-ea82-481c-97d9-c7fc16923d44
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 94aacf23397c2599acd44b8197d2d2af0f157ea1d61ba13becedb44ad03d002d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338535"
---
# <a name="idebugreference2setreferencetype"></a>IDebugReference2::SetReferenceType
设置引用类型。 保留供将来使用。

## <a name="syntax"></a>语法

```cpp
HRESULT SetReferenceType ( 
   REFERENCE_TYPE dwRefType
);
```

```csharp
int SetReferenceType ( 
   enum_REFERENCE_TYPE dwRefType
);
```

## <a name="parameters"></a>参数
`dwRefType`\
中 [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md) 枚举中的一个值，该值指定引用类型。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL`。

## <a name="see-also"></a>另请参阅
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md)
