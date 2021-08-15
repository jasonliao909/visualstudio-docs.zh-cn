---
description: 获取正在加载或卸载的模块。
title: IDebugModuleLoadEvent2：：GetModule |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModuleLoadEvent2::GetModule
helpviewer_keywords:
- IDebugModuleLoadEvent2::GetModule
ms.assetid: c86482bb-9ce5-4e63-bbe0-969b50169424
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c632f0de62f931b68b56c321e846eca9265f50b9c19f0704da7fee2b7bd8a8ae
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417036"
---
# <a name="idebugmoduleloadevent2getmodule"></a>IDebugModuleLoadEvent2::GetModule
获取正在加载或卸载的模块。

## <a name="syntax"></a>语法

```cpp
HRESULT GetModule( 
   IDebugModule2** pModule,
   BSTR*           pbstrDebugMessage,
   BOOL*           pbLoad
);
```

```csharp
int GetModule( 
   out IDebugModule2 pModule,
   ref string        pbstrDebugMessage,
   ref int           pbLoad
);
```

## <a name="parameters"></a>参数
`pModule`\
[out]返回一 [个 IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) 对象，该对象表示正在加载或卸载的模块。

`pbstrDebugMessage`\
[in， out]返回描述此事件的可选消息。 如果此参数为 null 值，则不请求任何消息。

`pbLoad`\
[in， out]如果模块 () ，则不为零;如果模块正在卸载， () 零 `TRUE` `FALSE` 。 如果此参数为 null 值，则不请求任何状态。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
