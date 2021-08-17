---
description: 检索特定程序的程序节点。
title: IDebugProgramProvider2：： GetProviderProgramNode |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::GetProviderProgramNode
helpviewer_keywords:
- IDebugProgramProvider2::GetProviderProgramNode
ms.assetid: e62e8e83-acbb-4c52-aedf-ffbd4670db29
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bf520d68a47b8a7e8f4ed7b71c7544ffdf0a947fcdc2c140c68f0ce7ef328bf1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121402566"
---
# <a name="idebugprogramprovider2getproviderprogramnode"></a>IDebugProgramProvider2::GetProviderProgramNode
检索特定程序的程序节点。

## <a name="syntax"></a>语法

```cpp
HRESULT GetProviderProgramNode(
   PROVIDER_FLAGS       Flags,
   IDebugDefaultPort2*  pPort,
   AD_PROCESS_ID        processId,
   REFGUID              guidEngine,
   UINT64               programId,
   IDebugProgramNode2** ppProgramNode
);
```

```csharp
int GetProviderProgramNode(
   enum_PROVIDER_FLAGS    Flags,
   IDebugDefaultPort2     pPort,
   AD_PROCESS_ID          ProcessId,
   ref Guid               guidEngine,
   ulong                  programId,
   out IDebugProgramNode2 ppProgramNode
);
```

## <a name="parameters"></a>参数
`Flags`\
中 [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md) 枚举中的标志的组合。 下面是此调用的典型标志：

|标志|描述|
|----------|-----------------|
|`PFLAG_REMOTE_PORT`|调用方正在远程计算机上运行。|
|`PFLAG_DEBUGGEE`|当前正在调试调用方 (将为每个节点) 返回有关封送的附加信息。|
|`PFLAG_ATTACHED_TO_DEBUGGEE`|调用方已附加到，但调试器未启动。|

`pPort`\
中正在运行调用进程的端口。

`processId`\
中一个 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 结构，它保存包含相关程序的进程的 ID。

`guidEngine`\
中如果任何) ，程序会附加到 (的调试引擎的 GUID。

`programId`\
中要获取其程序节点的程序的 ID。

`ppProgramNode`\
弄表示请求的程序节点的 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
