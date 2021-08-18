---
description: 此函数获取源代码管理下一组选定文件的状态信息。
title: SccQueryInfo 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccQueryInfo
helpviewer_keywords:
- SccQueryInfo function
ms.assetid: 3973d336-a9b7-41a2-a4e6-bb8184a96aaf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 7b61a5cfd52bfbeadf2b11212bd3f215390d2d4d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110002"
---
# <a name="sccqueryinfo-function"></a>SccQueryInfo 函数
此函数获取源代码管理下一组选定文件的状态信息。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccQueryInfo(
   LPVOID  pvContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LPLONG  lpStatus
);
```

#### <a name="parameters"></a>参数
 pvContext

[in]源代码管理插件上下文结构。

 nFiles

[in]数组中指定的文件 `lpFileNames` 数和数组 `lpStatus` 的长度。

 lpFileNames

[in]要查询的文件的名称的数组。

 lpStatus

[in， out]一个数组，其中源代码管理插件返回每个文件的状态标志。 有关详细信息，请参阅文件 [状态代码](../extensibility/file-status-code-enumerator.md)。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|查询成功。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。 建议重试。|
|SCC_E_PROJNOTOPEN|项目未在源代码管理下打开。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 如果 `lpFileName` 为空字符串，则当前没有要更新的状态信息。 否则，它是状态信息可能已更改的文件的完整路径名称。

 返回数组可以是位掩码 `SCC_STATUS_xxxx` 。 有关详细信息，请参阅文件 [状态代码](../extensibility/file-status-code-enumerator.md)。 源代码管理系统可能不支持所有位类型。 例如， `SCC_STATUS_OUTOFDATE` 如果未提供 ，则不设置位。

 使用此函数签出文件时，请注意以下 `MSSCCI` 状态要求：

- `SCC_STATUS_OUTBYUSER` 在当前用户签出文件时设置 。

- `SCC_STATUS_CHECKEDOUT` 除非设置了 ，否则 `SCC_STATUS_OUTBYUSER` 无法设置 。

- `SCC_STATUS_CHECKEDOUT` 仅在将文件签出到指定的工作目录中时设置。

- 如果当前用户将文件签出到工作目录外的其他目录中，则 设置 `SCC_STATUS_OUTBYUSER` ， `SCC_STATUS_CHECKEDOUT` 但不设置 。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [文件状态代码](../extensibility/file-status-code-enumerator.md)
