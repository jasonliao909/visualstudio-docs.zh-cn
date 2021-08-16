---
description: 此函数调用源代码管理管理工具。
title: SccRunScc 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccRunScc
helpviewer_keywords:
- SccRunScc function
ms.assetid: bbe7c931-b17a-4779-9cf6-59e5f9f0c172
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 277bfe2aa6c49a8d93307ce93d46b6fff6156f4f9c4fc008f6e5bb8e25212a6d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121413942"
---
# <a name="sccrunscc-function"></a>SccRunScc 函数
此函数调用源代码管理管理工具。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccRunScc(
   LPVOID  pvContext,
   HWND    hWnd,
   LONG    nFiles,
   LPCSTR* lpFileNames
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

[in]所选文件名的数组。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功调用源代码管理管理工具。|
|SCC_I_OPERATIONCANCELED|操作已取消。|
|SCC_E_INITIALIZEFAILED|无法初始化源代码管理系统。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。|
|SCC_E_CONNECTIONFAILURE|无法连接到源代码管理系统。|
|SCC_E_FILENOTCONTROLLED|所选文件不在源代码管理下。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 此函数允许调用方通过外部管理工具访问源代码管理系统的全部功能。 如果源代码管理系统没有用户界面，源代码管理插件可以实施接口来执行必要的管理功能。

 使用当前所选文件的计数和文件名数组调用此函数。 如果管理工具支持，则文件列表可用于在管理界面中预先选择文件;否则，可以忽略列表。

 当用户从"文件源代码管理 **\<Source Control Server>**"菜单中选择"启动"时，  ->  **通常会调用此** 函数。 通过 **设置** 注册表项，始终可以禁用甚至隐藏此"启动"菜单选项。 有关详细信息 [，请参阅如何：安装源代码管理](../extensibility/internals/how-to-install-a-source-control-plug-in.md) 插件。 只有在[SccInitialize](../extensibility/sccinitialize-function.md)返回功能位时，才调用此 (请参阅功能标志，了解有关此功能位和其他功能位 `SCC_CAP_RUNSCC`) 。 [](../extensibility/capability-flags.md)

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [如何：安装源代码管理插件](../extensibility/internals/how-to-install-a-source-control-plug-in.md)
- [功能标志](../extensibility/capability-flags.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
