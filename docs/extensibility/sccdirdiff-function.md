---
description: 此函数显示客户端磁盘上的当前本地目录与源代码管理下的相应项目之间的差异。
title: SccDirDiff 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccDirDiff
helpviewer_keywords:
- SccDirDiff function
ms.assetid: 26c9ba92-e3b9-4dd2-bd5e-76b17745e308
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 617c94220d13eed915a854bb9cf638bb390db1aeaa3a111c089d65283446f15e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121447761"
---
# <a name="sccdirdiff-function"></a>SccDirDiff 函数
此函数显示客户端磁盘上的当前本地目录与源代码管理下的相应项目之间的差异。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccDirDiff(
   LPVOID    pContext,
   HWND      hWnd,
   LPCSTR    lpDirName,
   LONG      dwFlags,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>参数
 pContext

[in]源代码管理插件上下文结构。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 lpDirName

[in]要显示其视觉差异的本地目录的完全限定路径。

 dwFlags 

[in]命令标志 (请参阅"备注"部分) 。

 pvOptions

[in]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|磁盘上的目录与源代码管理中的项目相同。|
|SCC_I_FILESDIFFER|磁盘上的目录与源代码管理中的项目不同。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTCONTROLLED|目录不在源代码控制下。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。 建议重试。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|
|SCC_E_FILENOTEXIST|找不到本地目录。|

## <a name="remarks"></a>备注
 此函数用于指示源代码管理插件向用户显示对指定目录的更改列表。 插件以自己选择的格式打开自己的窗口，以显示磁盘上用户的目录与版本控制下的相应项目之间的差异。

 如果插件支持目录比较，则必须支持基于文件名比较目录，即使不支持"快速差异"选项。

|`dwFlags`|解释|
|---------------|--------------------|
|SCC_DIFF_IGNORECASE|不区分大小写的比较 (可用于快速差异或视觉) 。|
|SCC_DIFF_IGNORESPACE|忽略空格 (可用于快速差异或可视) 。|
|SCC_DIFF_QD_CONTENTS|如果源代码管理插件支持，则以无提示方式比较目录、字节字节。|
|SCC_DIFF_QD_CHECKSUM|如果插件支持，则通过校验和以无提示方式比较目录，或者，如果不受支持，则回滚到SCC_DIFF_QD_CONTENTS。|
|SCC_DIFF_QD_TIME|如果受插件支持，请通过时间戳以无提示方式比较目录，或者，如果不受支持，则SCC_DIFF_QD_CHECKSUM或SCC_DIFF_QD_CONTENTS。|

> [!NOTE]
> 此函数使用与 [SccDiff 相同的命令标志](../extensibility/sccdiff-function.md)。 但是，源代码管理插件可能会选择不支持目录的"快速差异"操作。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
