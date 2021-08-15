---
description: 此接口表示字节数组。
title: IEEDataStorage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage
helpviewer_keywords:
- IEEDataStorage interface
ms.assetid: 704e932d-2325-410e-89c4-ce88c6ec19da
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: a975190aebbb26ac77614e1fc0e0d7a358bda3440da0b5f8bcdb7562390902e2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121415684"
---
# <a name="ieedatastorage"></a>IEEDataStorage
此接口表示字节数组。

## <a name="syntax"></a>语法

```
IEEDataStorage : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 表达式计算器 (企业版) 实现此接口，以表示由类型可视化工具用来通过[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)接口) 检索和更改数据的 (字节数组。 企业版通常实现此接口以支持外部类型可视化工具。

## <a name="notes-for-callers"></a>调用方说明
 接口上的方法 `IPropertyProxyEESide` 都返回此接口。 调用 [GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md) 以获取 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) 接口。 在[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口上调用[QueryInterface](/cpp/atl/queryinterface)以获取[IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 `IEEDataStorage`接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetData](../../../extensibility/debugger/reference/ieedatastorage-getdata.md)|检索指定数目的数据字节到提供的缓冲区。|
|[GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)|检索可用的数据字节数。|

## <a name="remarks"></a>备注
 此接口由类型可视化工具用来访问由特定对象保存的数据。 数据被视为字节数组，使类型可视化工具能够以向用户显示它所需的任何方式对其进行操作。

 如果需要，自定义查看器还可以使用此接口，尽管更常见的情况是，自定义查看器会将自定义界面、 [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md) 或 [GetStringChars](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md) (用于面向字符串的数据) 。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
