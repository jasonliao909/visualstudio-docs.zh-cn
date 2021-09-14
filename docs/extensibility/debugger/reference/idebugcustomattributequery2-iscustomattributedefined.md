---
description: 确定自定义属性是否按名称存在。
title: IDebugCustomAttributeQuery2：：IsCustomAttributeDefined |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::IsCustomAttributeDefined
helpviewer_keywords:
- IDebugCustomAttributeQuery2::IsCustomAttributeDefined
ms.assetid: 5c07cc52-6d2d-42df-9d76-9f1f769641db
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d4e3fe35577c37d70413b0b4ad8a3bd17d76451c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600901"
---
# <a name="idebugcustomattributequery2iscustomattributedefined"></a>IDebugCustomAttributeQuery2::IsCustomAttributeDefined
确定自定义属性是否按名称存在。

## <a name="syntax"></a>语法

```cpp
HRESULT IsCustomAttributeDefined( 
   LPCOLESTR pszCustomAttributeName
);
```

```csharp
int IsCustomAttributeDefined(
   [In] string pszCustomAttributeName
);
```

## <a name="parameters"></a>parameters
`pszCustomAttributeName`\
[in]一个字符串，其中包含要查找的自定义属性的名称。

## <a name="return-value"></a>返回值
 如果S_OK定义了自定义属性，则返回属性，否则返回S_FALSE。

## <a name="remarks"></a>备注
 若要获取与自定义属性关联的属性字节，请调用 [GetCustomAttributeByName](../../../extensibility/debugger/reference/idebugcustomattributequery2-getcustomattributebyname.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
