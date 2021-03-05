---
description: 表示一个可直接访问元数据和核心符号接口的符号提供程序。
title: IDebugSymbolProviderDirect |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSymbolProviderDirect interface
ms.assetid: 872b04a8-70de-4ab5-aceb-684c81828545
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0d60af5be925341e5421badb4c3e6e3dae97903b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102149309"
---
# <a name="idebugsymbolproviderdirect"></a>IDebugSymbolProviderDirect
表示一个可直接访问元数据和核心符号接口的符号提供程序。

## <a name="syntax"></a>语法

```
IDebugSymbolProviderDirect: IUnknown
```

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetAppIDFromAddress](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getappidfromaddress.md)|检索给定了调试地址的应用程序域标识符。|
|[GetCurrentModulesInfo](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getcurrentmodulesinfo.md)|检索有关符号组中的模块的信息。|
|[GetCurrentModulesState](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getcurrentmodulesstate.md)|检索有关符号提供程序所属的符号组的信息。|
|[GetMetaDataImport](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getmetadataimport.md)|检索元数据导入信息。|
|[GetMethodFromAddress](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getmethodfromaddress.md)|检索有关指定调试地址处的方法的信息。|
|[GetSymUnmanagedReader](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getsymunmanagedreader.md)|检索非托管代码的符号读取器。|

## <a name="remarks"></a>备注
 此接口可用于替代其他所有符号提供程序接口。 它提供元数据和接口的直接访问 `CorSym` 。

## <a name="requirements"></a>要求
 标头： Sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
