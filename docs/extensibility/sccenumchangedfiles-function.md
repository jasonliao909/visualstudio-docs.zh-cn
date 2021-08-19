---
description: 给定本地文件列表后，此函数确定哪些文件与源代码管理数据库中的相应版本不同。
title: SccEnumChangedFiles 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccEnumChangedFiles
helpviewer_keywords:
- SccEnumChangedFiles function
ms.assetid: 76cac510-107b-4c1a-ba60-9c39b6db2e71
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 8d1f2cac97ee883ddca7fec7a2f5d0725459c029
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122158302"
---
# <a name="sccenumchangedfiles-function"></a>SccEnumChangedFiles 函数
给定本地文件列表后，此函数确定哪些文件与源代码管理数据库中的相应版本不同。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccEnumChangedFiles(
   LPVOID  pContext,
   HWND    hWnd,
   LONG    cFiles,
   LPCSTR* lpFileNames,
   LONG*   plIsFileDifferent
);
```

### <a name="parameters"></a>参数
 pContext

[in]源代码管理插件上下文指针。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 cFiles

[in]数组中指定的文件名 `lpFileNames` 数。 还指定数组 `plIsFileDifferent` 的大小。

 lpFileNames

[in]要检查的本地文件名数组。

 plIsFileDifferent

[in， out]值数组，指示数组中每个文件 (的状态必须至少有 `cFiles` 一个) 。 非零表示文件不同。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|操作已成功完成。|
|SCC_UNSPECIFIEDERROR|常规错误。|

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
