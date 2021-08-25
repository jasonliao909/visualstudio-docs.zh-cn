---
title: “将类型移到匹配的文件”重构
description: 将某个类型移动到具有相同名称的单独文件。 右键单击该类型，选择“快速操作和重构”，然后选择“将类型移动到 <TypeName>.cs”。
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: aab621ab68d90b44e1132ddbafeb69db57af209b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122117327"
---
# <a name="move-a-type-to-a-matching-file-refactoring"></a>“将类型移到匹配的文件”重构

此重构适用于：

- C#

- Visual Basic

功能：移动选定的类型到具有相同名称的单独文件。

时机：在想要分开的相同文件中有多个类、结构和接口等时。

原因：将多个类型置于相同的文件会使查找这些类型变得困难。 通过将类型移动到具有相同名称的文件，代码变得更具可读性且更易于导航。

## <a name="how-to"></a>操作方法

1. 将光标置于定义类型的类型名称中。 例如：

   ```csharp
   class Person
   ```

   ```vb
   Class Person
   ```

2. 接下来，执行以下操作之一：

   - 按“Ctrl”+ **。**
   - 右键单击类型名称，并选择“快速操作和重构”

1. 选择菜单中的“将类型移到 TypeName.cs”****，其中“TypeName”是选定类型的名称。

   此时，类型会移到项目中与它同名的文件中。

   - C#：

      ![内联结果 - C#](media/movetype-result-cs.png)

   - Visual Basic：

      ![内联结果 - Visual Basic](media/movetype-result-vb.png)

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
