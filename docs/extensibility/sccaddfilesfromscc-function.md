---
description: 此函数将文件列表从源代码管理添加到当前打开的项目。
title: SccAddFilesFromSCC 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccAddFilesFromSCC
helpviewer_keywords:
- SccAddFilesFromSCC function
ms.assetid: f21a3500-ade8-4dd8-8647-10e2179be9c1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c8d8715f18d68c6e8f3250f25e14a45da48ab8cd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602329"
---
# <a name="sccaddfilesfromscc-function"></a>SccAddFilesFromSCC 函数
此函数将文件列表从源代码管理添加到当前打开的项目。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccAddFilesFromSCC(
   LPVOID  pContext,
   HWND    hWnd,
   LPSTR   lpUser,
   LPSTR   lpAuxProjPath,
   LONG    cFiles,
   LPCSTR* lpFilePaths,
   LPCSTR  lpDestination,
   LPCSTR  lpComment,
   LPBOOL  pbResults
);
```

### <a name="parameters"></a>parameters
 pContext

[in]源代码管理插件上下文指针。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 lpUser

[in， out]用户名 (为 SCC_USER_SIZE，包括 null 终止符) 。

 lp一文ProjPath

[in， out]辅助字符串，标识项目 (`SCC_PRJPATH_` SIZE，包括 null 终止符) 。

 cFiles

[in]提供的文件数 `lpFilePaths` 。

 lpFilePaths

[in， out]要添加到当前项目的文件名数组。

 lpDestination

[in]要写入文件的目标路径。

 lpComment

[in]要应用于要添加的每个文件的注释。

 pbResults

[in， out]标志的数组，设置为指示成功 (非零或 TRUE) 或失败 (零或 FALSE) 对于每个文件 (数组的大小必须至少为 long `cFiles`) 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_E_PROJNOTOPEN|Project未打开。|
|SCC_E_OPNOTPERFORMED|连接与 指定的项目不同 `lpAuxProjPath.`|
|SCC_E_NOTAUTHORIZED|用户无权更新数据库。|
|SCC_E_NONSPECIFICERROR|未知错误。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
