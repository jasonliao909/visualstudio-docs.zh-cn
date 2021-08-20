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
ms.openlocfilehash: c97b2fae371fd5bd72860595ba5117786b7db808
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122148241"
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
