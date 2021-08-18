---
title: POPDIRLISTFUNC |Microsoft Docs
description: 了解 POPDIRLISTFUNC 回调函数，该函数传递给更新目录，以找出哪些受源代码管理。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- POPLISTFUNC
helpviewer_keywords:
- POPDIRLISTFUNC callback function
ms.assetid: 0ee90fd2-5467-4154-ab4c-7eb02ac3a14c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 21ccd6041eb5a6790635975150910bcb31a515aa6f800743ff94be45e36c579f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121447891"
---
# <a name="popdirlistfunc"></a>POPDIRLISTFUNC
这是一个回调函数，它向 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) 函数提供，用于更新目录的集合 () 选择使用文件名来找出哪些受源代码管理。

 应仅为这些目录和文件名调用回调 (在给定给实际受源代码管理) 函数 `POPDIRLISTFUNC` `SccPopulateDirList` 的列表中。

## <a name="signature"></a>签名

```cpp
typedef BOOL (*POPDIRLISTFUNC)(
   LPVOID pvCallerData,
   BOOL bFolder,
   LPCSTR lpDirectoryOrFileName
);
```

## <a name="parameters"></a>参数
 pvCallerData

[in]给定给 [SccPopulateDirList 的用户值](../extensibility/sccpopulatedirlist-function.md)。

 bFolder

[in] `TRUE` 如果 中的名称 `lpDirectoryOrFileName` 是目录，为 ;否则为文件名。

 lpDirectoryOrFileName

[in]源代码控制下的目录或文件名的完整本地路径。

## <a name="return-value"></a>返回值
 IDE 返回相应的错误代码：

|值|说明|
|-----------|-----------------|
|SCC_OK|继续处理。|
|SCC_I_OPERATIONCANCELED|停止处理。|
|SCC_E_xxx|任何适当的源代码管理错误都应停止处理。|

## <a name="remarks"></a>备注
 如果 `fOptions` 函数的 参数包含 标志，则列表可能包含文件名 `SccPopulateDirList` `SCC_PDL_INCLUDEFILES` 和目录名。

## <a name="see-also"></a>请参阅
- [由 IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)
- [错误代码](../extensibility/error-codes.md)
