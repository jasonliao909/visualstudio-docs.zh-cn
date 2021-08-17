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
ms.openlocfilehash: e066da4c1c294669ad4baf4932c6d934e283a9c4914e9c23efc45ef3b1f2335d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121226097"
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
