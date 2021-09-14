---
description: 指定从程序提供程序获取的所需属性。
title: PROVIDER_FLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROVIDER_FLAGS
helpviewer_keywords:
- PROVIDER_FLAGS enumeration
ms.assetid: 8cbd2312-ed2f-4477-b192-c3f25c6098c3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 116943ce1fd85b9f4dee2dc0f1512301a900fa74
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665366"
---
# <a name="provider_flags"></a>PROVIDER_FLAGS
指定从程序提供程序获取的所需属性。

## <a name="syntax"></a>语法

```cpp
enum enum_PROVIDER_FLAGS {
   PFLAG_NONE                    = 0x00,
   PFLAG_REMOTE_PORT             = 0x01,
   PFLAG_DEBUGGEE                = 0x02,
   PFLAG_ATTACHED_TO_DEBUGGEE    = 0x04,
   PFLAG_REASON_WATCH            = 0x08,
   PFLAG_GET_PROGRAM_NODES       = 0x10,
   PFLAG_GET_IS_DEBUGGER_PRESENT = 0x20
};
typedef DWORD PROVIDER_FLAGS;
```

```csharp
public enum enum_PROVIDER_FLAGS {
   PFLAG_NONE                    = 0x00,
   PFLAG_REMOTE_PORT             = 0x01,
   PFLAG_DEBUGGEE                = 0x02,
   PFLAG_ATTACHED_TO_DEBUGGEE    = 0x04,
   PFLAG_REASON_WATCH            = 0x08,
   PFLAG_GET_PROGRAM_NODES       = 0x10,
   PFLAG_GET_IS_DEBUGGER_PRESENT = 0x20
};
```

## <a name="fields"></a>字段
 `PFLAG_NONE`\
 未指定标志。

 `PFLAG_REMOTE_PORT`\
 调用方需要与 不同的计算机上程序的列表 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 。

 `PFLAG_DEBUGGEE`\
 进程当前正由 的此实例调试 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 。

 `PFLAG_ATTACH_TODEBUGGEE`\
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 附加到正在调试的程序，但没有启动它。

 `PFLAG_REASON_WATCH`\
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 正在监视事件。

 `PFLAG_GET_PROGRAM_NODES`\
 调用方需要 `ProgramNodes` 该结构PROVIDER_PROCESS_DATA字段。 [](../../../extensibility/debugger/reference/provider-process-data.md)

 `PFLAG_GET_IS_DEBUGGER_PRESENT`\
 调用方需要 `fIsTheDebuggerPresent` 结构的 `PROVIDER_PROCESS_DATA` 字段。

## <a name="remarks"></a>备注
 这些标志将传递给以下方法：

- [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)

- [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)

- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)

  这些值可以与位 合并 `OR` 。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)
- [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)
- [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
