---
title: 使用 new()
description: 了解如何在不能使用 `var` 时使用 `new()`。
ms.date: 11/03/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 2c1455d92501ee50bca84e655b83ca98435e2d47
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122061870"
---
# <a name="use-new"></a>使用 `new()`

这适用于：

- C#

**功能：** 请使用 `new()`。

**使用时机：** 字段无法使用 `var` 或代码样式首选项以便不使用 `var`。

操作原因：因此，无需重复键入两次类型来编写重复代码。

## <a name="how-to"></a>操作说明

1. 将脱字号置于字段声明上。

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

3. 选择“使用 ‘new(…)’”：

    ![使用 'new(...)'](media/use-new.png)

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
