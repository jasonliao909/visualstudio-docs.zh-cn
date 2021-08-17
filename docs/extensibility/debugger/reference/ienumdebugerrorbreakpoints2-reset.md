---
description: 将错误断点枚举重置为第一个元素。
title: IEnumDebugErrorBreakpoints2：： Reset |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugErrorBreakpoints2::Reset
helpviewer_keywords:
- IEnumDebugErrorBreakpoints2::Reset
ms.assetid: d5b04bba-a8b9-4141-94fb-250c77f0534c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cad6ccd10f21466c8e1b5cd052f6b88333c2255c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122029445"
---
# <a name="ienumdebugerrorbreakpoints2reset"></a>IEnumDebugErrorBreakpoints2::Reset
将枚举重置为第一个元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Reset(
   void
);
```

```csharp
int Reset();
```

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后， [下一次调用的方法将](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-next.md) 返回枚举的第一个元素。

## <a name="see-also"></a>请参阅
- [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)
