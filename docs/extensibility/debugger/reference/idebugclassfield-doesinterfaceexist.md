---
description: 确定是否在类中定义了特定接口。
title: IDebugClassField：:D oesInterfaceExist |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::DoesInterfaceExist
helpviewer_keywords:
- IDebugClassField::DoesInterfaceExist method
ms.assetid: cc0c8642-1a76-4fda-a309-7018a34883c9
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4248b653f5eea43a91d0c78a593431d53f5e68b8
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102173463"
---
# <a name="idebugclassfielddoesinterfaceexist"></a>IDebugClassField::DoesInterfaceExist
确定是否在类中定义了特定接口。

## <a name="syntax"></a>语法

```cpp
HRESULT DoesInterfaceExist( 
   LPCOLESTR pszInterfaceName
);
```

```csharp
int DoesInterfaceExist(
   [In] string pszInterfaceName
);
```

## <a name="parameters"></a>参数
`pszInterfaceName`\
中一个包含要查找的接口名称的字符串。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK，如果接口不存在，则返回 S_FALSE;否则，将返回错误代码。

## <a name="remarks"></a>备注
 此方法有效地获取所有接口的枚举，并在列表中搜索匹配的接口。

## <a name="see-also"></a>另请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
