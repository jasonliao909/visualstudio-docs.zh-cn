---
title: IDebugGenericParamField：： GetIndex |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugGenericParamField::GetIndex
ms.assetid: 8e0bdb26-1247-44d9-8d80-ec6e35187fb4
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c45f7c83c840566fb494c7944ccab9dbe37c3875
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99869695"
---
# <a name="idebuggenericparamfieldgetindex"></a>IDebugGenericParamField::GetIndex
检索此泛型参数的索引。

## <a name="syntax"></a>语法

```cpp
HRESULT GetIndex(
    DWORD* pIndex
);
```

```csharp
int GetIndex(
    out uint pIndex
);
```

## <a name="parameters"></a>parameters
`pIndex`\
弄此泛型参数的索引值。

## <a name="return-value"></a>返回值
如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
例如，对于字典 (K，V) ，K 为索引0，V 为索引1。

## <a name="example"></a>示例
下面的示例演示如何为公开 [IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)接口的 **CDebugGenericParamFieldType** 对象实现此方法。

```cpp
HRESULT CDebugGenericParamFieldType::GetIndex(DWORD* pIndex)
{
    HRESULT hr = S_OK;

    METHOD_ENTRY( CDebugGenericParamFieldType::GetIndex );

    IfFalseGo(pIndex, E_INVALIDARG );
    IfFailGo( this->LoadProps() );
    *pIndex = m_index;

Error:

    METHOD_EXIT( CDebugGenericParamFieldType::GetIndex, hr );
    return hr;
}
```

## <a name="see-also"></a>另请参阅
- [IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)
