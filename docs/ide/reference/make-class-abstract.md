---
title: 将类变为抽象
description: 了解如何使类在编写抽象方法之后抽象化。
ms.date: 11/03/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: ac3d6b9cef8d20d85049da830dfb830321faab75
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214533"
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
