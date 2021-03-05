---
description: 检索应用程序域的标识符。
title: IDebugAlias2：： GetAppDomainId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetAppDomainId
- IDebugAlias2::GetAppDomainId
ms.assetid: 23581aaa-5a53-4859-b264-eca49fc44bcd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6f5bd0d6a96ad41409b87433599fe693fc86c1cc
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143865"
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
