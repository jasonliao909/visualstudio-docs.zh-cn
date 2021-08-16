---
description: 此函数获取源代码管理插件支持的源代码管理插件 API 的版本号。
title: SccGetVersion 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGetVersion
helpviewer_keywords:
- SccGetVersion function
ms.assetid: a6e786bf-744e-4272-9e21-0be44d23b1a1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 2dd1501e4d9341241b0c07d67571d362ff0fe1dd0bffc489be8cf5c35b4ecd77
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121447748"
---
# <a name="sccgetversion-function"></a>SccGetVersion 函数
此函数获取源代码管理插件支持的源代码管理插件 API 的版本号。

## <a name="syntax"></a>语法

```cpp
LONG SccGetVersion(void);
```

#### <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 包含 `LONG` 支持的源代码管理插件 API 的版本号的数据类型：

|WORD|说明|
|----------|-----------------|
|HIWORD|主版本|
|LOWORD|次版本|

## <a name="remarks"></a>备注
 例如，如果源代码管理插件支持源代码管理插件 API 版本 1.3，则此函数将返回0x0103。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
