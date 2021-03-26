---
description: 检索应用程序域的标识符。
title: IDebugAlias2：： GetAppDomainId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetAppDomainId
- IDebugAlias2::GetAppDomainId
ms.assetid: 23581aaa-5a53-4859-b264-eca49fc44bcd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ee1caec6968f9a67a15a31c8064b7795a37a6829
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059101"
---
# <a name="idebugalias2getappdomainid"></a>IDebugAlias2::GetAppDomainId
检索应用程序域的标识符。

## <a name="syntax"></a>语法

```cpp
HRESULT GetAppDomainId (
   ULONG32* pappDomainId
);
```

```csharp
int GetAppDomainId (
   out uint pappDomainId
);
```

## <a name="parameters"></a>参数
`pappDomainId`\
弄返回应用程序域标识符。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 每当重新启动应用程序并创建新的应用程序域时，应用程序域标识符都会发生更改。

## <a name="see-also"></a>另请参阅
- [IDebugAlias2](../../../extensibility/debugger/reference/idebugalias2.md)
