---
description: 此函数检查完全限定目录的列表，了解其当前状态。
title: SccDirQueryInfo 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccDirQueryInfo
helpviewer_keywords:
- SccDirQueryInfo function
ms.assetid: 459e2d99-573d-47c4-b834-6d82c5e14162
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9a3e65fa03c7fc2b6a8ce83ba2bb39250547aadb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904612"
---
# <a name="sccdirqueryinfo-function"></a>SccDirQueryInfo 函数
此函数检查完全限定目录的列表，了解其当前状态。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccDirQueryInfo(
LPVOID  pContext,
LONG    nDirs,
LPCSTR* lpDirNames,
LPLONG  lpStatus
);
```

### <a name="parameters"></a>参数
 pContext

[in]源代码管理插件上下文结构。

 nDirs

[in]要查询的选定目录数。

 lpDirNames

[in]要查询的目录的完全限定路径的数组。

 lpStatus

[in， out]源代码管理插件的数组结构，用于返回状态标志 (目录 [状态](../extensibility/directory-status-code-enumerator.md) 代码了解详细信息) 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|查询成功。|
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。 建议重试。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 函数使用系列中的位掩码填充返回数组， (目录状态代码) ，每个给定目录有一 `SCC_DIRSTATUS` 个[](../extensibility/directory-status-code-enumerator.md)条目。 状态数组由调用方分配。

 IDE 在重命名目录之前使用此函数，通过查询目录是否具有相应的项目来检查该目录是否受源代码管理。 如果目录不在源代码管理下，IDE 可以为用户提供适当的警告。

> [!NOTE]
> 如果源代码管理插件选择不实现一个或多个状态值，则未实现位应设置为零。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [目录状态代码](../extensibility/directory-status-code-enumerator.md)
