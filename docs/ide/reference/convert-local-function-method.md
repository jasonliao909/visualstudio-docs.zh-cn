---
title: 将本地函数转换为方法
description: 了解如何使用“快速操作和重构”菜单将本地函数转换为方法。
ms.custom: SEO-VS-2020
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 3cecafe64f7ead8157a9cb6c80d2f0a245566390
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99919720"
---
# <a name="convert-a-local-function-to-a-method"></a>将本地函数转换为方法

此重构适用于：

- C#

**功能：** 将本地函数转换为方法。

**使用时机：** 需要在当前本地上下文之外定义一个本地函数。

操作原因：需要将本地函数转换为方法，以便可以在本地上下文之外调用它。 本地函数变得太长时，可能需要将其转换为方法。 在单独的方法中定义函数时，代码更易于阅读。

## <a name="convert-local-function-to-method-refactoring"></a>将本地函数转换为方法重构

1. 将光标置于本地函数中。

    ![将本地函数转换为方法代码示例](media/convert-local-function-to-method.png)

2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。

    ![将本地函数转换为方法代码修补程序示例](media/convert-local-function-to-method-codefix.png)

2. 按 Enter 接受重构。

    ![将本地函数转换为方法结果示例](media/convert-local-function-to-method-result.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
- [针对 .NET 开发人员的提示](../csharp-developer-productivity.md)
