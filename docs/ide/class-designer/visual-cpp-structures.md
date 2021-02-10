---
title: 类设计器中的 C++ 结构
description: 了解类设计器如何支持使用关键字 struct 声明的 C++ 结构。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Class Designer [Visual Studio], structures
ms.assetid: bad18ab6-d956-47a6-a413-811cc26db5f5
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- cplusplus
ms.openlocfilehash: 3ca35f9e1c3c1340330ddbbe36ede540fe1e547d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99879951"
---
# <a name="c-structures-in-class-designer"></a>类设计器中的 C++ 结构

类设计器支持使用关键字 `struct` 声明的 C++ 结构。 下面是一个示例：

```cpp
struct MyStructure
{
   char a;
   int i;
   long j;
};
```

若要详细了解如何使用 `struct` 类型，请参阅 [struct](/cpp/cpp/struct-cpp)。

类图中的 C++ 结构形状的外观和运行方式都与类形状相似，不同之处在于它的标签名为 **Struct**，且为方角（而不是圆角）。

|Code 元素|类设计器视图|
|------------------| - |
|`struct StructureName {};`|**StructureName**<br /><br /> 结构|

## <a name="see-also"></a>另请参阅

- [使用 C++ 代码](working-with-visual-cpp-code.md)
- [类和结构](/cpp/cpp/classes-and-structs-cpp)
- [struct](/cpp/cpp/struct-cpp)
