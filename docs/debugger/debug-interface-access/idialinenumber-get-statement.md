---
description: 检索一个标志，该标志指示此行信息描述程序源中的语句（而不是表达式）的开头。
title: IDiaLineNumber：：get_statement |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_statement method
ms.assetid: 22b8ee29-79ef-427f-bd05-00d255ab836b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 1af9fd6462f668e23d2a24d6d7db4939322a30e4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832048"
---
# <a name="idialinenumberget_statement"></a>IDiaLineNumber::get_statement
检索一个标志，该标志指示此行信息描述程序源中的语句（而不是表达式）的开头。

## <a name="syntax"></a>语法

```C++
HRESULT get_statement ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]如果 `TRUE` 此行信息描述程序源中语句的开头，则返回 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果 `S_FALSE` 不支持此属性，则返回 。 否则，返回错误代码。

## <a name="remarks"></a>备注
 语句可以跨多行。 此方法指示关联的行号是否标记此类多行语句的开头。

## <a name="see-also"></a>另请参阅
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
