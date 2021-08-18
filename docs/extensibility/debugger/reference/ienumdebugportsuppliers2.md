---
description: 此接口枚举端口供应商。
title: IEnumDebugPortSuppliers2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPortSuppliers2
helpviewer_keywords:
- IEnumDebugPortSuppliers2
ms.assetid: cd0a73dc-dd25-46fd-8c4f-5b011501afeb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 7620b528b90bf2a34894618ad186c4fdb8aa1c2e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122034820"
---
# <a name="ienumdebugportsuppliers2"></a>IEnumDebugPortSuppliers2
此接口枚举端口供应商。

## <a name="syntax"></a>语法

```
IEnumDebugPortSuppliers2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 Visual Studio 实现此接口来表示端口供应商的列表。

## <a name="notes-for-callers"></a>调用方说明
 调用 [EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md) 以获取端口供应商列表。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IEnumDebugPortSuppliers2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-next.md)|检索枚举序列中指定数目的端口供应商。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-skip.md)|跳过枚举序列中指定数目的端口供应商。|
|[重置](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-reset.md)|将枚举序列重置到开始处。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-getcount.md)|获取枚举器中的端口供应商数。|

## <a name="remarks"></a>备注
 通常，调试引擎不需要获取此接口。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)
