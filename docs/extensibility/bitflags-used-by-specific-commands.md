---
title: 特定命令使用的位|Microsoft Docs
description: 了解源代码管理插件 API 使用的位标志，它们由使用它们的函数进行组织。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- source control plug-ins, bitflags used by specific commands
ms.assetid: 37969977-6f7d-45c9-ba03-1306ae71f5d1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 9cfa48cc8ef55e8fcd574055d1d0c6acc9c84935
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122043825"
---
# <a name="bitflags-used-by-specific-commands"></a>特定命令使用的位标志
可以通过在单个值中设置一个或多个位来修改源代码管理插件 API 中许多函数的行为。 这些值称为位标志。 此处详细介绍了源代码管理插件 API 使用的各种位标志，这些位标志按使用它们的函数分组。

## <a name="checked-out-flag"></a>签出标志
 可以针对 [SccAdd](../extensibility/sccadd-function.md) 或 [SccCheckin 设置此标志](../extensibility/scccheckin-function.md)。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_KEEP_CHECKEDOUT`|0x1000|使文件保持签出状态。|

## <a name="add-flags"></a>添加标志
 [SccAdd 使用这些标志](../extensibility/sccadd-function.md)。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_FILETYPE_AUTO`|0x00|源代码管理插件应自动检测文件是文本还是二进制文件。|
|`SCC_FILETYPE_TEXT`|0x01|文件类型为 text。|
|`SCC_FILETYPE_BINARY`|0x04|文件类型为二进制。 **注意：** `SCC_FILETYPE_TEXT``SCC_FILETYPE_BINARY`和 标志互斥。   只设置一个或两者。|
|`SCC_ADD_STORELATEST`|0x02|仅存储最新版本 (没有增量) 。|

## <a name="diff-flags"></a>差异标志
 [SccDiff](../extensibility/sccdiff-function.md)使用这些标志来定义差异操作的范围。 标志 `SCC_DIFF_QD_xxx` 是互斥的。 如果指定了其中任何一个，则不提供视觉反馈。 在"快速差异" (QD) 中，插件不会确定文件的差异，只有当文件不同时。 如果未指定这些标志，则完成"视觉差异";将计算并显示详细的文件差异。 如果请求的 QD 不受支持，插件将移动到下一个最佳 QD。 例如，如果 IDE 请求校验和，并且插件不支持校验和，则插件执行完整内容检查 (比可视化显示) 。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_DIFF_IGNORECASE`|0x0002|忽略大小写差异。|
|`SCC_DIFF_IGNORESPACE`|0x0004|忽略空白差异。 **注意：**  和 `SCC_DIFF_IGNORECASE` `SCC_DIFF_IGNORESPACE` 标志是可选的位标志。|
|`SCC_DIFF_QD_CONTENTS`|0x0010|通过比较整个文件内容进行 QD。|
|`SCC_DIFF_QD_CHECKSUM`|0x0020|QD by checksum。|
|`SCC_DIFF_QD_TIME`|0x0040|按文件日期/时间戳进行 QD。|
|`SCC_DIFF_QUICK_DIFF`|0x0070|这是一个掩码，用于检查所有 QD 位标志。 它不应传递到函数中;这三个 QD 位标志是互斥的。 QD 始终表示不显示 UI。|

## <a name="populatelist-flag"></a>PopulateList 标志
 此标志由 [参数中的 SccPopulateList](../extensibility/sccpopulatelist-function.md) `fOptions` 使用。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_PL_DIR`|0x00000001L|IDE 传递的是目录，而不是文件。|

## <a name="populatedirlist-flags"></a>PopulateDirList 标志
 这些标志由 参数中的 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) `fOptions` 使用。

|选项值|值|说明|
|------------------|-----------|-----------------|
|SCC_PDL_ONELEVEL|0x0000|仅检查目录的一 (这是默认) 。|
|SCC_PDL_RECURSIVE|0x0001|以递归方式检查每个给定目录下的所有目录。|
|SCC_PDL_INCLUDEFILES|0x0002|在检查过程中包括文件名。|

## <a name="openproject-flags"></a>OpenProject 标志
 这些标志由 [参数中的 SccOpenProject](../extensibility/sccopenproject-function.md) `dwFlags` 使用。

|选项值|值|说明|
|------------------|-----------|-----------------|
|SCC_OP_CREATEIFNEW|0x00000001L|如果源代码管理中不存在项目，请创建它。 如果未设置此标志，则提示用户项目创建 (，除非 `SCC_OP_SILENTOPEN` 在) 。|
|SCC_OP_SILENTOPEN|0x00000002L|不提示用户创建项目;只需返回 `SCC_E_UNKNOWNPROJECT` 。|

## <a name="get-flags"></a>获取标志
 SccGet 和[](../extensibility/sccget-function.md)[SccCheckout 使用这些标志](../extensibility/scccheckout-function.md)。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_GET_ALL`|0x00000001L|IDE 传递的是目录，而不是文件：获取这些目录中的所有文件。|
|`SCC_GET_RECURSIVE`|0x00000002L|IDE 正在传递目录：获取这些目录及其所有子目录。|

## <a name="noption-values"></a>nOption 值
 [SccSetOption](../extensibility/sccsetoption-function.md)在 参数中使用这些 `nOption` 标志。

|标志|值|说明|
|----------|-----------|-----------------|
|`SCC_OPT_EVENTQUEUE`|0x00000001L|设置事件队列的状态。|
|`SCC_OPT_USERDATA`|0x00000002L|为 指定用户数据 `SCC_OPT_NAMECHANGEPFN` 。|
|`SCC_OPT_HASCANCELMODE`|0x000000003L|IDE 可以处理取消。|
|`SCC_OPT_NAMECHANGEPFN`|0x00000004L|为名称更改设置回调。|
|`SCC_OPT_SCCCHECKOUTONLY`|0x000000005L|禁用源代码管理插件 UI 签出，不设置工作目录。|
|`SCC_OPT_SHARESUBPROJ`|0x000000006L|从源代码管理系统添加 以指定工作目录。 如果关联项目是直接后代，请尝试共享该项目。|

## <a name="dwval-bitflags"></a>dwVal 位标志
 [SccSetOption](../extensibility/sccsetoption-function.md)在 参数中使用这些 `dwVal` 标志。

|标志|值|说明|由值 `nOption` 使用|
|----------|-----------|-----------------|-----------------------------|
|`SCC_OPT_EQ_DISABLE`|0x00L|挂起事件队列活动。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_EQ_ENABLE`|0x01L|启用事件队列日志记录。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_HCM_NO`|0L| (默认) 无取消模式;插件必须提供 （如果需要）。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_HCM_YES`|1L|IDE 处理取消。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_SCO_NO`|0L| (默认) "确定"，以从插件 UI 签出;工作目录已设置。|`SCC_OPT_SCCCHECKOUTONLY`|
|`SCC_OPT_SCO_YES`|1L|没有插件 UI 签出，没有工作目录。|`SCC_OPT_SCCCHECKOUTONLY`|

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
