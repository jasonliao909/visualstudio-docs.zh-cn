---
title: QUERYCHANGESFUNC |Microsoft Docs
description: QUERYCHANGESFUNC 回调函数用于枚举文件名的集合并确定每个文件的状态。
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
ms.workload:
- vssdk
ms.openlocfilehash: b061fbfb6644f77348574020c0a5cb614691ae6b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899129"
---
# <a name="querychangesfunc"></a>QUERYCHANGESFUNC
这是 [SccQueryChanges](../extensibility/sccquerychanges-function.md) 操作用来枚举文件名集合并确定每个文件状态的回调函数。

 `SccQueryChanges`为函数提供文件列表和指向回调的 `QUERYCHANGESFUNC` 指针。 源代码管理插件对给定的列表进行枚举，并 (通过此回调) 列表中每个文件的状态。

## <a name="signature"></a>签名

```cpp
typedef BOOL (*QUERYCHANGESFUNC)(
   LPVOID pvCallerData,
   QUERYCHANGESDATA * pChangesData
);
```

## <a name="parameters"></a>参数
 pvCallerData

[in]调用方 `pvCallerData` 将 IDE (传递给 [SccQueryChanges](../extensibility/sccquerychanges-function.md)) 参数。 源代码管理插件不应对此值的内容做出任何假设。

 pChangesData

[in]指向 [描述对文件的更改的 QUERYCHANGESDATA](#LinkQUERYCHANGESDATA) 结构结构的指针。

## <a name="return-value"></a>返回值
 IDE 返回相应的错误代码：

|值|描述|
|-----------|-----------------|
|SCC_OK|继续处理。|
|SCC_I_OPERATIONCANCELED|停止处理。|
|SCC_E_xxx|任何适当的 SCC 错误都应停止处理。|

## <a name="querychangesdata-structure"></a><a name="LinkQUERYCHANGESDATA"></a> QUERYCHANGESDATA 结构
 每个文件传入的结构如下所示：

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

 dwSize 此结构的大小 (字节数) 。

 lpFileName 此项的原始文件名。

 dwChangeType 代码，指示文件的状态：

|代码|说明|
|----------|-----------------|
|`SCC_CHANGE_UNKNOWN`|无法判断发生了哪些更改。|
|`SCC_CHANGE_UNCHANGED`|此文件的名称不会更改。|
|`SCC_CHANGE_DIFFERENT`|具有不同标识的文件，但数据库中存在同一名称。|
|`SCC_CHANGE_NONEXISTENT`|数据库中或本地不存在文件。|
|`SCC_CHANGE_DATABASE_DELETED`|在数据库中删除的文件。|
|`SCC_CHANGE_LOCAL_DELETED`|文件已在本地删除，但该文件仍然存在于数据库中。 如果无法确定这一点，则返回 `SCC_CHANGE_DATABASE_ADDED` 。|
|`SCC_CHANGE_DATABASE_ADDED`|文件已添加到数据库，但本地不存在。|
|`SCC_CHANGE_LOCAL_ADDED`|数据库中不存在文件，它是一个新的本地文件。|
|`SCC_CHANGE_RENAMED_TO`|数据库中重命名或移动的文件为 `lpLatestName` 。|
|`SCC_CHANGE_RENAMED_FROM`|在数据库中重命名或移动的文件;如果跟踪成本过高，则 `lpLatestName` 返回其他标志，例如 `SCC_CHANGE_DATABASE_ADDED` 。|

 lpLatestName 此项的当前文件名。

## <a name="see-also"></a>另请参阅
- [由 IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccQueryChanges](../extensibility/sccquerychanges-function.md)
- [错误代码](../extensibility/error-codes.md)
