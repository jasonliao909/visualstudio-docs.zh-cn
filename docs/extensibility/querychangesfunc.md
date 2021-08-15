---
title: QUERYCHANGESFUNC |Microsoft Docs
description: QUERYCHANGESFUNC 回调函数用于枚举文件名的集合，并确定每个文件的状态。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- QUERYCHANGESFUNC
helpviewer_keywords:
- QUERYCHANGESFUNC callback function
- QUERYCHANGESDATA structure
ms.assetid: 9d383e2c-eee1-4996-973a-0652d4c5951c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: e9a28e4f75187cce110280d471f0a6f830d52e96706654c91929b324da70f57d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121375164"
---
# <a name="querychangesfunc"></a>QUERYCHANGESFUNC
这是 [SccQueryChanges](../extensibility/sccquerychanges-function.md) 操作用于枚举文件名集合并确定每个文件的状态的回调函数。

 `SccQueryChanges`函数提供文件列表和指向回调的指针 `QUERYCHANGESFUNC` 。 源代码管理插件枚举给定列表，并通过此回调) 为列表中的每个文件提供状态 (。

## <a name="signature"></a>签名

```cpp
typedef BOOL (*QUERYCHANGESFUNC)(
   LPVOID pvCallerData,
   QUERYCHANGESDATA * pChangesData
);
```

## <a name="parameters"></a>参数
 pvCallerData

中 `pvCallerData` 调用方传递的参数 (IDE) 为 [SccQueryChanges](../extensibility/sccquerychanges-function.md)。 源代码管理插件不应假设此值的内容。

 pChangesData

中指向 [QUERYCHANGESDATA 结构](#LinkQUERYCHANGESDATA) 的指针，该结构描述文件的更改。

## <a name="return-value"></a>返回值
 IDE 将返回相应的错误代码：

|值|说明|
|-----------|-----------------|
|SCC_OK|继续处理。|
|SCC_I_OPERATIONCANCELED|停止处理。|
|SCC_E_xxx|任何适当的 SCC 错误都应停止处理。|

## <a name="querychangesdata-structure"></a><a name="LinkQUERYCHANGESDATA"></a> QUERYCHANGESDATA 结构
 为每个文件传入的结构如下所示：

```cpp
struct QUERYCHANGESDATA_A
{
    DWORD  dwSize;
    LPCSTR lpFileName;
    DWORD  dwChangeType;
    LPCSTR lpLatestName;
};

typedef struct QUERYCHANGESDATA_A QUERYCHANGESDATA;

struct QUERYCHANGESDATA_W
{
    DWORD   dwSize;
    LPCWSTR lpFileName;
    DWORD   dwChangeType;
    LPCWSTR lpLatestName;
};
```

 此结构的 dwSize 大小)  (以字节为单位）。

 lpFileName 此项的原始文件名。

 指示文件状态的 dwChangeType 代码：

|代码|说明|
|----------|-----------------|
|`SCC_CHANGE_UNKNOWN`|无法判断发生了什么变化。|
|`SCC_CHANGE_UNCHANGED`|此文件没有名称更改。|
|`SCC_CHANGE_DIFFERENT`|具有不同标识但同名的文件存在于数据库中。|
|`SCC_CHANGE_NONEXISTENT`|文件在数据库中或在本地不存在。|
|`SCC_CHANGE_DATABASE_DELETED`|已在数据库中删除文件。|
|`SCC_CHANGE_LOCAL_DELETED`|文件在本地删除，但该文件仍然存在于数据库中。 如果无法确定，则返回 `SCC_CHANGE_DATABASE_ADDED` 。|
|`SCC_CHANGE_DATABASE_ADDED`|文件已添加到数据库中，但不存在于本地。|
|`SCC_CHANGE_LOCAL_ADDED`|文件在数据库中不存在，并且是新的本地文件。|
|`SCC_CHANGE_RENAMED_TO`|文件在数据库中重命名或移动为 `lpLatestName` 。|
|`SCC_CHANGE_RENAMED_FROM`|已在数据库中重命名或移动文件 `lpLatestName` ; 如果此值太昂贵而无法跟踪，则返回其他标志，例如 `SCC_CHANGE_DATABASE_ADDED` 。|

 lpLatestName 此项的当前文件名。

## <a name="see-also"></a>另请参阅
- [IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccQueryChanges](../extensibility/sccquerychanges-function.md)
- [错误代码](../extensibility/error-codes.md)
