---
description: 检索应用程序域的标识符。
title: IDebugAlias2：：GetAppDomainId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetAppDomainId
- IDebugAlias2::GetAppDomainId
ms.assetid: 23581aaa-5a53-4859-b264-eca49fc44bcd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 20be3f4abaa53dd6d65770142935003db7b211ab
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600961"
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

## <a name="parameters"></a>parameters
`pappDomainId`\
[out]返回应用程序域标识符。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 每当重启应用程序并创建一个新的应用程序域时，应用程序域标识符都会更改。

## <a name="see-also"></a>另请参阅
- [IDebugAlias2](../../../extensibility/debugger/reference/idebugalias2.md)
