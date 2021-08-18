---
description: 此接口枚举DEBUG_REFERENCE_INFO结构。
title: IEnumDebugReferenceInfo2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugReferenceInfo2
helpviewer_keywords:
- IEnumDebugReferenceInfo2
ms.assetid: 7ed01441-686f-4032-8268-a4c750f19f85
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: e9b89ee48a0975a8b2e9c438267c17b5e94bd26b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122029250"
---
# <a name="ienumdebugreferenceinfo2"></a>IEnumDebugReferenceInfo2
此接口枚举 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 结构。

## <a name="syntax"></a>语法

```
IEnumDebugReferenceInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎 (DE) 实现此接口，作为对内存中对象的引用的支持的一部分。 只有在支持引用时，才能实现此接口。

## <a name="notes-for-callers"></a>调用方说明
 Visual Studio [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IEnumDebugReferenceInfo2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-next.md)|检索枚举序列 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 指定数目的对象结构。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-skip.md)|跳过枚举序列 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 指定数量的对象结构。|
|[重置](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-clone.md)|创建一个枚举器，其中包含与当前枚举器相同的枚举状态。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-getcount.md)|获取枚举 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 结构的数量。|

## <a name="remarks"></a>备注
 引用实质上是类型和地址，而属性是名称、类型和地址。 只要引用的对象存在于内存中，引用就一直存在。 有关详细信息[，请参阅 IDebugReference2。](../../../extensibility/debugger/reference/idebugreference2.md)

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
