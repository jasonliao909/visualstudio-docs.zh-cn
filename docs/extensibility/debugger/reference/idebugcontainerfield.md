---
description: 此接口表示一个符号或类型，该符号或类型是其他符号或类型的容器。
title: IDebugContainerField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugContainerField
helpviewer_keywords:
- IDebugContainerField interface
ms.assetid: a8bbe061-c382-4fe9-a193-3f7d12216041
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 1a6f915bf6047e6517768ec498eeb15044abe945
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122127397"
---
# <a name="idebugcontainerfield"></a>IDebugContainerField
此接口表示一个符号或类型，该符号或类型是其他符号或类型的容器。

## <a name="syntax"></a>语法

```
IDebugContainerField : IDebugField
```

## <a name="notes-for-implementers"></a>实现者说明
 符号提供程序在实现 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口的同一对象上实现此接口。 此接口也是表示容器的所有接口的基类。

## <a name="notes-for-callers"></a>调用方说明
 许多接口上的许多方法都返回此接口。 由于这是所有容器的基类，因此可以使用 [QueryInterface](/cpp/atl/queryinterface)从此接口获取更专用的接口。 此类接口包括 IDebugArrayField、IDebugClassField、IDebugMethodField 和[IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md)。 [](../../../extensibility/debugger/reference/idebugarrayfield.md) [](../../../extensibility/debugger/reference/idebugclassfield.md) [](../../../extensibility/debugger/reference/idebugmethodfield.md)

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口上的方法外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[EnumFields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md)|为容器的字段创建枚举器。|

## <a name="remarks"></a>备注
 数组 (变量的) 、方法和变量的 (容器) 以及用于参数和局部变量) 的方法 (容器都是容器的示例。

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
