---
title: 生成 C# Equals 和 GetHashCode 方法重写
description: 了解如何使用“快速操作和重构”菜单生成 Equals 和 GetHashCode 方法。
ms.custom: SEO-VS-2020
ms.date: 03/08/2021
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- dotnet
ms.openlocfilehash: 36f26e9ecbbd77cac7967f09d241f19ae158a36f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736892"
---
# <a name="generate-equals-and-gethashcode-method-overrides-in-visual-studio"></a>在 Visual Studio 中生成 C# Equals 和 GetHashCode 方法重写

此代码生成适用于：

- C#

功能：让你生成 Equals 和 GetHashCode 方法。

适用情况：当具备的类型应按一个或多个字段进行比较，而不是按内存中的对象位置进行比较时，生成这些重写。

操作原因：

- 如果要实现值类型，则应考虑重写 Equals 方法。 这样做与 ValueType 上 Equals 方法的默认实现相比，可以获得更高的性能。

- 在实现引用类型时，如果类型看起来像基类型（如点、字符串和 BigNumber 等），请考虑重写 Equals 方法。

- 重写 GetHashCode 方法，使类型能在哈希表中正常工作。 了解有关[相等运算符](/dotnet/standard/design-guidelines/equality-operators)的更多指南。

## <a name="how-to"></a>操作说明

1. 将游标放在类型声明的行上。

    ```csharp
    public class ImaginaryNumber
    {
        public double RealNumber { get; set; }
        public double ImaginaryUnit { get; set; }
    }
    ```

   代码应如以下屏幕快照所示：

   ![要对其应用生成的方法的突出显示代码的屏幕截图](media/overrides-highlight-cs.png)

   > [!TIP]
   > 请勿双击选择类型名称，否则菜单选项将不可用。 只需将游标置于行上的某处。

1. 接下来，选择下列操作之一：

   - 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

   - 右键单击并选择“快速操作和重构”菜单。

   - 单击 ![Visual Studio 中快速操作螺丝刀图标的屏幕截图](../media/screwdriver-icon.png) 显示的螺丝刀图标。

1. 在下拉菜单中，选择“生成 Equals(object)”或“生成 Equals 和 GetHashCode” 。

   ![“生成重写”下拉菜单的屏幕截图](media/overrides-preview-cs.png)

1. 在“选取成员”对话框中，选择要为其生成方法的成员：

    ![生成重写对话框](media/overrides-dialog-cs.png)

    > [!TIP]
    > 也可以通过使用对话框底部附近的复选框，选择从此对话框中生成运算符。

   `Equals` 和 `GetHashCode` 方法是通过默认实现生成的，如以下代码所示：

    ```csharp
   public class ImaginaryNumber : IEquatable<ImaginaryNumber>
    {
        public double RealNumber { get; set; }
        public double ImaginaryUnit { get; set; }

        public override bool Equals(object obj)
        {
            return Equals(obj as ImaginaryNumber);
        }

        public bool Equals(ImaginaryNumber other)
        {
            return other != null &&
                   RealNumber == other.RealNumber &&
                   ImaginaryUnit == other.ImaginaryUnit;
        }

        public override int GetHashCode()
        {
            return HashCode.Combine(RealNumber, ImaginaryUnit);
        }
    }
    ```

   代码应如以下屏幕快照所示：

   ![生成的方法的结果的屏幕截图](media/overrides-result-cs.png)

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
