---
description: 初始化 span 类的新实例。
title: span::span 构造函数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: a1f3a073caa56dba1bc680a1e2205a7be0448f44
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122157275"
---
# <a name="spanspan-constructor"></a>span::span 构造函数

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
