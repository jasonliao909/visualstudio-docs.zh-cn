---
description: 确定是否可以在原始调试目录中查找 .pdb 文件。
title: IDiaLoadCallback2::RestrictOriginalPathAccess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2::RestrictOriginalPathAccess method
ms.assetid: 31fde3af-2824-4b0f-8d0d-cee6046596f6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: ed1c3cb17a8f1e3e43f0798bce4c18bd0457370d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832028"
---
# <a name="idialoadcallback2restrictoriginalpathaccess"></a>IDiaLoadCallback2::RestrictOriginalPathAccess
确定是否可以在原始调试目录中查找 .pdb 文件。

## <a name="syntax"></a>语法

```C++
HRESULT RestrictOriginalPathAccess ();
```

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 除以外的任何返回代码 `S_OK` 都禁止在原始调试目录中查找 .pdb 文件。 初始调试目录是打开调试时编译到可执行文件中的符号文件的路径。 此路径不一定与可执行文件所在的路径相同。

## <a name="see-also"></a>另请参阅
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
