---
description: 获取有关在调试Office自动插入的应用的应用的信息。
title: GetAutoInsertExtensions 方法
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
ms.openlocfilehash: 7bb7a75c4bc1abd5c5fb29c55a3be42e44ff2af55403c1d9ecccbf00efb5c755
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121268321"
---
# <a name="getautoinsertextensions-method"></a>GetAutoInsertExtensions 方法
  获取有关在调试Office自动插入的应用的应用的信息。

 此方法保留供将来使用。

## <a name="syntax"></a>语法

```csharp
HRESULT GetAutoInsertExtensions(
    [out, retval] SAFEARRAY(BSTR)* psaExtensionNames
);
```

### <a name="parameters"></a>参数

|参数|说明|
|---------------|-----------------|
|*psaExtensionNames*|Office 的应用的扩展Office。|

## <a name="return-value"></a>返回值
 HRESULT 值，指示方法是否已成功完成。

## <a name="remarks"></a>备注
 要插入Office的每个应用都作为一Office应用程序扩展名返回，该名称对应于 **HKEY_CURRENT_USER\Software\Microsoft\Office\WEF\Developer。** 主机必须在注册表中查找这些值，然后自动插入扩展。
