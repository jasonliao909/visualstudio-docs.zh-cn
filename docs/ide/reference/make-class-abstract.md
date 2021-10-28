---
title: 将类变为抽象
description: 了解如何使类在编写抽象方法之后抽象化。
ms.date: 11/03/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 767a81ae1957a7a3c2865bef060f5f0016e7a7c2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641778"
---
# <a name="make-class-abstract"></a>将类变为抽象

此重构适用于：

- C#

- Visual Basic

**功能：** 进行类抽象重构。

**使用时机：** 在非抽象类中编写抽象方法。

操作原因：让代码修补程序使类在编写抽象方法之后抽象化会节省时间。

## <a name="how-to"></a>操作说明

1. 将脱字号放置在抽象方法上。

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

3. 选择“将类变为‘抽象’”。

    ![将类变为抽象](media/make-class-abstract.png)

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
