---
description: 此函数将以前签出的文件签入到源代码管理系统，存储更改并创建新版本。
title: SccCheckin 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccCheckin
helpviewer_keywords:
- SccCheckin function
ms.assetid: e3f26ac2-6163-42e1-a764-22cfea5a3bc6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: e97fb25d9d0d3f91914d3e8d965796877b77a8dfc41a0812b1b6cc0a93aba794
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121400876"
---
# <a name="scccheckin-function"></a>SccCheckin 函数
此函数将以前签出的文件签入到源代码管理系统，存储更改并创建新版本。 使用计数和要签入的文件的名称数组调用此函数。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccCheckin (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPSTR*    lpFileNames,
   LPCSTR    lpComment,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>参数
 pvContext

[in]源代码管理插件上下文结构。

 hWnd

[in]SCC 插件可以用作其提供的任何对话框的父级的 IDE 窗口句柄。

 nFiles

[in]要签入的选定文件数。

 lpFileNames

[in]要签入的文件的完全限定的本地路径名称的数组。

 lpComment

[in]要应用于要签入的每个选定文件的注释。 如果 `NULL` 源代码管理插件应提示提供注释，则此参数为 。

 fOptions

[in]命令标志，0 或 `SCC_KEEP_CHECKEDOUT` 。

 pvOptions

[in]特定于 SCC 插件的选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|文件已成功签入。|
|SCC_E_FILENOTCONTROLLED|所选文件不在源代码控制下。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特定故障。 文件未签入。|
|SCC_E_NOTCHECKEDOUT|用户尚未签出该文件，因此无法签入。|
|SCC_E_CHECKINCONFLICT|无法执行签入，因为：<br /><br /> - 另一个用户已提前签入， `bAutoReconcile` 并且为 false。<br /><br /> -或-<br /><br /> - 自动合并不能 (，例如，当文件是二进制) 。|
|SCC_E_VERIFYMERGE|文件已自动合并，但尚未签入挂起的用户验证。|
|SCC_E_FIXMERGE|文件已自动合并，但由于必须手动解决的合并冲突而未签入。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_I_OPERATIONCANCELED|操作在完成之前已取消。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTEXIST|找不到本地文件。|

## <a name="remarks"></a>备注
 注释适用于正在签入的所有文件。 comment 参数可以是字符串，在这种情况下，源代码管理插件可以提示 `null` 用户输入每个文件的注释字符串。

 可以给参数提供 标志的值，以指示用户签入文件并 `fOptions` `SCC_KEEP_CHECKEDOUT` 再次签出文件的意向。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
