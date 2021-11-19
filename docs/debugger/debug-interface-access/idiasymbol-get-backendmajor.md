---
description: 检索编译器的后端主版本号。
title: IDiaSymbol::get_backEndMajor | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_backEndMajor method
ms.assetid: 900a05dd-c29b-44ad-b46b-f43bda819a66
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 09a7f32a36077d6bb80907ff81243d3d1a189257
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832609"
---
# <a name="idiasymbolget_backendmajor"></a>IDiaSymbol::get_backEndMajor
检索编译器的后端主版本号。

## <a name="syntax"></a>语法

```C++
HRESULT get_backEndMajor ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回后端主版本号。 请参阅“备注”。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 编译器通常由两个主要元素组成：前端（分析器），负责将源代码分析为中间形式；后端（代码生成器），将中间形式转换为程序集。 前端与后端具有不同版本的情况并不少见。

 前端或后端版本号由三部分组成：\<major>.\<minor>.\<build>，其中 \<major> 是主版本号，\<minor> 是次要版本号，\<build> 是生成号。 例如，13.10.3077。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
