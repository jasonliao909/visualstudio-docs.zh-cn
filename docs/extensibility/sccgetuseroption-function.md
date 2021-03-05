---
description: 此函数检索各种用户特定的选项。
title: SccGetUserOption 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetUserOption
helpviewer_keywords:
- SccGetUserOption function
ms.assetid: 17863747-1901-4c53-a2b3-ed996085e120
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c137630e4a29fc534e9bfced16cffe862e07a046
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102220620"
---
# <a name="sccgetuseroption-function"></a>SccGetUserOption 函数
此函数检索各种用户特定的选项。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccGetUserOption(
   LPVOID pContext,
   LONG nOption,
   LPLONG lpVal
);
```

#### <a name="parameters"></a>参数
 pContext

中源代码管理插件上下文指针。

 nOption

中用于检索 (的选项，请参阅) 的可能选项的备注。

 lpVal

弄与选项关联的值。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|已成功检索选项。|
|SCC_E_OPNOTSUPPORTED|选项不受支持。|
|SCC_E_NONSPECIFICERROR|发生了未指定的错误。|

## <a name="remarks"></a>备注
 此命令支持以下选项：

|用户选项|描述|
|-----------------|-----------------|
|`SCC_USEROPT_CHECKOUT_LOCALVER`|确定用户是否希望签出文件的本地版本。 `lpVal` 分配 `SCC_USEROPT_COLV_YES` (用户要) 或签出本地文件 `SCC_USEROPT_COLV_NO` 。|

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [错误代码](../extensibility/error-codes.md)
