---
title: 为 IComparable 生成比较运算符
ms.custom: SEO-VS-2020
description: 为了提高性能，为实现 IComparable 的类型生成比较运算符。
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- dotnet
ms.openlocfilehash: b0a2c2e532258594834d73c091314451f8b2cd3f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126644403"
---
# <a name="generate-comparison-operators-for-types-that-implement-icomparable"></a>为实现 IComparable 的类型生成比较运算符

此代码生成适用于：

- C#

**功能：** 让你能够为实现 IComparable 的类型生成比较运算符。

**使用时机：** 如果你有一个实现 IComparable 的类型，我们将自动添加比较运算符。

操作原因：如果实现值类型，则应考虑重写 Equals 方法，针对 Equals 方法在 ValueType 上的默认实现提升相关性能。

## <a name="how-to"></a>操作说明

1. 将光标置于类内部或 IComparable 关键字上。

2. 接下来，执行以下操作之一：

   - 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

   - 右键单击并选择“快速操作和重构”菜单。

   - 单击 ![左边缘中](../media/screwdriver-icon.png) 显示的螺丝刀图标。

   ![生成比较运算符](media/generate-comparison-operators.png)

3. 从下拉菜单中选择“生成 Equals(object)”。

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
