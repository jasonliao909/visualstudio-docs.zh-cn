---
description: 表示变量的数值别名。
title: IDebugAlias |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias
helpviewer_keywords:
- IDebugAlias interface
ms.assetid: 3cc4c9a4-7805-4239-b00e-eb4a024f3c55
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 52590d62bb2bc6d9090432efe7e11a343601cfd9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122064781"
---
# <a name="idebugalias"></a>IDebugAlias
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示变量的数值别名。 别名只是变量的不同名称。

## <a name="syntax"></a>语法

```
IDebugAlias : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 表达式计算 (企业版) 实现此接口以支持变量的数字别名。

## <a name="notes-for-callers"></a>调用方说明
- [CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md) 为特定对象创建别名。 若要搜索别名，请使用 [FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md) 或 [GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 以下方法在 接口中 `IDebugAlias` 定义。

|方法|说明|
|------------|-----------------|
|[GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)|获取此别名引用的对象。|
|[GetName](../../../extensibility/debugger/reference/idebugalias-getname.md)|获取别名。|
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugalias-geticordebugvalue.md)|检索一 `ICorDebugValue` 个接口，该接口提供对此对象的托管代码信息的访问 (托管代码) 。|
|[释放](../../../extensibility/debugger/reference/idebugalias-dispose.md)|将此别名标记为不再使用。|

## <a name="remarks"></a>备注
 别名是字符串形式的十进制数，后跟 # 字符，例如 1001#。

## <a name="requirements"></a>要求
 标头：ee.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)
- [FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)
- [GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)
