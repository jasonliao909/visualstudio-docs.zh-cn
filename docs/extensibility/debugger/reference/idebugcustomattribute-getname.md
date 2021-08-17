---
description: 获取自定义属性的名称。
title: IDebugCustomAttribute：：GetName |Microsoft Docs
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122089348"
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

## <a name="parameters"></a>参数
`bstrName`\
[out]返回一个包含自定义属性名称的字符串。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的命名 对应于用于声明属性的类的名称。 这可能不完全对应于自定义属性类本身的名称，因为 C# 允许在声明中使用"Attribute"后缀时从自定义属性名称删除它。

## <a name="see-also"></a>请参阅
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
