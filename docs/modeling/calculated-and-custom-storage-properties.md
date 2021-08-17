---
title: 计算的和自定义的存储属性
description: 了解如何在关系图和语言资源管理器中向用户 (DSL) 域特定语言的所有域属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain properties
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 5a112d515b66262b5981bec8560a83207c5dd38a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122055596"
---
# <a name="calculated-and-custom-storage-properties"></a>计算的和自定义的存储属性
DSL (域特定语言) 属性都可以在关系图和语言资源管理器中向用户显示，并且可以通过程序代码访问。 但是，属性在存储其值的方式上有所不同。

## <a name="kinds-of-domain-properties"></a>域属性类型
 在 DSL 定义中，可以设置 **域属性的"** 种类"，如下表所列：

|域属性类型|说明|
|-|-|
|**标准** (默认) |一个域属性，该属性保存在 *存储中* 并序列化为文件。|
|**Calculated**|一个只读域属性，不保存在存储中，但根据其他值计算。<br /><br /> 例如， `Person.Age` 可以通过 进行计算 `Person.BirthDate` 。<br /><br /> 必须提供执行计算的代码。 通常，从其他域属性计算值。 但是，也可使用外部资源。|
|**自定义存储**|一个域属性，该属性不直接保存在存储中，但可以同时获取和设置。<br /><br /> 必须提供获取和设置值的方法。<br /><br /> 例如， `Person.FullAddress` 可以存储在 、 `Person.StreetAddress` `Person.City` 和 中 `Person.PostalCode` 。<br /><br /> 还可以访问外部资源，例如从数据库获取和设置值。<br /><br /> 如果 为 true，则代码不应在 `Store.InUndoRedoOrRollback` 存储区中设置值。 请参阅[事务和自定义 Setter。](#setters)|

## <a name="providing-the-code-for-a-calculated-or-custom-storage-property"></a>为计算或自定义存储属性提供代码
 如果将"域类型"属性设置为"计算"或"自定义存储，必须提供访问方法。 生成解决方案时，错误报告将告诉你所需的内容。

#### <a name="to-define-a-calculated-or-custom-storage-property"></a>定义计算属性或自定义存储属性

1. 在 DslDefinition.dsl 中，选择关系图或 DSL 资源管理器 中的 **域属性**。

2. 在"**属性"** 窗口中，将"**种类**"字段设置为 **"计算**"或 **"自定义存储"。**

     请确保还将"类型" **设置为** 想要的类型。

3. 在 **的工具栏中单击** "转换所有 **模板** 解决方案资源管理器" 。

4. 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

     收到以下错误消息 *："YourClass* 不包含 Get *YourProperty* 的定义。"

5. 双击错误消息。

     Dsl\GeneratedCode\DomainClasses.cs 或 DomainRelationships.cs 将打开。 在突出显示的方法调用上方，注释会提示你提供 Get *YourProperty* () 。

    > [!NOTE]
    > 此文件从 DslDefinition.dsl 生成。 如果编辑此文件，则下次单击"转换所有模板"时 **，所做的更改将丢失**。 相反，在单独的文件中添加所需的方法。

6. 在单独的文件夹中创建或打开类文件，例如 CustomCode \\ *YourDomainClass*.cs。

     请确保命名空间与生成的代码中的 命名空间相同。

7. 在 类文件中，编写域类的部分实现。 在 类中，为缺少的方法编写类似于以下示例 `Get` 的定义：

    ```
    namespace Company.FamilyTree
    {  public partial class Person
       {  int GetAgeValue()
          { return System.DateTime.Today.Year - this.BirthYear; }
    }  }
    ```

8. 如果将 Kind **设置为** **Custom 存储，** 则还必须提供 `Set` 方法。 例如：

    ```
    void SetAgeValue(int value)
    { if (!Store.InUndoRedoOrRollback)
        this.BirthYear =
            System.DateTime.Today.Year - value; }
    ```

     如果 为 true，则代码不应在 `Store.InUndoRedoOrRollback` 存储区中设置值。 请参阅[事务和自定义 Setter。](#setters)

9. 生成并运行解决方案。

10. 测试 属性。 请确保尝试"撤消 **"和**"**重做"。**

## <a name="transactions-and-custom-setters"></a><a name="setters"></a> 事务和自定义 Setter
 在 Custom 存储 属性的 Set 方法中，不需要打开事务，因为方法通常在活动事务内调用。

 但是，如果用户调用 Undo 或 Redo，或者正在回滚事务，则也可以调用 Set 方法。 当 <xref:Microsoft.VisualStudio.Modeling.Store.InUndoRedoOrRollback%2A> 为 true 时，Set 方法的行为应如下所示：

- 它不应在存储区中进行更改，例如将值分配给其他域属性。 撤消管理器将设置其值。

- 但是，它应更新任何外部资源，例如数据库或文件内容，或存储外部的对象。 这将确保它们与存储中的值保持同步。

  例如：

```
void SetAgeValue(int value)
{
  // If we are in Undo, no changes to Store objects:
  if (!this.Store.InUndoRedoOrRollback)
  {
    this.BirthYear = System.DateTime.Today.Year - value;
  }
  // But always update external objects:
  System.IO.File.WriteAllText(AgeFile, value);
}
```

 有关事务详细信息，请参阅在程序代码中 [导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

## <a name="see-also"></a>请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [域属性的属性](../modeling/properties-of-domain-properties.md)
- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)
