---
title: 将 Switch 语句转换为 Switch 表达式
description: 了解如何使用“快速操作和重构”菜单将 switch 语句转换为 C# 8.0 switch 表达式。
ms.custom: SEO-VS-2020
ms.date: 06/19/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: b7d01862774fd36bc5c9347df3fce6bd02c56263
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122094147"
---
# <a name="convert-switch-statement-to-switch-expression"></a>将 Switch 语句转换为 Switch 表达式

此重构适用于：

- C#

**功能：** 将 [Switch 语句](/dotnet/csharp/language-reference/keywords/switch)转换为 C# 8.0 [Switch 表达式](/dotnet/csharp/whats-new/csharp-8#switch-expressions)。

**使用时机：** 想要将 `switch` 语句转换为 `switch` 表达式，反之亦然。 

操作原因：若仅在使用表达式，可以通过此重构轻松地实现传统 `switch` 语句的转换。

## <a name="how-to"></a>操作说明

1. 在项目文件中[将语言版本设置为预览版](/dotnet/csharp/language-reference/configure-language-version#edit-the-project-file)，因为 `switch` 表达式是新的 C# 8.0 功能。
2. 请将光标置于 `switch` 关键字，并按“Ctrl+.” 。 触发“快速操作和重构”  菜单。
3. 选择“将 Switch 语句转换为表达式”。

   ![将 Switch 语句转换为 Switch 表达式](media/convert-switch-statement-to-switch-expression.png) 

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
