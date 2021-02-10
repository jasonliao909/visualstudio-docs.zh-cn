---
title: 将类变为抽象
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
ms.openlocfilehash: 7b44c8331c10bc0cf2f87e19094a77c0cbec251a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99919416"
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
