---
description: 创建一个枚举器，其中包含与当前节贡献枚举器相同的枚举状态。
title: IDiaEnumSectionContribs::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Clone method
ms.assetid: 81d3f3a7-3684-4e5c-b028-29b268684a2c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 68e3b20d2a51a048cc1b9a3988ac0b0a02d85d76
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832238"
---
# <a name="idiaenumsectioncontribsclone"></a>IDiaEnumSectionContribs::Clone
创建一个枚举器，其中包含与当前枚举器相同的枚举状态。

## <a name="syntax"></a>语法

```C++
HRESULT Clone( 
   IDiaEnumSectionContrib** ppenum
);
```

#### <a name="parameters"></a>参数
 ppenum

[out] 返回包含枚举器副本的 [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md) 对象。 不会复制节贡献，只会复制枚举器。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)
