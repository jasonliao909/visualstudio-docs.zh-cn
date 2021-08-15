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
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: a0e13e1ea1eda0e0768a1982b56bd7eeb496a1a2fc49ee9a2be64ad8e47dc0ea
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121424185"
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

### <a name="parameters"></a>参数

|参数|说明|
|---------------|-----------------|
|*lpwszCompatibleFrameworksXML*|请不要使用。|
|*pbstrValidFrameworkTag*|请不要使用。|

## <a name="return-value"></a>返回值
 如果该函数成功，则它将返回 **S_OK**。 如果函数失败，则返回错误代码。
