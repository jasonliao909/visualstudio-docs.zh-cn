---
title: 目录状态代码枚举器 |Microsoft Docs
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
ms.openlocfilehash: 81f7e81ded2b45b560350c065e13ef69455468d9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665356"
---
# <a name="directory-status-code-enumerator"></a>目录状态代码枚举器
`SccDirStatus`枚举器包含指定源代码管理系统中目录状态的命名常量值。 此枚举由 [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)使用。 源代码管理插件 API 版本1.2 中引入了此项。

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
 无法获取 SCC_DIRSTATUS_INVALID 状态;不要依赖于它。

 SCC_DIRSTATUS_NOTCONTROLLED 目录不受源代码管理。

 SCC_DIRSTATUS_CONTROLLED 目录受源代码管理。

 与此目录相对应 SCC_DIRSTATUS_EMPTYPROJ Project 为空。

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)
