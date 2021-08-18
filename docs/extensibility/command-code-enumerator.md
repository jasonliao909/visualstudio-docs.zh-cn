---
title: 命令代码枚举器|Microsoft Docs
description: 命令代码枚举器用于 SccGetCommandOptions 和 SccPopulateListto 的选项中，以指示指定选项的命令。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- command code enumerator
- source control plug-ins, command code enumeration
ms.assetid: 5d2c360c-59e4-4da8-bcb4-dd07c7441e40
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 37c692cc7f2dcfa1f978b5448b84e255178a6cf390bb50a1a2918a6981a07543
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434797"
---
# <a name="command-code-enumerator"></a>命令代码枚举器
此枚举器用于 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) 和 [SccPopulateList](../extensibility/sccpopulatelist-function.md)的选项中，以指示指定选项的命令。

## <a name="syntax"></a>语法

```
enum SCCCOMMAND {
   SCC_COMMAND_GET,
   SCC_COMMAND_CHECKOUT,
   SCC_COMMAND_CHECKIN,
   SCC_COMMAND_UNCHECKOUT,
   SCC_COMMAND_ADD,
   SCC_COMMAND_REMOVE,
   SCC_COMMAND_DIFF,
   SCC_COMMAND_HISTORY,
   SCC_COMMAND_RENAME,
   SCC_COMMAND_PROPERTIES,
   SCC_COMMAND_OPTIONS
};
```

## <a name="members"></a>成员
SCC_COMMAND_GET对应于 [SccGet](../extensibility/sccget-function.md)。

SCC_COMMAND_CHECKOUT对应于 [SccCheckout](../extensibility/scccheckout-function.md)。

SCC_COMMAND_CHECKIN对应于 [SccCheckin](../extensibility/scccheckin-function.md)。

SCC_COMMAND_UNCHECKOUT对应于 [SccUncheckout](../extensibility/sccuncheckout-function.md)。

SCC_COMMAND_ADD对应于 [SccAdd](../extensibility/sccadd-function.md)。

SCC_COMMAND_REMOVE 对应于 [SccRemove](../extensibility/sccremove-function.md)。

SCC_COMMAND_DIFF对应于 [SccDiff](../extensibility/sccdiff-function.md)。

SCC_COMMAND_HISTORY对应于 [SccHistory](../extensibility/scchistory-function.md)。

SCC_COMMAND_RENAME对应于 [SccRename](../extensibility/sccrename-function.md)。

SCC_COMMAND_PROPERTIES对应于 [SccProperties](../extensibility/sccproperties-function.md)。

SCC_COMMAND_OPTIONS对应于 [SccSetOption](../extensibility/sccsetoption-function.md)。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
