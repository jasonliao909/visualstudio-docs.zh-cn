---
description: 在给定要检查的目录 (，此函数) 文件（可选）存储在源代码管理中。
title: SccPopulateDirList 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccPopulateDirList
helpviewer_keywords:
- SccPopulateDirList function
ms.assetid: dfff634b-b155-498b-a356-6eb252ac4fad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b20978e9eeb45f402fbade7f7e7de5dc92a66295
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110054"
---
# <a name="sccpopulatedirlist-function"></a>SccPopulateDirList 函数
在给定要检查的目录 (，此函数) 文件（可选）存储在源代码管理中。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccPopulateDirList(
   LPVOID        pContext,
   LONG          nDirs,
   LPCSTR*       lpDirPaths,
   POPDIRLISTFUNCpfnPopulate,
   LPVOID        pvCallerData,
   LONG          fOptions
);
```

#### <a name="parameters"></a>参数
 pContext

[in]源代码管理插件上下文指针。

 nDirs

[in]数组中的目录路径 `lpDirPaths` 数。

 lpDirPaths

[in]要检查的目录路径数组。

 pfnPopulate

[in]若要调用每个目录路径和路径的回调 (可以选择) 文件名 (`lpDirPaths` [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md) 了解) 。

 pvCallerData

[in]将保持不变传递给回调函数的值。

 fOptions

[in]控制如何处理目录的值的组合 (请参阅特定命令使用的 [Bitflags](../extensibility/bitflags-used-by-specific-commands.md) 的"PopulateDirList 标志"部分，了解可能的值) 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功完成该操作”。|
|SCC_E_UNKNOWNERROR|出现了错误。|

## <a name="remarks"></a>备注
 只有这些 (和) 源代码管理存储库中实际使用的文件名才传递给回调函数。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md)
- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)
- [错误代码](../extensibility/error-codes.md)
