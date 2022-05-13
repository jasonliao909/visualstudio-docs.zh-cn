---
title: span 类 | Microsoft Docs
description: 了解 span 类及其如何定义应用程序阶段。 还将了解 span 类公共构造函数和继承层次结构。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::span
helpviewer_keywords:
- Concurrency::diagnostic::span class
ms.assetid: 527826a8-2590-43ad-b907-7bc0b7288e92
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 8eba44f0858afb7a37874ffc8d9c544f86c7e4e5
ms.sourcegitcommit: caf5ca17efde4dc4de8b1bdfbe7770f6d705024d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2022
ms.locfileid: "145017733"
---
# <a name="span-class"></a>span 类

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]
定义应用程序的一个阶段。

## <a name="syntax"></a>语法

```cpp
class span;
```

## <a name="members"></a>成员

### <a name="public-constructors"></a>公共构造函数

|名称|说明|
|----------|-----------------|
|[span::span 构造函数](../profiling/span-span-constructor.md)|初始化 `span` 类的新实例。|
|[span::~span 析构函数](../profiling/span-tilde-span-destructor.md)|销毁 `span` 对象并释放其资源。|

## <a name="inheritance-hierarchy"></a>继承层次结构
 `span`

## <a name="requirements"></a>要求
 **标头：cvmarkersobj.h** 

 **命名空间：** Concurrency::diagnostic

## <a name="see-also"></a>另请参阅
- [diagnostic 命名空间](../profiling/diagnostic-namespace.md)