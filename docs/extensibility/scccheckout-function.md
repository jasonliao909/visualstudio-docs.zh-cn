---
description: 给定完全限定文件名的列表后，此函数会将其签出到本地驱动器。
title: SccCheckout 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccCheckout
helpviewer_keywords:
- SccCheckout function
ms.assetid: 06e9ecd7-fc09-40c1-9dd1-2b56c622c80b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 72d36ccaf5c6dcddb6730f52b0ce1c3074c605a7
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904716"
---
# <a name="scccheckout-function"></a>SccCheckout 函数
给定完全限定文件名的列表后，此函数会将其签出到本地驱动器。 注释适用于要签出的所有文件。注释参数可以是 `null` 字符串。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccCheckout (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LPCSTR    lpComment,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>参数
 pvContext

[in]源代码管理插件上下文结构。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 nFiles

[in]要签出的文件数。

 lpFileNames

[in]要签出的文件的完全限定本地路径名称的数组。

 lpComment

[in]要应用于要签出的每个选定文件的注释。

 fOptions

[in]命令标志 (特定命令使用的[Bitflags) 。](../extensibility/bitflags-used-by-specific-commands.md)

 pvOptions

[in]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|签出成功。|
|SCC_E_FILENOTCONTROLLED|所选文件不在源代码控制下。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。 建议重试。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_NONSPECIFICERROR|非特定故障。 文件未签出。|
|SCC_E_ALREADYCHECKEDOUT|用户已签出文件。|
|SCC_E_FILEISLOCKED|文件已锁定，禁止创建新版本。|
|SCC_E_FILEOUTEXCLUSIVE|另一个用户已对此文件执行排他签出。|
|SCC_I_OPERATIONCANCELED|操作在完成之前已取消。|

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md)
