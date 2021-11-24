---
description: 检索映像应基于的内存位置。
title: IDiaImageData::get_imageBase | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaImageData::get_imageBase method
ms.assetid: 4ba3d9e4-b205-4ee6-a41d-6996972f1f85
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 699ad3a289ff790c414a4c3e8a552436a22ab633
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832096"
---
# <a name="idiaimagedataget_imagebase"></a>IDiaImageData::get_imageBase
检索映像应基于的内存位置。

## <a name="syntax"></a>语法

```C++
HRESULT get_imageBase ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回建议的映像基值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="remarks"></a>备注
 由于映像基底冲突，加载时可能会自动将映像变基到未使用的内存位置。 此方法返回在编译时存储在模块中的基础映像提示（建议的内存位置）。

## <a name="see-also"></a>另请参阅
- [IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)
