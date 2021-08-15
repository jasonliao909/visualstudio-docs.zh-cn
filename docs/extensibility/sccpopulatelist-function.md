---
description: 此函数更新特定源代码管理命令的文件列表，并针对所有给定文件提供源代码管理状态。
title: SccPopulateList 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccPopulateList
helpviewer_keywords:
- SccPopulateList function
ms.assetid: 7416e781-c571-4a7f-8af3-a089ce8be662
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ce9ed39a90e467bb31f8272d9977406149a5b1ecdf3eecc390903ad0bf24c9e2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121305199"
---
# <a name="sccpopulatelist-function"></a>SccPopulateList 函数
此函数更新特定源代码管理命令的文件列表，并针对所有给定文件提供源代码管理状态。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccPopulateList (
   LPVOID          pvContext,
   enum SCCCOMMAND nCommand,
   LONG            nFiles,
   LPCSTR*         lpFileNames,
   POPLISTFUNC     pfnPopulate,
   LPVOID          pvCallerData,
   LPLONG          lpStatus,
   LONG            fOptions
);
```

#### <a name="parameters"></a>参数
 pvContext

[in]源代码管理插件上下文结构。

 nCommand

[in]将应用于数组中所有文件的源代码管理 (请参阅命令代码，了解命令中可能 `lpFileNames`) 。 [](../extensibility/command-code-enumerator.md)

 nFiles

[in]数组中的文件 `lpFileNames` 数。

 lpFileNames

[in]IDE 已知的文件名数组。

 pfnPopulate

[in]要调用以添加和删除文件的 IDE 回调函数 ([POPLISTFUNC，](../extensibility/poplistfunc.md) 了解) 。

 pvCallerData

[in]将保持不变传递给回调函数的值。

 lpStatus

[in， out]源代码管理插件的数组，用于返回每个文件的状态标志。

 fOptions

[in]命令标志 (请参阅特定命令使用的 [Bitflags](../extensibility/bitflags-used-by-specific-commands.md) 的"PopulateList 标志"部分，了解) 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|成功。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 此函数检查文件列表，了解其当前状态。 当文件与 的条件不匹配时，它使用回调函数 `pfnPopulate` 通知调用方 `nCommand` 。 例如，如果命令为 且列表中未签出文件，则回调 `SCC_COMMAND_CHECKIN` 用于通知调用方。 有时，源代码管理插件可能会找到其他文件，这些文件可能是命令的一部分并添加它们。 例如，这允许Visual Basic签出其项目.bmp但不显示在项目文件中Visual Basic文件。 用户在 IDE 中选择 **Get** 命令。 IDE 将显示它认为用户可以获取的所有文件的列表，但在显示列表之前，将调用 函数以确保要显示的列表是 `SccPopulateList` 最新的。

## <a name="example"></a>示例
 IDE 会生成一个认为用户可以获取的文件列表。 在显示此列表之前，它会调用 函数，使源代码管理插件有机会从列表中添加 `SccPopulateList` 和删除文件。 插件通过调用给定的回调函数来修改列表， ([POPLISTFUNC](../extensibility/poplistfunc.md) 了解详细信息) 。

 插件将继续调用 函数，该函数添加和删除文件，直到它完成， `pfnPopulate` 然后从函数 `SccPopulateList` 返回。 然后，IDE 可以显示其列表。 数组 `lpStatus` 表示 IDE 传入的原始列表中的所有文件。 插件除了使用回调函数之外，还填充所有这些文件的状态。

> [!NOTE]
> 源代码管理插件始终可以选择直接从此函数返回，并保留列表。 如果插件实现此函数，则可以通过在首次调用 `SCC_CAP_POPULATELIST` [SccInitialize](../extensibility/sccinitialize-function.md)时设置功能位标志来指示这一点。 默认情况下，插件应始终假定传入的所有项都是文件。 但是，如果 IDE 在 参数中设置 标志 `SCC_PL_DIR` `fOptions` ，则传入的所有项都将被视为目录。 插件应添加属于目录的所有文件。 IDE 永远不会将文件和目录混合使用。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
- [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md)
- [命令代码](../extensibility/command-code-enumerator.md)
