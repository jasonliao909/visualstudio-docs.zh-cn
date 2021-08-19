---
description: 根据自定义特性的名称获取自定义属性字节。
title: IDebugCustomAttributeQuery2：：GetCustomAttributeByName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
helpviewer_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
ms.assetid: 7428dfeb-8929-41b2-9b99-cb343a86c02d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e20f4cba0d826a7a9b608f1fc56fde1a35ae54c0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122079410"
---
# <a name="idebugcustomattributequery2getcustomattributebyname"></a>IDebugCustomAttributeQuery2::GetCustomAttributeByName
根据自定义特性的名称获取自定义属性字节。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCustomAttributeByName( 
   LPCOLESTR pszCustomAttributeName,
   BYTE*     ppBlob,
   DWORD*    pdwLen
);
```

```csharp
int GetCustomAttributeByName(
   [In] string        pszCustomAttributeName,
   [In, Out] byte[]   ppBlob,
   [In, Out] ref uint pdwLen
);
```

## <a name="parameters"></a>参数
`pszCustomAttributeName`\
[in]包含要查找的自定义属性的名称的字符串。

`ppBlob`\
[in， out]用自定义属性字节填充的数组。

`pdwLen`\
[in， out]指定在数组中返回的最大字节数，并 `ppBlob` 返回实际写入数组的字节数。

## <a name="return-value"></a>返回值
 如果成功，则S_OK，或者S_FALSE自定义属性不存在时返回 。 否则，返回错误代码。

## <a name="remarks"></a>备注
 将 `ppBlob` 参数设置为 null 值，以返回可用的属性字节数。 然后分配一个数组，然后为 参数传递该 `ppBlob` 数组。

 属性字节表示自定义属性的原始数据。

 如果 和 参数设置为 null 值，则此方法可用于 `ppBlob` `pdwLen` 确定自定义属性是否仅存在。 但是，一种更简单的替代方法是调用 [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md) 方法。

## <a name="see-also"></a>请参阅
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)
