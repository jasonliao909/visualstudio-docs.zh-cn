---
description: 启用一个调试引擎，该引擎使用 DCOM Visual Studio UI，以确保防火墙不会阻止远程调试。
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
ms.openlocfilehash: 899413fa9064b463732fd2985bb0ddaf8dddf5a4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122088739"
---
# <a name="idebugfirewallconfigurationcallback2"></a>IDebugFirewallConfigurationCallback2
启用使用 DCOM 来请求 UI 确保防火墙不会阻止远程调试的 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 调试引擎。

## <a name="syntax"></a>语法

```
IDebugFirewallConfigurationCallback2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 由会话调试管理器的端口对象实现。

## <a name="methods"></a>方法
 下表显示了 的方法 `IDebugFirewallConfigurationCallback2` 。

|方法|说明|
|------------|-----------------|
|[EnsureDCOMUnblocked](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2-ensuredcomunblocked.md)|请求防火墙不阻止远程调试。|

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
