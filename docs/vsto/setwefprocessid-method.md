---
title: SetWefProcessId 方法
description: 了解 SetWefProcessId 方法如何提供将 (WEF) 内容运行 Web 扩展框架的进程标识符。
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
ms.openlocfilehash: 6d3fee5832c96de8fddec605399c9bd6ef565c2a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122032168"
---
# <a name="setwefprocessid-method"></a>SetWefProcessId 方法
  提供将 (WEF) 内容运行 Web 扩展框架的进程标识符。

## <a name="syntax"></a>语法

```csharp
HRESULT SetWefProcessId(
    [in] DWORD dwProcessId
);
```

#### <a name="parameters"></a>参数

|参数|说明|
|---------------|-----------------|
|*dwProcessId*|将用于运行 WEF 内容的进程标识符。|

## <a name="return-value"></a>返回值
 HRESULT 值，指示方法是否已成功完成。

## <a name="remarks"></a>备注
 在创建 WEF 内容进程之后但在任何 WEF 内容运行之前，必须调用此方法。

 如果希望开发环境将调试器附加到 WEF 内容进程，环境必须在此方法的实现中执行此操作。
