---
description: 将枚举重置为第一个 DEBUG_PROPERTY_INFO 元素。
title: IEnumDebugPropertyInfo2：：Reset |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPropertyInfo2::Reset
helpviewer_keywords:
- IEnumDebugPropertyInfo2::Reset
ms.assetid: fa4201c1-4633-4596-93aa-bd415c4ed71a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fda4458dac1f315edf3963a30595fd81293779b9ded24444dbdb10085e8f8e95
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121306538"
---
# <a name="ienumdebugpropertyinfo2reset"></a>IEnumDebugPropertyInfo2::Reset
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
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后，对 [Next](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md) 方法的下一次调用将返回 枚举的第一个元素。

## <a name="see-also"></a>另请参阅
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
