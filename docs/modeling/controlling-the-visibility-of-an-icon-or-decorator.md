---
title: 控制图标或修饰器的可见性
description: 了解如何控制图标或修饰器的可见性，具体视模型中的属性状态而定。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 54dd15b59628883d42f28ab9988ae75d0c7bbd52
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665038"
---
# <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>控制图标或修饰器的可见性
修饰器是显示在域特定语言 (DSL) 中的形状上的图标或文本行。 你可以根据模型中的属性状态来让修饰器显示和消失。 例如，在表示一个“人”的形状上，你可以根据这个人的性别、子女数等来显示不同的图标。

## <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>控制图标或修饰器的可见性
 以下过程假设你已定义了一个形状以及它到域类的映射。 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。

#### <a name="to-control-the-visibility-of-an-icon-or-text-decorator"></a>控制图标或修饰器的可见性

1. 在 DSL 定义关系图中，向形状类添加要显示的图标或文本修饰器。

   1. 右键单击形状类，指向“添加”，然后单击所需的修饰器类型。

   2. 设置修饰器的“位置”属性。 可以为多个修饰器设置相同的位置。 例如，可以让男性和女性的图标共享同一个位置。

   3. 设置图标修饰器的“默认图标”属性。

2. 选择关系图元素映射，它是 DSL 定义关系图上形状类和域类之间的灰色线条。

3. 在“DSL 详细信息”窗口中，在“修饰器映射”选项卡中，选择修饰器。 例如 MaleDecorator。

4. 选中“可见性筛选器”框。

5. 如果应控制可见性的域属性位于直接域类上，请将“筛选器属性的路径”留空。

    否则，请单击下拉菜单，并导航到属性所在的关系或类。

   - 若要避免错误报告，不应在导航工具中导航到带有“*”标记的关系。

6. 将“筛选器属性”设置为域属性。 例如“性别”。

7. 在“可见性条目”列表中，添加应显示修饰器的此域属性的值。 例如“男性”。

8. 针对每个图标重复上述步骤。

9. 转换所有模板、生成并运行，并打开测试关系图。

10. 当你更改控制属性值时，修饰器应显示并消失。

    通常，你希望使用更复杂的公式来控制可见性，而不是使用简单的值集。 例如，想要使图标依赖于特定类型的链接数，或者想使图标依赖于某个数字是否在特定范围内。 在这种情况下，请按以下过程进行操作。

#### <a name="to-control-the-visibility-of-a-decorator-based-on-a-formula"></a>基于公式控制修饰器的可见性

1. 向域类添加计算域属性。 在“属性”窗口中，设置以下值：

     IsBrowsable =  `False`  - 这将向用户隐藏属性 

     种类 =  `Calculated`  - 这意味着你需要提供计算其值的代码 

     名称：例如 DecoratorControl 

     类型 = `Boolean`

     有关详细信息，请参阅[计算和自定义存储属性](../modeling/calculated-and-custom-storage-properties.md)。

2. 使新属性控制修饰器的可见性。

    1. 选择关系图元素映射，它是从域类到形状的灰色线条。 在“DSL 详细信息”窗口中，打开“修饰器映射”选项卡 。

    2. 选中“可见性筛选器”框。

    3. 在“筛选器属性”中，选择控制属性“DecoratorControl” 。

    4. 在“可见性条目”下，输入 `True`。

3. 在“解决方案资源管理器”工具栏中，单击“转换所有模板” 。

4. 在“生成”菜单上，单击“生成解决方案” 。

5. 双击出现的错误报告：“YourClass 未包含 GetDecoratorControlValue 的定义 ...”。

     文本编辑器随即将在 Dsl\GeneratedCode\DomainClasses.cs 上打开。 突出显示的错误上方是要求你添加方法的注释。

6. 请注意缺少的命名空间、类和方法。  例如 Company.FamilyTree.Person.GetDecoratorControlValue()。

7. 在单独的代码文件中，编写包含缺少的方法的分部类定义。 例如：

    ```
    namespace Company.FamilyTree
    { partial class Person
      { bool GetDecoratorControlValue()
        {
          return this.Children.Count > 0;
    } } }
    ```

     有关使用程序代码自定义模型的详细信息，请参阅[在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

8. 重新生成并运行解决方案。

## <a name="see-also"></a>另请参阅

- [定义形状和连接线](../modeling/defining-shapes-and-connectors.md)
- [在图表上设置背景图像](../modeling/setting-a-background-image-on-a-diagram.md)
- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)