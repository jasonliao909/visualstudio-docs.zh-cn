---
description: 检索源列表，该列表已由属性提供程序或编译过程的其他组件放入符号存储区中。
title: IDiaSession::findInjectedSource | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findInjectedSource method
ms.assetid: 907531b6-1ef8-4153-986d-b72611a1632d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 4e7e6aeec300aaf8941fa0d3ac28ddce7ace8de4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831918"
---
# <a name="idiasessionfindinjectedsource"></a>IDiaSession::findInjectedSource
检索源列表，该列表已由属性提供程序或编译过程的其他组件放入符号存储区中。

## <a name="syntax"></a>语法

```C++
HRESULT findInjectedSource ( 
   LPCOLESTR                 srcFile,
   IDiaEnumInjectedSources** ppResult
);
```

#### <a name="parameters"></a>参数
 srcFile

[in] 要搜索的源文件的名称。

 ppResult

[out] 返回包含所有注入源的列表的 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
