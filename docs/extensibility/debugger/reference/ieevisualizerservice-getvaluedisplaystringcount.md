---
description: 检索要为指定的属性或字段显示的值字符串的数目。
title: IEEVisualizerService：： GetValueDisplayStringCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IEEVisualizerService::GetValueDisplayStringCount
- GetValueDisplayStringCount
ms.assetid: d683a833-fbfb-4042-84df-6905124a268a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: aaabad975a57e18c9257df178b29b594d892441482db30fcd00836c322fb0169
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121389418"
---
# <a name="ieevisualizerservicegetvaluedisplaystringcount"></a>IEEVisualizerService::GetValueDisplayStringCount
检索要为指定的属性或字段显示的值字符串的数目。

## <a name="syntax"></a>语法

```cpp
HRESULT GetValueDisplayStringCount (
   DWORD         displayKind,
   IDebugField * propertyOrField,
   ULONG *       pcelt
);
```

```csharp
int GetValueDisplayStringCount (
   uint        displayKind,
   IDebugField propertyOrField,
   out ulong   pcelt
);
```

## <a name="parameters"></a>参数
`displayKind`\
中 [DisplayKind](../../../extensibility/debugger/reference/displaykind.md) 枚举中的值。

`propertyOrField`\
中表示属性或字段的 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口。

`pcelt`\
弄返回要显示的值字符串的数目。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
