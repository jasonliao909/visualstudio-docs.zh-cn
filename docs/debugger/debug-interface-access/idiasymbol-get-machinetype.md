---
description: 检索目标 CPU 的类型。
title: IDiaSymbol::get_machineType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_machineType method
ms.assetid: 30870b10-6f32-45c6-a0d7-020dea707710
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 7b3d3712b8e74b5aab1f5427fc5b058090eeaf59
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832742"
---
# <a name="idiasymbolget_machinetype"></a>IDiaSymbol::get_machineType
检索目标 CPU 的类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_machineType ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 从 [IMAGE_FILE_MACHINE_ Constants](/windows/desktop/SysInfo/image-file-machine-constants) 返回一个指定目标 CPU 类型的值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="see-also"></a>另请参阅
- [IMAGE_FILE_MACHINE_ Constants](/windows/desktop/SysInfo/image-file-machine-constants) 
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
