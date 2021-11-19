---
description: 检索枚举序列中指定数目的源文件。
title: IDiaEnumSourceFiles::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSourceFiles::Next method
ms.assetid: 83bf6317-ff39-4c5c-8987-cba34e7a6983
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: a2b7e18417cead3100a879b2a9f2dcd19ed18f22
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832197"
---
# <a name="idiaenumsourcefilesnext"></a>IDiaEnumSourceFiles::Next
检索枚举序列中指定数目的源文件。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG            celt,
   IDiaSourceFile** rgelt,
   ULONG*           pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

中要检索的枚举器中的源文件数。

 rgelt

弄一个数组，它将用表示所需源文件的 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) 对象进行填充。

 pceltFetched

弄返回提取的枚举器中的源文件数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 `S_FALSE`如果没有更多的源文件，则返回。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)
- [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
