---
title: IDebugSourceServerModule |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSourceServerModule interface
ms.assetid: 38213060-451d-46e6-8b4a-efc123e01a2c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8dfc4b3defc0b74c1e22c45670209682692a4807
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99837692"
---
# <a name="idebugsourceservermodule"></a>IDebugSourceServerModule
表示 PDB 文件中包含的源服务器信息。

## <a name="syntax"></a>语法

```
IDebugSourceServerModule : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 此接口由调试器引擎实现并由调试器 UI 使用。

## <a name="methods"></a>方法
 下表显示的方法 `IDebugSourceServerModule` 。

|方法|说明|
|------------|-----------------|
|[GetSourceServerData](../../../extensibility/debugger/reference/idebugsourceservermodule-getsourceserverdata.md)|检索源服务器信息的数组。|

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
