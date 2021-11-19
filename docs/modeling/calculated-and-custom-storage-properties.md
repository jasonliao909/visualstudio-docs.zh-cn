---
title: 计算的和自定义的存储属性
description: 了解如何在关系图上以及在你的语言资源管理器中向用户显示域特定语言 (DSL) 中的所有域属性。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126667491"
---
# <a name="calculated-and-custom-storage-properties"></a>计算的和自定义的存储属性
可以在关系图上以及在你的语言资源管理器中向用户显示域特定语言 (DSL) 中的所有域属性，并且可以通过程序代码进行访问。 但是，属性的存储方式与它们值的存储方式不同。

## <a name="kinds-of-domain-properties"></a>域属性的种类
 在 DSL 定义中，可以设置域属性的“种类”，如下表所示：

|域属性种类|说明|
|-|-|
|标准（默认值）|一种域属性，该属性保存在存储中并且会序列化为文件。|
|**Calculated**|一种只读域属性，该属性不保存在存储中，但它是通过其他值计算的。<br /><br /> 例如，可以通过 `Person.BirthDate` 计算 `Person.Age`。<br /><br /> 你需要提供执行计算的代码。 通常，需要通过其他域属性来计算值。 但是，也可以使用外部资源。|
|自定义存储|一种域属性，该属性不直接保存在存储中，但可以同时获取和设置该属性。<br /><br /> 你需要提供获取和设置值的方法。<br /><br /> 例如，`Person.FullAddress` 可以存储在 `Person.StreetAddress`、`Person.City` 和 `Person.PostalCode` 中。<br /><br /> 还可以访问外部资源，例如从数据库获取和设置值。<br /><br /> 当 `Store.InUndoRedoOrRollback` 为 true 时，你的代码不应在存储中设置值。 请参阅[事务和自定义资源库](#setters)。|

## <a name="providing-the-code-for-a-calculated-or-custom-storage-property"></a>为计算或自定义存储属性提供代码
 如果将某一域属性的“种类”设置为“计算”或“自定义存储”，那么你需要提供访问方法。 当你生成解决方案时，错误报告将告诉你所需的内容。

#### <a name="to-define-a-calculated-or-custom-storage-property"></a>定义计算或自定义存储属性

1. 在 DslDefinition.dsl 中，在关系图中或“DSL 资源管理器”中选择域属性。

2. 在“属性”窗口中，将“种类”字段设置为“计算”或“自定义存储”   。

     确保同时将它的“类型”设置为所需类型。

3. 在“解决方案资源管理器”的工具栏中，单击“转换所有模板” 。

4. 在“生成”菜单中，单击“生成解决方案”。

     你将收到以下错误消息：“YourClass 未包含 GetYourProperty 的定义” 

5. 双击此错误消息。

     随即会打开 Dsl\GeneratedCode\DomainClasses.cs 或 DomainRelationships.cs。 在突出显示的调用方法上方，注释会提示你提供 GetYourProperty() 的实现。

    > [!NOTE]
    > 此文件是通过 DslDefinition.dsl 生成的。 如果编辑此文件，在下次单击“转换所有模板”时，你所做的更改将丢失。 因此，请改为在单独的文件中添加所需方法。

6. 在单独的文件夹中创建或打开一个类文件，例如 CustomCode\\*YourDomainClass*.cs。

     确保命名空间与生成的代码中的命名空间相同。

7. 在此类文件中，编写域类的部分实现。 在类中，编写缺少的 `Get` 方法的定义，如以下示例所示：

    ```
    namespace Company.FamilyTree
    {  public partial class Person
       {  int GetAgeValue()
          { return System.DateTime.Today.Year - this.BirthYear; }
    }  }
    ```

8. 如果将“种类”设置为“自定义存储”，还需要提供 `Set` 方法 。 例如：

    ```
    void SetAgeValue(int value)
    { if (!Store.InUndoRedoOrRollback)
        this.BirthYear =
            System.DateTime.Today.Year - value; }
    ```

     当 `Store.InUndoRedoOrRollback` 为 true 时，你的代码不应在存储中设置值。 请参阅[事务和自定义资源库](#setters)。

9. 生成并运行解决方案。

10. 测试属性。 请确保尝试进行“撤消”和“恢复” 。

## <a name="transactions-and-custom-setters"></a><a name="setters"></a> 事务和自定义资源库
 在“自定义存储”属性的 Set 方法中，无需打开事务，因为方法通常是在活动事务内调用的。

 但是，如果用户调用“撤消”和“恢复”，或者如果正在回滚事务，也可能会调用 Set 方法。 当 <xref:Microsoft.VisualStudio.Modeling.Store.InUndoRedoOrRollback%2A> 为 true 时，Set 方法的行为应如下所示：

- 它不应在存储中进行更改，例如将值分配给其他域属性。 撤消管理器将设置它们的值。

- 但是，它应对任何外部资源进行更新，例如存储外部的数据库或文件内容，或对象。 这将确保它们与存储中的值保持同步。

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

 有关事务的详细信息，请参阅[在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

## <a name="see-also"></a>另请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [域属性的属性](../modeling/properties-of-domain-properties.md)
- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)
