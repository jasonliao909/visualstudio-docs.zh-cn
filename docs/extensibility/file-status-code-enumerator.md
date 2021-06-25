---
title: 文件状态代码枚举器|Microsoft Docs
description: SccStatus 枚举器包含常量值，这些值指定源代码管理系统中文件的状态，由 SccQueryInfo 和 POPLISTFUNC 使用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- named constants, SccStatus enumerator
- source control plug-ins, file status enumeration
- SccStatus enumerator
- file status code enumerator
ms.assetid: 5c37876b-c83c-4ca1-837b-57cd465a879a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 95de8a29efcd56880cdaf452c9f21b90bba1c5c9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900962"
---
# <a name="file-status-code-enumerator"></a>文件状态代码枚举器
`SccStatus`枚举器包含指定源代码管理系统中文件的状态的命名常量值。 [SccQueryInfo](../extensibility/sccqueryinfo-function.md)和回调函数使用此枚举 (`POPLISTFUNC` [POPLISTFUNC，](../extensibility/poplistfunc.md)了解) 。

## <a name="syntax"></a>语法

```
enum SccStatus {
   SCC_STATUS_INVALID          = -1L,
   SCC_STATUS_NOTCONTROLLED    = 0x0000L,
   SCC_STATUS_CONTROLLED       = 0x0001L,
   SCC_STATUS_CHECKEDOUT       = 0x0002L,
   SCC_STATUS_OUTOTHER         = 0x0004L,
   SCC_STATUS_OUTEXCLUSIVE     = 0x0008L,
   SCC_STATUS_OUTMULTIPLE      = 0x0010L,
   SCC_STATUS_OUTOFDATE        = 0x0020L,
   SCC_STATUS_DELETED          = 0x0040L,
   SCC_STATUS_LOCKED           = 0x0080L,
   SCC_STATUS_MERGED           = 0x0100L,
   SCC_STATUS_SHARED           = 0x0200L,
   SCC_STATUS_PINNED           = 0x0400L,
   SCC_STATUS_MODIFIED         = 0x0800L,
   SCC_STATUS_OUTBYUSER        = 0x1000L
   SCC_STATUS_NOMERGE          = 0x2000L
   SCC_STATUS_RESERVED_1       = 0x4000L
   SCC_STATUS_RESERVED_2       = 0x8000L
};
```

## <a name="members"></a>成员
 SCC_STATUS_INVALID状态;不依赖它。

 SCC_STATUS_NOTCONTROLLED文件不在源代码管理下。

 SCC_STATUS_CONTROLLED文件受源代码管理。

 SCC_STATUS_CHECKEDOUT本地磁盘上的当前用户签出。

 SCC_STATUS_OUTOTHER另一个用户签出文件。

 SCC_STATUS_OUTEXCLUSIVE文件已以独占方式签出。

 SCC_STATUS_OUTMULTIPLE文件由多个用户签出。

 SCC_STATUS_OUTOFDATE文件不是最新的。

 SCC_STATUS_DELETED文件已从项目中删除。

 SCC_STATUS_LOCKED文件已锁定;不允许更多版本。

 SCC_STATUS_MERGED文件已合并但尚未修复/验证。

 SCC_STATUS_SHARED文件在项目之间共享。

 SCC_STATUS_PINNED文件共享到显式版本。

 SCC_STATUS_MODIFIED文件已被修改/损坏/违反。

 SCC_STATUS_OUTBYUSER当前用户签出文件。

 SCC_STATUS_NOMERGE文件永远不能与 合并，并且不需要在 GET 之前保存。

 SCC_STATUS_RESERVED_1保留供内部使用。

 SCC_STATUS_RESERVED_2保留供内部使用。

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [SccQueryInfo](../extensibility/sccqueryinfo-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
