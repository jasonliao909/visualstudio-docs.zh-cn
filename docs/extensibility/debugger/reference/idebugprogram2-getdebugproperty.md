---
description: 获取程序的属性。
title: IDebugProgram2：：GetDebugProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetDebugProperty
helpviewer_keywords:
- IDebugProgram2::GetDebugProperty
ms.assetid: d194224e-f0e6-46ab-85d4-9e2639e28946
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: adac39c45a001a45d57b7e2cc5ac816ba4d6dd87
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122087842"
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

## <a name="parameters"></a>参数
`ppProperty`\
[out]返回表示 [程序属性的 IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的属性特定于程序。 如果程序需要返回多个属性，则此方法返回的 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 对象是附加属性的容器，调用 [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) 方法将返回所有属性的列表。

 程序可能会公开任何数量和类型的其他属性，可通过 接口 `IDebugProperty2` 描述这些属性。 IDE 可以通过泛型属性浏览器用户界面显示其他程序属性。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
