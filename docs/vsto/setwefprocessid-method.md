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
ms.workload:
- office
ms.openlocfilehash: 9c3d745f14185d46dce08d46b8c56391b108627d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99882403"
---
# <a name="setwefprocessid-method"></a>SetWefProcessId 方法
  提供将 (WEF) 内容运行 Web 扩展框架的进程标识符。

## <a name="syntax"></a>语法

```csharp
HRESULT SetWefProcessId(
    [in] DWORD dwProcessId
);
```

#### <a name="parameters"></a>parameters

|参数|说明|
|---------------|-----------------|
|*dwProcessId*|将用于运行 WEF 内容的进程标识符。|

## <a name="return-value"></a>返回值
 HRESULT 值，指示方法是否已成功完成。

## <a name="remarks"></a>备注
 在创建 WEF 内容进程之后但在任何 WEF 内容运行之前，必须调用此方法。

 如果希望开发环境将调试器附加到 WEF 内容进程，环境必须在此方法的实现中执行此操作。
