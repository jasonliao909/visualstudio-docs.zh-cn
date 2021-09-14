---
description: 为此类实现的接口创建枚举器。
title: IDebugClassField：：EnumInterfacesImplemented |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumInterfacesImplemented
helpviewer_keywords:
- IDebugClassField::EnumInterfacesImplemented method
ms.assetid: e5523e45-d350-491e-a92c-fe0ca97d2052
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8395a35a2f0e5aa7481148562dc12b66da39e257
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600914"
---
# <a name="idebugclassfieldenuminterfacesimplemented"></a>IDebugClassField::EnumInterfacesImplemented
为此类实现的接口创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumInterfacesImplemented( 
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumInterfacesImplemented(
   out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>parameters
`ppEnum`\
[out]返回表示 [实现的接口列表的 IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象。 如果没有接口，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK，或者S_FALSE类上没有实现的接口时返回 。 否则，返回错误代码。

## <a name="remarks"></a>备注
 枚举的每个元素都是描述接口的 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) 对象。 请注意，非托管代码不使用接口作为离散实体，因此此方法始终返回非托管代码的 null [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] 值。

## <a name="see-also"></a>另请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
