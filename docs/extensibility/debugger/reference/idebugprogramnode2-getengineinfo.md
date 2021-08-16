---
description: 获取 (DE) 运行程序的调试引擎的名称和标识符。
title: IDebugProgramNode2：： GetEngineInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetEngineInfo
helpviewer_keywords:
- IDebugProgramNode2::GetEngineInfo
ms.assetid: 664e7fe5-9100-4b7d-9dc5-e5a4dd0d0451
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 17bcdaf97ae37aead254bb04c2ffde96e45bbf55501acd4817d51d9d97e95ec2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121449191"
---
# <a name="idebugprogramnode2getengineinfo"></a>IDebugProgramNode2::GetEngineInfo
获取 (DE) 运行程序的调试引擎的名称和标识符。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEngineInfo ( 
   BSTR* pbstrEngine,
   GUID* pguidEngine
);
```

```csharp
int GetEngineInfo(
   out string pbstrEngine,
   out Guid pguidEngine
);
```

## <a name="parameters"></a>参数
`pbstrEngine`\
弄返回正在运行的程序的名称 (c + + 特定的：这可以是 null 指针，指示调用方不会对引擎名称) 感兴趣。

`pguidEngine`\
弄返回运行程序 (的全局唯一标识符，该标识符是特定于 c + + 的运行程序的：这可以是 null 指针，指示调用方不会对引擎) 的 GUID 感兴趣。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
