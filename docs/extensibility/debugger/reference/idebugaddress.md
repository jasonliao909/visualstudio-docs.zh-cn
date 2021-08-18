---
description: 此接口表示项的地址。
title: IDebugAddress |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress
helpviewer_keywords:
- IDebugAddress interface
ms.assetid: bc709ff7-4966-4f36-9af2-690efe2cea1d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: ce700d7f002689d4257f93f079862504c902d0ee
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122104451"
---
# <a name="idebugaddress"></a>IDebugAddress
此接口表示项的地址。 它由符号处理程序返回。

## <a name="syntax"></a>语法

```
IDebugAddress : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 符号提供程序实现此接口以表示对象的地址。

## <a name="notes-for-callers"></a>调用方说明
 许多接口上的许多方法都返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[获取地址](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)|检索描述对象及其位置的 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 结构。|

## <a name="remarks"></a>备注
 符号提供程序返回此接口以表示对象及其在特定范围 (例如，函数、方法或类) 中的位置。 此接口从返回并传递给符号提供程序和表达式计算器的各种方法。 通常，符号提供程序是唯一需要解释此接口内容的实体。

## <a name="requirements"></a>要求
 标头： sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
