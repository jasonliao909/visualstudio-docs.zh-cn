---
description: 按源文件标识符检索源文件。
title: IDiaSession::findFileById | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findFileById method
ms.assetid: 710efe04-78b5-4f3e-a1d8-f9b069063503
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 2e34d25ea59b20eebc986106123070dd1d23b9dd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831920"
---
# <a name="idiasessionfindfilebyid"></a>IDiaSession::findFileById
按源文件标识符检索源文件。

## <a name="syntax"></a>语法

```C++
HRESULT findFileById ( 
   DWORD            uniqueId,
   IDiaSourceFile** ppResult
);
```

#### <a name="parameters"></a>参数
 `uniqueId`

[in] 指定源文件标识符。

 `ppResult`

[out] 返回表示检索到的源文件的 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="remarks"></a>备注
 源文件标识符是在内部用于 DIA SDK 的唯一值，用于使所有源文件唯一。 此方法通常在内部用于 DIA SDK。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
