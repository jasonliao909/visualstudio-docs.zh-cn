---
title: 对字符串长度的限制 |Microsoft Docs
description: 了解由源代码管理插件 API 施加的各种函数所使用的字符串长度限制。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- source control plug-ins, restrictions on string lengths
ms.assetid: 877173d2-ca27-43b3-b1f4-8379f7c5e268
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 5322ff52097a55994cec569597841202677d7dfd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602333"
---
# <a name="restrictions-on-string-lengths"></a>字符串长度限制
源代码管理插件 API 限制各种函数中使用的字符串的长度。

## <a name="string-length-values"></a>字符串长度值

|常数|“值”|
|--------------|-----------|
|`SCC_NAME_LEN`|31|
|`SCC_AUXLABEL_LEN`|31|
|`SCC_USER_LEN`|31|
|`SCC_PRJPATH_LEN`|300|

> [!NOTE]
> 长度不包括终止 `null` 。 具有 "_SIZE" 后缀而不是 "_LEN" 的其他常量都包含用于终止的空间 `null` 。

|常数|“值”|
|--------------|-----------|
|SCC_NAME_SIZE|32|
|SCC_AUXLABEL_SIZE|32|
|SCC_USER_SIZE|32|
|SCC_PRJPATH_SIZE|301|

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
