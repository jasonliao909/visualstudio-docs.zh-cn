---
title: 生成类或类型
description: 了解如何使用“快速操作和重构”菜单快速生成类或类型的代码。
ms.custom: SEO-VS-2020
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
f1_keywords:
- vsl.GenerateFromUsage
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 3af7bb3f8a52029c0b9e11df802b8f4788711af0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126644405"
---
# <a name="generate-a-class-or-type-in-visual-studio"></a>在 Visual Studio 中生成类或类型

此代码生成适用于：

- C#

- Visual Basic

功能：立即生成类或类型的代码。

时机：引入一个新类或类型，并想要自动以适当的方式声明它时。

原因：可以在使用类或类型前对其进行声明，但此功能将自动生成类或类型。

## <a name="how-to"></a>操作说明

1. 将光标置于红色波浪线上。 红色波浪线表示尚无任何类。

   - C#：

       ![突出显示的代码 C#](media/class-highlight-cs.png)

   - Visual Basic：

       ![突出显示的代码 VB](media/class-highlight-vb.png)

2. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单。
      - 将鼠标悬停在红色波形曲线上，然后单击出现的 ![错误灯泡](media/error-bulb.png) 图标。
      - 单击 ![错误灯泡](media/error-bulb.png) 图标（如果文本光标已在具有红色波形曲线的行上，它会出现在左边缘）。

      ![生成类预览](media/class-preview-cs.png)

3. 可从下拉菜单中选择一种选项：

   - 在新文件中生成“TypeName”类&mdash;在名为 *TypeName*.cs/.vb 的文件中创建名为 TypeName 的类
   - 创建“TypeName”类&mdash;在当前文件创建名为 TypeName 的类 。
   - 创建“TypeName”嵌套类&mdash;在当前类的内部创建名为 TypeName 的嵌套类 。
   - 创建新类...&mdash;使用所指定的所有属性创建新类或结构。

   > [!TIP]
   > 进行选择前，使用预览窗口底部的“预览更改”链接[查看将发生的所有更改](../../ide/preview-changes.md)。

4. 如果选择的是“生成新类型”项，则打开“生成类型”对话框 。 配置新类型的可访问性、类型和位置。

   ![生成类型](media/class-newtype-cs.png)

   选择 | 说明
   --- | ---
   Access | 将类型设置为具有“默认”、“内部”或“公共”访问权限。
   类型 | 这可被设置为“类”或“结构”。
   名称 | 无法对此进行更改，将使用已键入的名称。
   Project | 如果在你的解决方案中有多个项目，可以选择想要设置类/结构所在的位置。
   文件名 | 可以创建一个新文件，或将该类型添加到现有文件。

已创建类或结构。 对于 C#，还会创建一个构造函数。

- C#

   ![生成类结果 C#](media/class-result-cs.png)

- Visual Basic

   ![生成类结果 VB](media/class-result-vb.png)

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
