---
description: 此方法获取字段的大小（以字节为单位）。
title: IDebugField：：GetSize |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetSize
helpviewer_keywords:
- IDebugField::GetSize method
ms.assetid: 73329924-3751-4f44-af54-5986b7943374
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 705d597993c0d29ba66a9165c17c65c4ca475cc157c29252bafa27383f430798
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121360321"
---
# <a name="idebugfieldgetsize"></a>IDebugField::GetSize
此方法获取字段的大小（以字节为单位）。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSize( 
   DWORD* pdwSize
);
```

```csharp
int GetSize(
   out uint pdwSize
);
```

## <a name="parameters"></a>参数
`pdwSize`\
[out]返回大小。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 所有字段都有一个类型，并且所有类型都有一个大小。 例如，一个字节类型的字段的大小为 1 个字节。

## <a name="see-also"></a>请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
