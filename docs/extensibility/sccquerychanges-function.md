---
description: 此函数枚举给定的文件列表，通过回调函数提供有关每个文件的名称更改的信息。
title: SccQueryChanges 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccQueryChanges
helpviewer_keywords:
- SccQueryChanges function
ms.assetid: 4cd58eb3-6952-49b1-9620-8682e3eaa604
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f93ed14671995502356ae4a19664b14bbd32ce7b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900468"
---
# <a name="sccquerychanges-function"></a>SccQueryChanges 函数
此函数枚举给定的文件列表，通过回调函数提供有关每个文件的名称更改的信息。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccQueryChanges(
   LPVOID           pContext,
   LONG             nFiles,
   LPCSTR*          lpFileNames,
   QUERYCHANGESFUNC pfnCallback,
   LPVOID           pvCallerData
);
```

#### <a name="parameters"></a>参数
 pContext

[in]源代码管理插件上下文指针。

 nFiles

[in]数组中的文件 `lpFileNames` 数。

 lpFileNames

[in]要获取相关信息的文件名数组。

 pfnCallback

[in]若要为列表中每个文件名调用的回调函数 ([QUERYCHANGESFUNC，](../extensibility/querychangesfunc.md) 了解) 。

 pvCallerData

[in]将保持不变传递给回调函数的值。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|查询过程已成功完成。|
|SCC_E_PROJNOTOPEN|项目尚未在源代码管理中打开。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。|
|SCC_E_NONSPECIFICERROR|发生未指定或常规错误。|

## <a name="remarks"></a>备注
 要查询的更改将针对 命名空间：具体而言，重命名、添加和删除文件。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)
- [错误代码](../extensibility/error-codes.md)
