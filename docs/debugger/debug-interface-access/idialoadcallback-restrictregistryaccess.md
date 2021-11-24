---
description: 确定是否可以使用注册表查询来查找符号搜索路径。
title: IDiaLoadCallback::RestrictRegistryAccess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::RestrictRegistryAccess method
ms.assetid: de4760c3-a746-4bab-8065-1388fed31b67
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 3ed6183e1e159b1883d268a2514c597df7d09197
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832038"
---
# <a name="idialoadcallbackrestrictregistryaccess"></a>IDiaLoadCallback::RestrictRegistryAccess
确定是否可以使用注册表查询来查找符号搜索路径。

## <a name="syntax"></a>语法

```C++
HRESULT RestrictRegistryAccess();
```

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="remarks"></a>备注
 除 `S_OK` 外的任何返回代码都阻止查询注册表来获取符号搜索路径。

## <a name="see-also"></a>另请参阅
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
