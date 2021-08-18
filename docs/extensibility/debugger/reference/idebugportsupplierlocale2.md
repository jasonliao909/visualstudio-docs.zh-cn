---
description: 为端口供应商提供区域设置支持。
title: IDebugPortSupplierLocale2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierLocale2 interface
ms.assetid: 910e7220-da2a-4339-9fff-9fb1bad3c28c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: fb273e38e207f36f7d438b7fba0bfe093f1c8344
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122088011"
---
# <a name="idebugportsupplierlocale2"></a>IDebugPortSupplierLocale2
为端口供应商提供区域设置支持。

## <a name="syntax"></a>语法

```
IDebugPortSupplierLocale2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 自定义端口供应商实现此接口以设置区域设置。

## <a name="methods"></a>方法
 下表显示了 **IDebugPortSupplierLocale2** 的方法。

|方法|说明|
|------------|-----------------|
|[SetLocale](../../../extensibility/debugger/reference/idebugportsupplierlocale2-setlocale.md)|设置端口供应商的区域设置。|

## <a name="requirements"></a>要求
 标头： Portpriv

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
