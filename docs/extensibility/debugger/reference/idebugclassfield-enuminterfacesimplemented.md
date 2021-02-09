---
title: IDebugClassField：： EnumInterfacesImplemented |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumInterfacesImplemented
helpviewer_keywords:
- IDebugClassField::EnumInterfacesImplemented method
ms.assetid: e5523e45-d350-491e-a92c-fe0ca97d2052
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b7283d8a2996d5ab4dfc52cde446170e7632c27c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876077"
---
# <a name="idebugclassfieldenuminterfacesimplemented"></a>IDebugClassField::EnumInterfacesImplemented
为此类实现的接口创建一个枚举器。

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
弄返回一个 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象，该对象表示所实现的接口的列表。 如果没有接口，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK 或返回 S_FALSE （如果没有在此类上实现的接口）。 否则，返回错误代码。

## <a name="remarks"></a>备注
 枚举的每个元素都是描述接口的 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) 对象。 请注意，非托管 [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] 代码不使用接口作为离散实体，因此此方法始终为非托管代码返回 null 值 [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] 。

## <a name="see-also"></a>另请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
