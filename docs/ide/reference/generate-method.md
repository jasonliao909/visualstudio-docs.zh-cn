---
title: 生成方法
description: 了解如何使用“快速操作和重构”菜单快速地将方法添加到类。
ms.custom: SEO-VS-2020
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- dotnet
ms.openlocfilehash: 21d77611c621eca9a20f467a012395d5d509aa9f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122123900"
---
# <a name="generate-a-method-in-visual-studio"></a>在 Visual Studio 中生成方法

此代码生成适用于：

- C#

- Visual Basic

功能：将方法快速添加到类。

时机：想要引入新方法，并想要自动以适当的方式声明它时。

原因：可以在使用该方法和参数之前对其进行声明，但此功能可自动生成声明。

## <a name="how-to"></a>操作说明

1. 将光标置于红色波浪线上。 红色波浪线表示尚无任何方法。

   - C#：

       ![突出显示的代码 C#](media/method-highlight-cs.png)

   - Visual Basic：

       ![突出显示的代码 VB](media/method-highlight-vb.png)

2. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”  + **。** 触发“快速操作和重构”菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单。
      - 将鼠标悬停在红色波形曲线上，然后单击出现的 ![错误灯泡](media/error-bulb.png) 图标。
      - 单击 ![错误灯泡](media/error-bulb.png) 图标（如果文本光标已在具有红色波形曲线的行上，它会出现在左边缘）。

      ![生成方法预览](media/method-preview-cs.png)

3. 从下拉菜单中选择“生成方法”。

   > [!TIP]
   > 进行选择前，使用预览窗口底部的“预览更改”链接[查看将发生的所有更改](../../ide/preview-changes.md)。

   使用从其用法推断出的任意参数创建此方法。

   - C#：

       ![“生成方法”的结果 C#](media/method-result-cs.png)

   - Visual Basic：

       ![“生成方法”的结果 VB](media/method-result-vb.png)

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
