---
description: 此接口表示实现 IDebugObject 接口的对象的集合。
title: IEnumDebugObjects |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugObjects
helpviewer_keywords:
- IEnumDebugObjects interface
ms.assetid: 0950364c-6c8a-4b6c-ba37-c6aa359fa72c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 5521d5f6c825fd0ae5be96500d2e57af98746dba
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103333"
---
# <a name="ienumdebugobjects"></a>IEnumDebugObjects
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示实现 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 接口的对象的集合。

## <a name="syntax"></a>语法

```
IEnumDebugObjects : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 表达式计算程序实现此接口以提供实现 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 接口的对象集。 请注意，由于存在 [GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md) 方法，因此这不是标准 COM 枚举。

## <a name="notes-for-callers"></a>调用方说明
- [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md) 返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 此接口实现以下方法。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugobjects-next.md)|从 枚举中检索下一组 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugobjects-skip.md)|跳过指定数量的条目。|
|[重置](../../../extensibility/debugger/reference/ienumdebugobjects-reset.md)|将枚举重置为第一个条目。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugobjects-clone.md)|检索当前枚举的副本。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md)|检索 枚举中的条目数。|

## <a name="remarks"></a>备注
 此接口允许调试引擎枚举数组中的一组对象。

## <a name="requirements"></a>要求
 标头：ee.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)
