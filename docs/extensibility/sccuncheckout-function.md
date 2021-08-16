---
description: 此函数撤消以前的签出操作，从而将所选文件或文件的内容还原到签出之前的状态。
title: SccUncheckout 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccUncheckout
helpviewer_keywords:
- SccUncheckout function
ms.assetid: 6d498b70-29c7-44b7-ae1c-7e99e488bb09
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f98cbcab81570b78a1455a47b67bb9da873222acec9c81be590eaaccb1cfdab4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121400551"
---
# <a name="sccuncheckout-function"></a>SccUncheckout 函数
此函数撤消以前的签出操作，从而将所选文件或文件的内容还原到签出之前的状态。 自签出以来对文件进行的所有更改将丢失。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccUncheckout (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
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

[in]要撤消签出的文件的完全限定本地路径名称的数组。

 fOptions

[in]命令标志 (不) 。

 pvOptions

[in]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|撤消签出成功。|
|SCC_E_FILENOTCONTROLLED|所选文件不在源代码控制下。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特定故障。 撤消签出未成功。|
|SCC_E_NOTCHECKEDOUT|用户未签出文件。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_PROJNOTOPEN|项目尚未从源代码管理打开。|
|SCC_I_OPERATIONCANCELED|操作在完成之前已取消。|

## <a name="remarks"></a>备注
 此操作后，将同时为执行撤消签出的文件清除 `SCC_STATUS_CHECKEDOUT` `SCC_STATUS_MODIFIED` 和 标志。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
