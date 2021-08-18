---
description: 此方法获取有关符号或类型的与类型无关的信息。
title: IDebugField：： GetTypeInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetTypeInfo
helpviewer_keywords:
- IDebugField::GetTypeInfo method
ms.assetid: bb5acfa3-04c3-4088-be84-9ff8926cd16f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e30cfd7b27cda63e935066f29972d0c2d966db27f0f2b74f62b5a36c472cd604
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433874"
---
# <a name="idebugfieldgettypeinfo"></a>IDebugField::GetTypeInfo
此方法获取有关符号或类型的与类型无关的信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetTypeInfo( 
   TYPE_INFO* pTypeInfo
);
```

```csharp
int GetTypeInfo(
   TYPE_INFO[] pTypeInfo
);
```

## <a name="parameters"></a>参数
`pTypeInfo`\
弄返回所提供的 [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) 结构中的类型信息。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 与类型无关的信息将包括 AppDomain、模块以及包含符号的类。

## <a name="see-also"></a>请参阅
- [GetType](../../../extensibility/debugger/reference/idebugfield-gettype.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
