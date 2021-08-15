---
description: 启用使用 DCOM 来请求 Visual Studio UI 的调试引擎，以确保防火墙不会阻止远程调试。
title: IDebugFirewallConfigurationCallback2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFirewallConfigurationCallback2 interface
ms.assetid: 0827361c-b97c-4851-9898-ab6d88c81811
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 18dd45fa041732f733d121d7304650ea82cf5983a76fa58e434b088ba8fcb684
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121402761"
---
# <a name="idebugfirewallconfigurationcallback2"></a>IDebugFirewallConfigurationCallback2
启用使用 DCOM 来要求 UI 的调试引擎， [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 以确保防火墙不会阻止远程调试。

## <a name="syntax"></a>语法

```
IDebugFirewallConfigurationCallback2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 由会话调试管理器的端口对象实现。

## <a name="methods"></a>方法
 下表显示的方法 `IDebugFirewallConfigurationCallback2` 。

|方法|说明|
|------------|-----------------|
|[EnsureDCOMUnblocked](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2-ensuredcomunblocked.md)|请求防火墙不阻止远程调试。|

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
