---
description: 此方法获取字段的容器。
title: IDebugField：：GetContainer |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetContainer
helpviewer_keywords:
- IDebugField::GetContainer method
ms.assetid: 6d6c8213-6181-4adf-9584-3e4cac163dd8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e87248314a97301fb49a8f4c4fef7db1a44f3e9d4eca7a84b58ea139ef12d188
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121389873"
---
# <a name="idebugfieldgetcontainer"></a>IDebugField::GetContainer
此方法获取字段的容器。

## <a name="syntax"></a>语法

```cpp
HRESULT GetContainer( 
   IDebugContainerField** ppContainerField
);
```

```csharp
int GetContainer(
   out IDebugContainerField ppContainerField
);
```

## <a name="parameters"></a>参数
`ppContainerField`\
[out]返回由 [IDebugContainerField 接口表示的](../../../extensibility/debugger/reference/idebugcontainerfield.md) 容器。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 如果此字段没有容器，则返回的 将为 `ppContainerField` null 值。

## <a name="see-also"></a>另请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
