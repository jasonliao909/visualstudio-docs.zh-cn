---
description: 将转储写入文件。
title: IDebugProgram2：：WriteDump |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::WriteDump
helpviewer_keywords:
- IDebugProgram2::WriteDump
ms.assetid: 375afb8c-882d-44db-bfa7-e2c9eb555122
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1cbe4f60032be54f3b76d1b9f98701b0a5e52c00
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122030069"
---
# <a name="idebugprogram2writedump"></a>IDebugProgram2::WriteDump
将转储写入文件。

## <a name="syntax"></a>语法

```cpp
HRESULT WriteDump( 
   DUMPTYPE  DumpType,
   LPCOLESTR pszDumpUrl
);
```

```csharp
int WriteDump( 
   enum_DUMPTYPE  DumpType,
   string         pszDumpUrl
);
```

## <a name="parameters"></a>参数
`DumpType`\
[in]DUMPTYPE [枚举](../../../extensibility/debugger/reference/dumptype.md) 中的一个值，该值指定转储的类型，例如 short 或 long。

`pszDumpUrl`\
[in]要写入转储的 URL。 通常，此格式为 `file://c:\path\filename.ext` ，但可能是任何有效的 URL。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 程序转储通常包括当前堆栈帧、堆栈本身、在程序中运行的线程列表，以及程序拥有的任何内存。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
