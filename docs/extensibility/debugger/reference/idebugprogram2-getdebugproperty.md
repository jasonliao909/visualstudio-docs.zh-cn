---
title: IDebugProgram2：： GetDebugProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetDebugProperty
helpviewer_keywords:
- IDebugProgram2::GetDebugProperty
ms.assetid: d194224e-f0e6-46ab-85d4-9e2639e28946
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: eb0bb520d3a821d777d5deaeaa200c4b7e526f65
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99911953"
---
# <a name="idebugprogram2getdebugproperty"></a>IDebugProgram2::GetDebugProperty
获取程序的属性。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDebugProperty( 
   IDebugProperty2** ppProperty
);
```

```csharp
int GetDebugProperty( 
   out IDebugProperty2 ppProperty
);
```

## <a name="parameters"></a>parameters
`ppProperty`\
弄返回一个 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 对象，该对象表示程序的属性。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的属性特定于程序。 如果程序需要返回多个属性，则此方法返回的 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 对象是附加属性的容器，并且调用 [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) 方法将返回所有属性的列表。

 程序可能会公开任何数量和类型的其他属性，这些属性可通过接口进行描述 `IDebugProperty2` 。 IDE 可以通过通用属性浏览器用户界面显示其他程序属性。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
