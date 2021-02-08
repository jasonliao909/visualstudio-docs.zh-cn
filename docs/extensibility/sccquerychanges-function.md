---
title: SccQueryChanges 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccQueryChanges
helpviewer_keywords:
- SccQueryChanges function
ms.assetid: 4cd58eb3-6952-49b1-9620-8682e3eaa604
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fd69183b290fa194d87dff79d69596dd65ec19ba
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99836717"
---
# <a name="sccquerychanges-function"></a>SccQueryChanges 函数
此函数枚举给定的文件列表，并通过回调函数提供每个文件的名称更改的相关信息。

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

#### <a name="parameters"></a>parameters
 pContext

中源代码管理插件上下文指针。

 n

中数组中的文件数 `lpFileNames` 。

 lpFileNames

中要获取其相关信息的文件名数组。

 pfnCallback

中要对列表中的每个文件名调用的回调函数 (参阅 [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md) 了解详细信息) 。

 pvCallerData

中将以不更改的形式传递给回调函数的值。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|查询过程已成功完成。|
|SCC_E_PROJNOTOPEN|未在源代码管理中打开该项目。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。|
|SCC_E_NONSPECIFICERROR|出现未指定的错误或常规错误。|

## <a name="remarks"></a>备注
 查询的更改是命名空间：具体而言，即重命名、添加和删除文件。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)
- [错误代码](../extensibility/error-codes.md)
