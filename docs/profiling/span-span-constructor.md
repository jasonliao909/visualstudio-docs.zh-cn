---
description: 初始化 span 类的新实例。
title: span::span 构造函数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::span::span
helpviewer_keywords:
- Concurrency::diagnostic::span constructor
ms.assetid: 8b5578aa-5e5c-4ac7-87c7-ce87c4246e2c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 2aabbb6716f0044b7ab1da4529adbc26df4a622d
ms.sourcegitcommit: caf5ca17efde4dc4de8b1bdfbe7770f6d705024d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2022
ms.locfileid: "145017824"
---
# <a name="spanspan-constructor"></a>span::span 构造函数

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

初始化 `span` 类的新实例。

## <a name="syntax"></a>语法

```cpp
span(
   const marker_series& _Series,
   _In_ LPCTSTR _Format,
   ...
);
span(
   const marker_series& _Series,
   marker_importance _Importance,
   _In_ LPCTSTR _Format,
   ...
);
span(
   const marker_series& _Series,
   int _Category,
   _In_ LPCTSTR _Format,
   ...
);
span(
   const marker_series& _Series,
   marker_importance _Importance,
   int _Category,
   _In_ LPCTSTR _Format,
   ...
);
```

#### <a name="parameters"></a>参数

`_Series` 有效标记系列上下文。

`_Format` 一个复合格式字符串，其中包含与零个或多个格式项混合的文本，这些格式项对应于参数列表中的对象。

`_Importance` 重要性级别。

`_Category` 类别。

## <a name="requirements"></a>要求

**标头：cvmarkersobj.h** 

**命名空间：** Concurrency::diagnostic

## <a name="see-also"></a>另请参阅

- [span 类](../profiling/span-class.md)
