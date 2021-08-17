---
title: POPLISTFUNC |Microsoft Docs
description: 了解 POPLISTFUNC 回调函数，该函数由源代码管理插件用来更新文件或目录列表。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- POPDIRLISTFUNC
helpviewer_keywords:
- POPLISTFUNC callback function
ms.assetid: b2199fd5-d707-4628-92dd-e2a01e2f507a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: bdd7a8fea7725d9152036bbf0b23d351d62596692118c2ef7f904c5ec886e35b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121336715"
---
# <a name="poplistfunc"></a>POPLISTFUNC
此回调由 IDE 提供给 [SccPopulateList，](../extensibility/sccpopulatelist-function.md) 由源代码管理插件用来更新文件或目录的列表 (也提供给函数 `SccPopulateList`) 。

 当用户在 IDE 中选择 **Get** 命令时，IDE 会显示一个列表框，其中列出了用户可以获取的所有文件。 遗憾的是，IDE 不知道用户可能获得的所有文件的确切列表;只有插件才具有此列表。 如果其他用户将文件添加到源代码管理项目，则这些文件应出现在列表中，但 IDE 不知道它们。 IDE 生成一个列表，其中列出了它认为用户可以获取的文件。 在向用户显示此列表之前，它会调用[SccPopulateList，](../extensibility/sccpopulatelist-function.md)使源代码管理插件有机会从列表中添加 `,` 和删除文件。

## <a name="signature"></a>签名
 源代码管理插件通过调用具有以下原型的 IDE 实现的函数来修改列表：

```cpp
typedef BOOL (*POPLISTFUNC) (
   LPVOID pvCallerData,
   BOOL fAddRemove,
   LONG nStatus,
   LPSTR lpFileName
);
```

## <a name="parameters"></a>Parameters
 pvCallerData `pvCallerData` 调用方向 [SccPopulateList](../extensibility/sccpopulatelist-function.md) (IDE) 传递的参数。 源代码管理插件不应假设此参数的内容。

 fAddRemove 如果为 ，则 是应 `TRUE` `lpFileName` 添加到文件列表中的文件。 如果 `FALSE` `lpFileName` 为 ，则 是应从文件列表中删除的文件。

 n状态： (位的组合;有关详细信息，请参阅文件状态代码 `lpFileName` `SCC_STATUS`) 。 [](../extensibility/file-status-code-enumerator.md)

 lpFileName 从列表中添加或删除的文件名的完整目录路径。

## <a name="return-value"></a>返回值

|值|描述|
|-----------|-----------------|
|`TRUE`|该插件可以继续调用此函数。|
|`FALSE`|IDE 端存在问题， (内存不足的情况) 。 插件应停止操作。|

## <a name="remarks"></a>备注
 对于源代码管理插件想要在文件列表中添加或删除的每个文件，它调用此函数，并传递 `lpFileName` 。 `fAddRemove`标志指示要添加到列表的新文件或要删除的旧文件。 `nStatus`参数提供文件的状态。 当 SCC 插件完成添加和删除文件时，它将从 [SccPopulateList](../extensibility/sccpopulatelist-function.md) 调用返回 。

> [!NOTE]
> 需要 `SCC_CAP_POPULATELIST` 功能位才能Visual Studio。

## <a name="see-also"></a>请参阅
- [由 IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
- [文件状态代码](../extensibility/file-status-code-enumerator.md)
