---
title: 由 IDE 函数实现的回调|Microsoft Docs
description: 了解插件可以在源代码管理操作期间在适当时间调用的回调函数，以将信息传递给 IDE。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- source control plug-ins, callback functions
- callback functions, source control plug-ins
ms.assetid: 4a8833f0-6ac0-4ea7-9400-8275aa991468
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 78ce3a9cdd183cff0518ee3c6da9326c63297a85
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899142"
---
# <a name="callback-functions-implemented-by-the-ide"></a>由 IDE 实现的回调函数
若要尽可能无缝地 (IDE) 集成开发环境，并提供统一的最终用户体验，源代码管理插件可以使用由 IDE 实现的回调函数。 插件可以在源代码管理操作期间的适当时间调用这些函数，以将信息传递给 IDE;然后，IDE 可以在其本机 UI 中将此信息显示为嵌入元素。 与插件采用自己的 UI 相比，用户在此方案中的体验碎片更少。

 所需的头文件是 *scc.h*。 默认位置为 *\Program Files\VSIP 8.0\EnvSDK\common\inc \\*。 它还位于 VSIP 文件夹中，该文件夹中的源代码管理插件示例位于 *\Program Files\VSIP 8.0\MSSCCI \\*。

## <a name="in-this-section"></a>在本节中
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md) 描述 [SccOpenProject](../extensibility/sccopenproject-function.md) 用于通过 IDE 显示来自源代码管理插件的消息的回调函数。

- [POPLISTFUNC](../extensibility/poplistfunc.md) 描述 [SccPopulateList](../extensibility/sccpopulatelist-function.md) 在 IDE 无法完全访问仅适用于源代码管理插件的信息（例如版本控制下的文件的完整列表）时使用的回调函数。

- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md) 描述 [SccQueryChanges](../extensibility/sccquerychanges-function.md) 操作使用的回调函数。

- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md) 描述 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) 操作使用的回调函数。

- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md) 描述通过调用 [SccSetOption](../extensibility/sccsetoption-function.md) 设置的回调函数，该函数使源代码管理插件能够将名称更改传递回 IDE。

## <a name="related-sections"></a>相关章节
- [SccOpenProject](../extensibility/sccopenproject-function.md) 打开项目。

- [SccPopulateList](../extensibility/sccpopulatelist-function.md) 检查文件列表，了解其当前状态。 此外， 使用 `pfnPopulate` 函数在文件与 的条件不匹配时通知调用方 `nCommand` 。

- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) 检查受源代码管理的项目或项目中的目录和文件列表。 找到的每个目录和文件名都传递给回调函数。

- [SccQueryChanges](../extensibility/sccquerychanges-function.md) 检查对文件列表进行的名称更改。 每个文件名连同其更改状态一起传递给回调函数。

- [SccSetOption](../extensibility/sccsetoption-function.md) 设置各种选项。 每个选项以 开头 `SCC_OPT_xxx` ，并且具有其自己的已定义值集。

- [源代码管理插件](../extensibility/source-control-plug-ins.md) 介绍源代码管理插件 SDK 的参考部分的内容。
