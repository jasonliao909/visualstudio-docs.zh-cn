---
description: 此方法为指定的 DE 引擎添加 (程序) 节点。
title: IDebugProcessEx2：：AddImplicitProgramNodes |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes
helpviewer_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes method
ms.assetid: 8b491b00-f9e7-45b3-9115-fe58c3464289
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0721c4cdeaae4d0109e8b130abc40d61d712bb70
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126630"
---
# <a name="idebugprocessex2addimplicitprogramnodes"></a>IDebugProcessEx2::AddImplicitProgramNodes
此方法为指定的 DE 引擎添加 (程序) 节点。

## <a name="syntax"></a>语法

```cpp
HRESULT AddImplicitProgramNodes(
   REFGUID guidLaunchingEngine,
   GUID*   rgguidSpecificEngines,
   DWORD   celtSpecificEngines
);
```

```csharp
int AddImplicitProgramNodes(
   ref Guid guidLaunchingEngine,
   Guid[]   rgguidSpecificEngines,
   uint     celtSpecificEngines
);
```

## <a name="parameters"></a>参数
`guidLaunchingEngine`\
[in]DE 的 ，用于启动 (，并假定在 `GUID`) 。

`rgguidSpecificEngines`\
[in]要 `GUID` 添加程序节点的 DES 数组。

`celtSpecificEngines`\
[in]数组中的 `GUID` 数 `rgguidSpecificEngines` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
- [将为 中列出的](../../../extensibility/debugger/program-nodes.md) 每个 DE 添加程序节点 -不包括) 中给定的 (引擎节点，该引擎假定在启动程序时添加 `rgguidSpecificEngines` 自己的程序 `guidLaunchingEngine` 节点。

## <a name="see-also"></a>请参阅
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
- [程序节点](../../../extensibility/debugger/program-nodes.md)
