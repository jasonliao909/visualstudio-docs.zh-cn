---
title: 将匿名类型转换为元组
description: 了解如何在 Visual Studio 中使用“快速操作和重构”菜单将匿名类型转换为元组。
ms.custom: SEO-VS-2020
ms.date: 04/05/2022
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
ms.openlocfilehash: 17e692da97281a4df0ae73899b94bc3637189a55
ms.sourcegitcommit: 8623082339d642f30efe98e4a759b8f023a210cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2022
ms.locfileid: "141489134"
---
# <a name="convert-anonymous-type-to-tuple"></a>将匿名类型转换为元组

此重构适用于：

- C#

- Visual Basic

**功能：** 将匿名类型转换为元组。

**使用时机：** 有符合元组资格的匿名类型。

操作原因：[元组](/dotnet/csharp/tuples)有助于保持语法轻量级。 此快速操作可以更容易地利用此 C# 功能。

## <a name="how-to"></a>操作说明

1. 请将光标放置在匿名类型中。
2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。

   ![将匿名类型转换为元组](media/convert-anon-to-tuple.png)

2. 按 Enter 接受重构。

   ![将匿名类型转换为接受的元组](media/convert-anon-to-tuple-complete.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
