---
description: 此函数删除源代码管理系统中的文件。
title: SccRemove 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccRemove
helpviewer_keywords:
- SccRemove function
ms.assetid: 20830fdc-c0e9-4a5f-bf60-33f28874442f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d80daf83458c9e05ef0a081348080579e7fafef4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073867"
---
# <a name="sccremove-function"></a>SccRemove 函数
此函数删除源代码管理系统中的文件。

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

中源代码管理插件上下文结构。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 n

中数组中指定的文件数 `lpFileNames` 。

 lpFileNames

中要删除的文件的完全限定的本地路径名称数组。

 lpComment

中要应用于要删除的每个文件的注释。

 用于

中命令标志 (未使用的) 。

 pvOptions

中源代码管理插件特定的选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|删除成功。|
|SCC_E_FILENOTCONTROLLED|所选文件不受源代码管理。|
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|
|SCC_E_ISCHECKEDOUT|由于用户当前已签出某个文件，因此无法将其删除。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_NONSPECIFICERROR|模糊失败;文件未删除。|
|SCC_I_OPERATIONCANCELED|操作在完成前被取消。|

## <a name="remarks"></a>备注
 此函数会删除源代码管理系统中的文件，但不会将其从用户的本地硬盘上删除。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
