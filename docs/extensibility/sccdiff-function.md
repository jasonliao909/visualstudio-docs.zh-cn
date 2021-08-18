---
description: 此函数 (或选择性地只检查) 本地磁盘 (上的当前文件) 与源代码管理系统中上次签入版本之间的差异。
title: SccDiff 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccDiff
helpviewer_keywords:
- SccDiff function
ms.assetid: d49bc8c5-f631-4153-9d3c-feb3564da305
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 1a644d677fb2a6f1d50909294649b270617a5bf0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122117613"
---
# <a name="sccdiff-function"></a>SccDiff 函数
此函数 (或选择性地只检查) 本地磁盘 (上的当前文件) 与源代码管理系统中上次签入版本之间的差异。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccDiff(
   LPVOID    pvContext,
   HWND      hWnd,
   LPCSTR    lpFileName,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>参数
 pvContext

[in]源代码管理插件上下文结构。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 lpFileName

[in]请求差异的文件名。

 fOptions

[in]命令标志。 有关详细信息，请参阅“备注”。

 pvOptions

[in]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|工作副本和服务器版本相同。|
|SCC_I_FILESDIFFERS|工作副本不同于源代码管理下的版本。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTCONTROLLED|该文件不在源代码管理下。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特定故障;未获取文件差异。|
|SCC_E_FILENOTEXIST|找不到本地文件。|

## <a name="remarks"></a>备注
 此函数有两种不同的用途。 默认情况下，它显示对文件的更改列表。 源代码管理插件以它选择的任何格式打开自己的窗口，以显示用户磁盘上的文件与源代码管理下文件的最新版本之间的差异。

 或者，IDE 可能只需确定文件是否已更改。 例如，IDE 可能需要在不通知用户的情况下确定签出文件是否安全。 在这种情况下，IDE 将传递 标志 `SCC_DIFF_CONTENTS` 。 源代码管理插件必须对照源代码管理文件检查磁盘上的文件（字节字节），并返回一个值，该值指示两个文件是否不同，而不向用户显示任何内容。

 作为性能优化，源代码管理插件可能会使用基于校验和或时间戳的替代方法，而不是由 调用的字节比较：这些比较形式明显更快但 `SCC_DIFF_CONTENTS` 不太可靠。 并非所有源代码管理系统都支持这些备用比较方法，插件可能必须回退到内容比较。 所有源代码管理插件都必须至少支持内容比较。

> [!NOTE]
> 快速差异标志是互斥的。 不传递标志有效，但同时传递多个标志无效。 `SCC_DIFF_QUICK_DIFF`（合并所有标志的掩码）可用于测试，但不应将其作为参数传递。

|`fOption`|含义|
|---------------|-------------|
|SCC_DIFF_IGNORECASE|不区分大小写的比较 (可用于快速或视觉差异) 。|
|SCC_DIFF_IGNORESPACE|忽略空格 (可用于快速或视觉差异) 。|
|SCC_DIFF_QD_CONTENTS|以无提示方式比较文件（字节）。|
|SCC_DIFF_QD_CHECKSUM|如果支持，则通过校验和以无提示方式比较文件。 如果不受支持， 将返回到内容的比较。|
|SCC_DIFF_QD_TIME|如果支持，则通过文件的时间戳以无提示方式比较文件。 如果不受支持， 将返回到内容的比较。|

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
