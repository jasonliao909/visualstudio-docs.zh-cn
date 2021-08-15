---
description: 此函数从源代码管理系统中删除文件。
title: SccRemove 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccRemove
helpviewer_keywords:
- SccRemove function
ms.assetid: 20830fdc-c0e9-4a5f-bf60-33f28874442f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c3555d53ccd845d878fe91f8802e4f8b02f3087475dbd8cb85800aee5b23d961
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121413929"
---
# <a name="sccremove-function"></a>SccRemove 函数
此函数从源代码管理系统中删除文件。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccRemove(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LPCSTR    lpComment,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

#### <a name="parameters"></a>参数
 pvContext

[in]源代码管理插件上下文结构。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 nFiles

[in]数组中指定的文件 `lpFileNames` 数。

 lpFileNames

[in]要删除的文件的完全限定本地路径名称的数组。

 lpComment

[in]要应用于要删除的每个文件的注释。

 fOptions

[in]命令标志 (未使用的) 。

 pvOptions

[in]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|删除成功。|
|SCC_E_FILENOTCONTROLLED|所选文件不在源代码管理下。|
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|
|SCC_E_ISCHECKEDOUT|无法删除文件，因为用户当前已签出该文件。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_NONSPECIFICERROR|非特定故障;文件未删除。|
|SCC_I_OPERATIONCANCELED|操作在完成之前已取消。|

## <a name="remarks"></a>备注
 此函数从源代码管理系统中删除文件，但不从用户的本地硬盘驱动器中删除这些文件。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
