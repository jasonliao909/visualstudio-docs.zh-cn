---
description: 获取有关调试期间Office自动插入的应用的信息。
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
ms.openlocfilehash: 0a4da4447af30a44c00d824120fb6733f409a6ac
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122155988"
---
# <a name="getautoinsertextensions-method"></a>GetAutoInsertExtensions 方法
  获取有关调试期间Office自动插入的应用的信息。

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
