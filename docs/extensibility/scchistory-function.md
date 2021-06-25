---
description: 此函数显示指定文件的历史记录。
title: SccHistory 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccHistory
helpviewer_keywords:
- SccHistory function
ms.assetid: a636d9d3-47c1-4b48-ac6b-bcfde19d6cf9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1208bd0cb13661f1aa60bb9f97c9e4502e517e6d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902535"
---
# <a name="scchistory-function"></a>SccHistory 函数
此函数显示指定文件的历史记录。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccHistory(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

#### <a name="parameters"></a>参数
 `pvContext`

[in]源代码管理插件上下文结构。

 `hWnd`

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 `nFiles`

[in]数组中指定的文件 `lpFileName` 数。

 `lpFileName`

[in]文件的完全限定名称的数组。

 `fOptions`

[in]命令标志 (当前未) 。

 `pvOptions`

[in]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|已成功获取版本历史记录。|
|SCC_I_RELOADFILE|源代码管理系统实际上在提取历史记录时修改了 (，例如，通过获取旧版本的) ，因此 IDE 应重新加载此文件。|
|SCC_E_FILENOTCONTROLLED|该文件不在源代码管理下。|
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。 建议重试。|
|SCC_E_PROJNOTOPEN|尚未打开项目。|
|SCC_E_NONSPECIFICERROR|非特定故障。 无法获取文件历史记录。|

## <a name="remarks"></a>备注
 源代码管理插件可以显示其自己的对话框，以使用 作为父 `hWnd` 窗口来显示每个文件的历史记录。 或者，如果支持，可以使用提供给 [SccOpenProject](../extensibility/sccopenproject-function.md) 的可选文本输出回调函数。

 请注意，在某些情况下，要检查的文件在执行此调用期间可能会更改。 例如 [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] ，history 命令为用户提供获取旧版本文件的机会。 在这种情况下，源代码管理插件将返回 ，以警告 `SCC_I_RELOAD` IDE 它需要重新加载文件。

> [!NOTE]
> 如果源代码管理插件不支持文件数组的此函数，则只能显示第一个文件的文件历史记录。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
