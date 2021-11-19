---
description: 返回与指定的内联函数名称对应的内联帧的符号枚举。
title: IDiaSession::findAcceleratorInlineesByName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: e203e5c2-6563-43fa-be56-3063955043ab
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 813be3beb3514e716a025086efdd579344686f2e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831924"
---
# <a name="idiasessionfindacceleratorinlineesbyname"></a>IDiaSession::findAcceleratorInlineesByName
返回与指定的内联函数名称对应的内联帧的符号枚举。

## <a name="syntax"></a>语法

```C++
HRESULT findAcceleratorInlineeLinesByName ( 
   LPCOLESTR             name,
   DWORD                 option,
   IDiaEnumSymbols**     ppResult
);
```

#### <a name="parameters"></a>参数
 `name`

[in]要搜索的内联函数名称。

 `option`

[in]搜索与 对应的内联帧时使用的名称搜索选项 `name` 。 有关详细信息，请参阅 [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)。

 `ppResult`

[out]指向使用 `IDiaEnumSymbols` 结果初始化的接口指针的指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 此函数仅在快捷键存根函数中搜索内联。 它忽略本机 C++ 过程记录。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
