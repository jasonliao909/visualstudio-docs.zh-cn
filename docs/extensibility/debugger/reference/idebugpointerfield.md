---
description: 此接口表示指针类型。
title: IDebugPointerField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerField
helpviewer_keywords:
- IDebugPointerField interface
ms.assetid: d51bd5b2-f18e-4e27-b4fb-e6f652fbf635
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: eba0654d97d37633ca1b2afce45b83de1a96bc1b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122133076"
---
# <a name="idebugpointerfield"></a>IDebugPointerField
此接口表示指针类型。

## <a name="syntax"></a>语法

```
IDebugPointerField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实现者说明
 符号提供程序实现此接口以表示指针。

## <a name="notes-for-callers"></a>调用方说明
 如果 GetKind 返回 ，则使用 [QueryInterface](/cpp/atl/queryinterface) 从 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口 [获取此](../../../extensibility/debugger/reference/idebugfield-getkind.md) 接口 `FIELD_TYPE_POINTER` 。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 除了 和 接口上 `IDebugField` `IDebugContainerField` 的方法外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetDereferencedField](../../../extensibility/debugger/reference/idebugpointerfield-getdereferencedfield.md)|返回[描述指针目标的 IDebugField。](../../../extensibility/debugger/reference/idebugfield.md)|

## <a name="remarks"></a>备注
 在 C/C++ 中，如果指针与数组表示法一起使用，则指针可以是容器。 例如，在 `char *pString` 给定 `pString` 后， 具有指向 的指针类型 `char` 。 `pString[3]` 具有容器的类型，该容器是指向 `char` 引用该容器的第四个元素的指针。

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
