---
description: 表示具有特定于托管代码的方法的 COM+ 符号提供程序。
title: IDebugComPlusSymbolProvider |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider interface
ms.assetid: 5b98e908-fd15-49a6-9010-933c9b948085
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: da8d6c4ebd64c4dd4f3a4610e2f4753b86aa0ef5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122145037"
---
# <a name="idebugcomplussymbolprovider"></a>IDebugComPlusSymbolProvider
表示具有特定于托管代码的方法的 COM+ 符号提供程序。

## <a name="syntax"></a>语法

```
IDebugComPlusSymbolProvider : IDebugSymbolProvider
```

## <a name="notes-for-implementers"></a>实现者说明
 尽管对表达式计算程序和 DE (企业版) 使用的接口没有 () 分离， 以下方法可能仅对 DE 开发人员感兴趣：AreSymbolsLoaded、GetAddressesInModuleFromPosition、GetEntryPoint、GetFunctionLineOffset、GetLocalVariableLayout、IsFunctionStale、LoadSymbols、LoadSymbolsFromStream、ReplaceSymbols、UnloadSymbols 和 UpdateSymbols。

## <a name="methods"></a>方法
 除了 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) 接口上的方法外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[AreSymbolsLoaded](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-aresymbolsloaded.md)|根据给定的应用程序域标识符，确定是否为指定的模块加载调试符号。|
|[CreateTypeFromPrimitive](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-createtypefromprimitive.md)|从指定的基元类型创建类型。|
|[GetAddressesInModuleFromPosition](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getaddressesinmodulefromposition.md)|地图指定模块中的文档位置指定为调试地址数组。|
|[GetArrayTypeFromAddress](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getarraytypefromaddress.md)|根据指定的数组的调试地址检索有关该数组的类型信息。|
|[GetAssemblyName](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getassemblyname.md)|根据程序集的模块和应用程序域检索程序集的名称。|
|[GetAttributedClassesForLanguage](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getattributedclassesforlanguage.md)|检索具有以给定编程语言实现的指定特性的类。|
|[GetAttributedClassesinModule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getattributedclassesinmodule.md)|检索给定模块中具有指定属性的类。|
|[GetEntryPoint](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getentrypoint.md)|检索应用程序入口点。|
|[GetFunctionLineOffset](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getfunctionlineoffset.md)|检索表示给定行偏移量的函数中的地址。|
|[GetLocalVariablelayout](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getlocalvariablelayout.md)|检索一组方法的本地变量的布局。|
|[GetNameFromToken](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getnamefromtoken.md)|返回与指定标记关联的名称（给定其元数据对象）。|
|[GetSymAttribute](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getsymattribute.md)|检索具有指定模块的给定父属性的调试符号。|
|[GetSymUnmanagedReader](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getsymunmanagedreader.md)|检索非托管代码使用的符号读取器。|
|[GetTypeFromAddress](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-gettypefromaddress.md)|根据给定的调试地址检索到符号类型。|
|[IsFunctionDeleted](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-isfunctiondeleted.md)|确定是否删除指定调试地址中的函数。|
|[IsFunctionStale](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-isfunctionstale.md)|确定指定调试地址中的函数是否被视为过时。|
|[IsHiddenCode](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-ishiddencode.md)|确定指定调试器地址中的代码是否隐藏。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-loadsymbols.md)|在内存中加载指定的调试符号。|
|[LoadSymbolsFromStream](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-loadsymbolsfromstream.md)|加载给定数据流的调试符号。|
|[ReplaceSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-replacesymbols.md)|将当前调试符号替换为指定数据流中的符号。|
|[UnloadSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-unloadsymbols.md)|从内存中卸载指定模块的调试符号。|
|[UpdateSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-updatesymbols.md)|使用指定的数据流更新内存中的调试符号。|

## <a name="requirements"></a>要求
 标头：Sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
