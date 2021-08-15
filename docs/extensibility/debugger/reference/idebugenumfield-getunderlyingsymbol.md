---
description: 此方法返回表示枚举名称的 IDebugField。
title: IDebugEnumField：：GetUnderlyingSymbol |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetUnderlyingSymbol
helpviewer_keywords:
- IDebugEnumField::GetUnderlyingSymbol method
ms.assetid: c3b8a117-6708-4cfd-8ffc-5f007d706bc5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 692f5cb3be55e76e1471836bbd422367d637d6b12b93ee5099fc5a70705821f7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342201"
---
# <a name="idebugenumfieldgetunderlyingsymbol"></a>IDebugEnumField::GetUnderlyingSymbol
此方法返回表示枚举名称的[IDebugField。](../../../extensibility/debugger/reference/idebugfield.md)

## <a name="syntax"></a>语法

```cpp
HRESULT GetUnderlyingSymbol(
   IDebugField** ppField
);
```

```csharp
int GetUnderlyingSymbol(
   out IDebugField ppField
);
```

## <a name="parameters"></a>参数
`ppField`\
[out]返回[描述此枚举的名称的 IDebugField。](../../../extensibility/debugger/reference/idebugfield.md)

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 枚举的名称还包含枚举的类型，该枚举通过使用 Bind 绑定到内存 [位置](../../../extensibility/debugger/reference/idebugbinder-bind.md)。

## <a name="see-also"></a>另请参阅
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)
