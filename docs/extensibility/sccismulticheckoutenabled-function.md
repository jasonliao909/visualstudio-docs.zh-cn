---
description: 此函数检查源代码管理插件是否允许对文件进行多次签出。
title: SccIsMultiCheckoutEnabled 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccIsMultiCheckoutEnabled
helpviewer_keywords:
- SccIsMultiCheckoutEnabled function
ms.assetid: 6721639d-e475-4766-81b5-ee40a280fc70
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: fc46414d5f48dac38c9f457f5f70ccb90698507e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110145"
---
# <a name="sccismulticheckoutenabled-function"></a>SccIsMultiCheckoutEnabled 函数
此函数检查源代码管理插件是否允许对文件进行多次签出。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccIsMultiCheckoutEnabled(
   LPVOID pContext,
   LPBOOL pbMultiCheckout
);
```

#### <a name="parameters"></a>参数
 pContext

[in]源代码管理插件上下文结构。

 pbMultiCheckout

[out]指定是否为此项目启用多个签出 (非零表示支持多个签出) 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|检查成功。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 IDE 进行两次检查，以确定多个用户是否可同时签出文件。 首先，源代码管理系统必须支持多个签出。 源代码管理插件可以通过指定 在初始化期间指定此功能 `SCC_CAP_MULTICHECKOUT` 。 此后，作为第二次检查，IDE 调用此函数以确定当前项目是否支持多个签出。 如果所选项目支持多个签出，该插件将返回成功代码，并 () `pbMultiCheckout` `TRUE` `FALSE` 非零值。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
