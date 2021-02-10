---
title: 为结构生成 IEquatable 运算符
description: 了解如何使用“快速操作和重构”菜单为结构生成 Equals 和 IEquatable 运算符。
ms.custom: SEO-VS-2020
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 05792636e1094c53869f0235145aec73b26deea9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99952975"
---
# <a name="generate-iequatable-operators-when-generating-equals-for-structs"></a>在为结构生成 Equals 时生成 IEquatable 运算符

此代码生成适用于：

- C#

**功能：** 可便于为 [结构](/dotnet/csharp/language-reference/builtin-types/struct)生成 Equals 和 IEquatable 运算符。

**使用时机：** 你有一个结构，我们会为你自动添加 IEquatable 以及 Equals 和 Not Equals 运算符。

操作原因：

- 如果实现值类型，则应考虑重写 Equals 方法，针对 Equals 方法在 ValueType 上的默认实现提升相关性能。

- 实现 IEquatable 接口实现了特定于类型的 Equals() 方法。

## <a name="how-to"></a>操作说明

1. 将光标置于结构声明行上的某个位置。

2. 接下来，执行以下操作之一：

   - 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

   - 右键单击并选择“快速操作和重构”菜单。

   - 单击 ![左边缘中](../media/screwdriver-icon.png) 显示的螺丝刀图标。

   ![为结构生成 IEquatable 和 Equals](media/generate-equals-structs.png)

3. 在下拉菜单中，选择“生成 Equals(object)”。

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)