---
title: GetVstoSolutionMetadata 函数
description: 了解 GetVstoSolutionMetadata API 如何支持Office基础结构，并且不能直接从代码中使用。
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
ms.openlocfilehash: 14cf1d9ab6c8c3a734caa737b99a5edaededb94f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122026416"
---
# <a name="getvstosolutionmetadata-function"></a>GetVstoSolutionMetadata 函数
  此 API 支持Office基础结构，不直接通过代码使用。

## <a name="syntax"></a>语法

```csharp
HRESULT WINAPI GetVstoSolutionMetadata(
    LPCWSTR lpwszSolutionMetadataKey,
    ISolutionMetadata** ppSolutionInfo
);
```

### <a name="parameters"></a>参数

|参数|说明|
|---------------|-----------------|
|*lpwszSolutionMetadataKey*|请不要使用。|
|*ppSolutionInfo*|请不要使用。|

## <a name="return-value"></a>返回值
 如果函数成功， **它将返回** S_OK。 如果函数失败，它将返回错误代码。
