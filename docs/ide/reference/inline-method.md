---
title: 内联方法
description: 了解如何使用 Visual Studio 中的“快速操作和重构”菜单，重构内联方法声明并提供更清晰的语法。
ms.date: 11/03/2020
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
ms.openlocfilehash: 2c474c43451006121f940da5eed66dfb9277806a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122101201"
---
# <a name="inline-method"></a>内联方法

此重构适用于：

- C#

- Visual Basic

**功能：** 内联方法重构。 

**使用时机：** 要将单个语句中对静态、实例和扩展方法的使用替换为删除原始方法声明的选项。

操作原因：此重构会提供更清晰的语法。

## <a name="how-to"></a>操作说明

1. 将脱字号放在方法使用上。

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

3. 选择以下选项之一： 
    
   选择“内联 `<QualifiedMethodName>`”，删除内联方法声明：

    ![Visual Studio 中“快速操作和重构”菜单的屏幕截图，其中选中了“转换‘内联 CreateWidget()’”，并显示了 C# 代码更改。](media/inline-method-remove-declaration.png)

   选择“内联并保留 `<QualifiedMethodName>`”，保留原始方法声明：

    ![Visual Studio 中“快速操作和重构”菜单的屏幕截图，其中选中了“转换‘内联并保留 CreateWidget()’”，并显示了 C# 代码更改。](media/inline-method-preserve-declaration.png)

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
