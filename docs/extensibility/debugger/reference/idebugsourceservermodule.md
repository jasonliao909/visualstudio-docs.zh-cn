---
description: 表示 PDB 文件中包含的源服务器信息。
title: IDebugSourceServerModule |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSourceServerModule interface
ms.assetid: 38213060-451d-46e6-8b4a-efc123e01a2c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: d8271fe7d639ab937f3b3a51ff66b86649b90693
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664450"
---
# <a name="idebugsourceservermodule"></a>IDebugSourceServerModule
表示 PDB 文件中包含的源服务器信息。

## <a name="syntax"></a>语法

```
IDebugSourceServerModule : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 此接口由调试器引擎实现，由调试器 UI 使用。

## <a name="methods"></a>方法
 下表显示了 的方法 `IDebugSourceServerModule` 。

|方法|说明|
|------------|-----------------|
|[GetSourceServerData](../../../extensibility/debugger/reference/idebugsourceservermodule-getsourceserverdata.md)|检索源服务器信息的数组。|

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
