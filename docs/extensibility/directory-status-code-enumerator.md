---
title: 目录状态代码枚举器|Microsoft Docs
description: SccDirStatus 枚举器包含命名常量值，这些值指定源代码管理系统中目录的状态，由 SccDirQueryInfo 使用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- directory status code enumerator
- source control plug-ins, directory status enumeration
ms.assetid: 616026b5-f529-40ef-90c1-1836e116d797
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 73105d2a15ac1ad3528bcaac1b8c439b292a224ab1606d8a819a39ca607560c4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338028"
---
# <a name="directory-status-code-enumerator"></a>目录状态代码枚举器
`SccDirStatus`枚举器包含指定源代码管理系统中目录的状态的命名常量值。 此枚举由 [SccDirQueryInfo 使用](../extensibility/sccdirqueryinfo-function.md)。 源代码管理插件 API 版本 1.2 中引入了此功能。

## <a name="syntax"></a>语法

```
enum SccDirStatus {
   SCC_DIRSTATUS_INVALID       = -1L,
   SCC_DIRSTATUS_NOTCONTROLLED = 0x0000L,
   SCC_DIRSTATUS_CONTROLLED    = 0x0001L,
   SCC_DIRSTATUS_EMPTYPROJ     = 0x0002L
};
```

## <a name="members"></a>成员
 SCC_DIRSTATUS_INVALID状态;不依赖它。

 SCC_DIRSTATUS_NOTCONTROLLED目录不在源代码管理下。

 SCC_DIRSTATUS_CONTROLLED目录受源代码管理。

 SCC_DIRSTATUS_EMPTYPROJ Project目录对应的行为空。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)
