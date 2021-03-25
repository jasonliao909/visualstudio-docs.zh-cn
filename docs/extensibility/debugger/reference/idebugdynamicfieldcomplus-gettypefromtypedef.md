---
description: 如果给定标记，IDebugDynamicFieldCOMPlus：： GetTypeFromTypeDef 会检索该类型。
title: IDebugDynamicFieldCOMPlus：： GetTypeFromTypeDef |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetTypeFromTypeDef
- IDebugDynamicFieldCOMPlus::GetTypeFromTypeDef
ms.assetid: 7f6cd3d3-f4da-4893-be91-8dd104be8010
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4cc8e9167085895ce4f0f10784b07aa418afd3fa
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105093998"
---
# <a name="idebugdynamicfieldcomplusgettypefromtypedef"></a>IDebugDynamicFieldCOMPlus::GetTypeFromTypeDef
在给定其标记的情况中检索类型。

## <a name="syntax"></a>语法

```cpp
HRESULT GetTypeFromTypeDef(
   ULONG32       ulAppDomainID,
   GUID          guidModule,
   _mdToken      tokClass,
   IDebugField** ppType
);
```

```csharp
int GetTypeFromTypeDef(
   uint            ulAppDomainID,
   Guid            guidModule,
   int             tokClass,
   out IDebugField ppType
);
```

## <a name="parameters"></a>参数
`ulAppDomainID`\
中应用程序域的标识符。

`guidModule`\
中模块的唯一标识符。

`tokClass`\
中表示类型的标记。

`ppType`\
弄返回一个包含类型的 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugDynamicFieldCOMPlus](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus.md)
