---
title: GetValidCompatibleFramework 函数
description: 了解 GetValidCompatibleFramework API 如何支持 Office 基础结构，不应在代码中直接使用。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b089f954c59219461c8e267ee6e88e47015fc794
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860615"
---
# <a name="getvalidcompatibleframework-function"></a>GetValidCompatibleFramework 函数
  此 API 支持 Office 基础结构，不应在代码中直接使用。

## <a name="syntax"></a>语法

```csharp
HRESULT WINAPI GetValidCompatibleFramework(
    LPCWSTR lpwszCompatibleFrameworksXML,
    BSTR* pbstrValidFrameworkTag
);
```

### <a name="parameters"></a>parameters

|参数|说明|
|---------------|-----------------|
|*lpwszCompatibleFrameworksXML*|请勿使用。|
|*pbstrValidFrameworkTag*|请勿使用。|

## <a name="return-value"></a>返回值
 如果该函数成功，则它将返回 **S_OK**。 如果函数失败，则返回错误代码。
