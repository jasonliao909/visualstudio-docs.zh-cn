---
description: 检索 C++ 修饰名的一部分或全部未修饰的名称 (链接) 名称。
title: IDiaSymbol：：get_undecoratedNameEx |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_undecoratedNameEx method
ms.assetid: 579aed0b-c57d-41a1-a94a-3bf665fd4a9d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 3db4b03f874a2f45c83989c01244fcba3308d334
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832649"
---
# <a name="idiasymbolget_undecoratednameex"></a>IDiaSymbol::get_undecoratedNameEx
检索 C++ 修饰名的一部分或全部未修饰的名称 (链接) 名称。

## <a name="syntax"></a>语法

```C++
HRESULT get_undecoratedNameEx( 
   DWORD undecorateOptions,
   BSTR* pRetval
);
```

#### <a name="parameters"></a>参数
 `undecoratedOptions`

[in]指定控制返回项的标志的组合。 有关特定值及其功能，请参阅"备注"部分。

 `pRetVal`

[out]返回 C++ 修饰名的未修饰名称。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 表示属性不可用于符号。

## <a name="remarks"></a>备注
 `undecorateOptions`可以是以下标志的组合。

> [!NOTE]
> 标志名称未在代码中DIA SDK，因此需要将声明添加到代码或使用原始值。

|标志|值|说明|
|----------|-----------|-----------------|
|UNDNAME_COMPLETE|0x0000|启用完全取消修饰。|
|UNDNAME_NO_LEADING_UNDERSCORES|0x0001|从 Microsoft 扩展关键字中删除前导下划线。|
|UNDNAME_NO_MS_KEYWORDS|0x0002|禁用 Microsoft 扩展关键字的扩展。|
|UNDNAME_NO_FUNCTION_RETURNS|0x0004|禁用主声明的返回类型的扩展。|
|UNDNAME_NO_ALLOCATION_MODEL|0x0008|禁用声明模型的扩展。|
|UNDNAME_NO_ALLOCATION_LANGUAGE|0x0010|禁用声明语言说明文字的扩展。|
|UNDNAME_RESERVED1|0x0020|已保留。|
|UNDNAME_RESERVED2|0x0040|已保留。|
|UNDNAME_NO_THISTYPE|0x0060|禁用类型上的所有 `this` 修饰符。|
|UNDNAME_NO_ACCESS_SPECIFIERS|0x0080|禁用成员的访问说明符的扩展。|
|UNDNAME_NO_THROW_SIGNATURES|0x0100|禁用函数和指向函数的指针的"throw-signatures"扩展。|
|UNDNAME_NO_MEMBER_TYPE|0x0200|禁用 或 `static` 成员的 `virtual` 扩展。|
|UNDNAME_NO_RETURN_UDT_MODEL|0x0400|禁用 UDT 返回的 Microsoft 模型的扩展。|
|UNDNAME_32_BIT_DECODE|0x0800|取消修饰 32 位修饰名。|
|UNDNAME_NAME_ONLY|0x1000|仅获取主声明的名称;仅返回 [scope：：]name。  展开模板参数。|
|UNDNAME_TYPE_ONLY|0x2000|输入只是一种类型编码;编写抽象声明符。|
|UNDNAME_HAVE_PARAMETERS|0x4000|可以使用实际模板参数。|
|UNDNAME_NO_ECSU|0x8000|取消枚举/class/struct/union。|
|UNDNAME_NO_IDENT_CHAR_CHECK|0x10000|禁止检查有效的标识符字符。|
|UNDNAME_NO_PTR64|0x20000|输出中不包括 ptr64。|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
