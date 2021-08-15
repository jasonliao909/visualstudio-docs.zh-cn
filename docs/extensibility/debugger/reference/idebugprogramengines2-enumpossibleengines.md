---
description: 返回可调试此程序的 DE (的所有) 引擎的 GUID。
title: IDebugProgramEngines2：：EnumPossibleEngines |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEngines2::EnumPossibleEngines
helpviewer_keywords:
- IDebugProgramEngines2::EnumPossibleEngines
ms.assetid: 993d70a4-f6a5-4e47-a603-0b162b9fde00
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: db9b8fa5a58b48ce8b093c00c5a5605b912d77ba182daf6022e8b9ebb3bfa268
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121416035"
---
# <a name="idebugprogramengines2enumpossibleengines"></a>IDebugProgramEngines2::EnumPossibleEngines
返回可调试此程序的 DE (的所有) 引擎的 GUID。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumPossibleEngines( 
   DWORD  celtBuffer,
   GUID*  rgguidEngines,
   DWORD* pceltEngines
);
```

```csharp
int EnumPossibleEngines( 
   uint      celtBuffer,
   GUID[]    rgguidEngines,
   ref DWORD pceltEngines
);
```

## <a name="parameters"></a>参数
`celtBuffer`\
[in]要返回的 DE GUID 数。 这还指定数组的最大 `rgguidEngines` 大小。

`rgguidEngines`\
[in， out]要填充的 DE GUID 数组。

`pceltEngines`\
[out]返回返回的实际 DE GUID 数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 如果缓冲区不够 `HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)` 大，则0x8007007A [C++] 或 [C#] 值。

## <a name="remarks"></a>备注
 若要确定有多少个引擎，请调用此方法一次，将 参数 `celtBuffer` 设置为 0，将 参数 `rgguidEngines` 设置为 null 值。 这将 (0x8007007A `HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)` C#) ，参数 `pceltEngines` 返回缓冲区的必要大小。

## <a name="see-also"></a>另请参阅
- [IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)
