---
title: SccGetVersion 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetVersion
helpviewer_keywords:
- SccGetVersion function
ms.assetid: a6e786bf-744e-4272-9e21-0be44d23b1a1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 91daeca1df76f6b624d0eddf9d28222369b2cc4a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99844536"
---
# <a name="sccgetversion-function"></a>SccGetVersion 函数
此函数获取源代码管理插件支持的源代码管理插件 API 版本号。

## <a name="syntax"></a>语法

```cpp
LONG SccGetVersion(void);
```

#### <a name="parameters"></a>parameters
 无。

## <a name="return-value"></a>返回值
 一个 `LONG` 数据类型，它包含受支持的源代码管理插件 API 的版本号：

|WORD|说明|
|----------|-----------------|
|HIWORD|主版本|
|LOWORD|次要版本|

## <a name="remarks"></a>备注
 例如，如果源代码管理插件支持源代码管理插件 API 版本1.3，则此函数将返回0x0103。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
