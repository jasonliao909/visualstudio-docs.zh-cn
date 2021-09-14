---
description: 获取自定义属性的名称。
title: IDebugCustomAttribute：： GetName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetName
helpviewer_keywords:
- IDebugCustomAttribute::GetName
ms.assetid: ba509cc5-5816-4925-a094-4c72d88c360c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 53345ce6c7cc7a261b15367d926a68701a087ef3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664539"
---
# <a name="idebugcustomattributegetname"></a>IDebugCustomAttribute::GetName
获取自定义属性的名称。

## <a name="syntax"></a>语法

```cpp
HRESULT GetName( 
   BSTR* bstrName
);
```

```csharp
int GetName(
   out string bstrName
);
```

## <a name="parameters"></a>parameters
`bstrName`\
弄返回一个字符串，该字符串包含自定义特性的名称。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的命名对应于用于声明特性的类的名称。 这与自定义特性类本身的名称可能并不完全一致，因为 c # 允许在声明中使用自定义属性名称时将其从自定义属性名称中删除。

## <a name="see-also"></a>另请参阅
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
