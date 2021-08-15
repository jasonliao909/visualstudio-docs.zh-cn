---
description: 获取枚举器中的自定义属性的数目。
title: IEnumDebugCustomAttributes：： GetCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCustomAttributes::GetCount
helpviewer_keywords:
- IEnumDebugCustomAttributes::GetCount
ms.assetid: fafe826f-4ebf-4572-b2a3-d5dd2916c12f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e2db37f558aaa39444deef994a885fc424cede528588e376d1382231a7d3a13f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121415437"
---
# <a name="ienumdebugcustomattributesgetcount"></a>IEnumDebugCustomAttributes::GetCount
获取枚举器中的自定义属性的数目。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCount( 
   ULONG* pcelt
);
```

```csharp
int GetCount(
   out uint pcelt
);
```

## <a name="parameters"></a>参数
`pcelt`\
弄返回枚举中的元素数。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法不是习惯的 COM 枚举接口的一部分，它指定只 `Next` `Clone` `Skip` 需实现、、和 `Reset` 。

## <a name="see-also"></a>另请参阅
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
