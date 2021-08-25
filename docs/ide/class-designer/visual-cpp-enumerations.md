---
title: 类设计器中的 C++ 枚举
description: 了解类设计器如何支持 C++ 枚举和区分范围的枚举类类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Class Designer [Visual Studio], enumerations
ms.assetid: 11e90ba1-18cd-44f8-9e26-e3746a7a19d1
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- cplusplus
ms.openlocfilehash: b4ab0dc47f9113e17b36617b432df1ffe5f0153e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122109495"
---
# <a name="c-enumerations-in-class-designer"></a>类设计器中的 C++ 枚举

类设计器支持 C++ `enum` 和域化的 `enum class` 类型。 下面是一个示例：

```cpp
enum CardSuit {
   Diamonds = 1,
   Hearts = 2,
   Clubs = 3,
   Spades = 4
};

// or...
enum class CardSuit {
   Diamonds = 1,
   Hearts = 2,
   Clubs = 3,
   Spades = 4
};
```

类图中的 C++ 枚举形状的外观和工作原理与结构形状类似，只不过其标签显示为 **Enum** 或 **Enum class**，标签的颜色为粉色而不是蓝色，并且具有带颜色的边框左边和上边。 两种枚举形状和结构形状都具有方角。

有关使用 `enum` 类型的更多信息，请参阅[枚举](/cpp/cpp/enumerations-cpp)。

## <a name="see-also"></a>另请参阅

- [使用 C++ 代码](working-with-visual-cpp-code.md)
- [枚举](/cpp/cpp/enumerations-cpp)
