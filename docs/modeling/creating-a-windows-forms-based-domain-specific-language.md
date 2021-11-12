---
title: 创建基于 Windows 窗体的域特定语言
description: 提供有关如何使用 Windows 窗体显示域特定语言模型的状态的信息。
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: 3355a84d34e297bb7394ca0e0feb8c3e635f615b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665032"
---
# <a name="create-a-windows-forms-based-domain-specific-language"></a>创建基于 Windows 窗体的域特定语言

可使用 Windows 窗体（而不是使用 DSL 关系图）来显示域特定语言 (DSL) 模型的状态。 本主题介绍如何使用 Visual Studio 可视化和建模 SDK 将 Windows 窗体绑定到 DSL。

下图显示了 Windows 窗体 UI 和 DSL 实例的模型资源管理器：

![Visual Studio 中的 DSL 实例](../modeling/media/dsl-wpf-2.png)

## <a name="create-a-windows-forms-dsl"></a>创建 Windows 窗体 DSL

“最小 WinForm 设计器”DSL 模板创建一个最小 DSL，你可以修改该 DSL 以满足自己的要求。

1. 使用“最小 WinForm 设计器”模板创建 DSL。

    本演练假定以下名称：

    - 解决方案和 DSL 名称：`FarmApp`
    - 命名空间：`Company.FarmApp`

2. 试验模板提供的初始示例：

   1. 转换所有模板。

   2. 生成并运行示例 (Ctrl+F5) 。

   3. 在 Visual Studio 实验实例中，打开调试项目中的 `Sample` 文件。

        请注意，它显示在 Windows 窗体控件中。

        还可查看显示在资源管理器中的模型的元素。

        在窗体或资源管理器中添加一些元素，并请注意，它们显示在另一个显示中。

   在 Visual Studio 的主实例中，请注意有关 DSL 解决方案的以下几点：

- `DslDefinition.dsl` 不包含关系图元素。 这是因为不会使用 DSL 关系图来查看此 DSL 的实例模型。 相反，需要将 Windows 窗体绑定到模型，窗体上的元素将显示模型。

- 除 `Dsl` 和 `DslPackage` 项目外，解决方案还包含名为 `UI.` 的第三个项目。UI 项目包含 Windows 窗体控件的定义。 `DslPackage` 依赖于 `UI`，`UI` 依赖于 `Dsl`。

- 在 `DslPackage` 项目中，`UI\DocView.cs` 包含显示在 `UI` 项目中定义的 Windows 窗体控件的代码。

- `UI` 项目包含绑定到 DSL 的窗体控件的工作示例。 但是，在你更改 DSL 定义后，它将不起作用。 `UI` 项目包含：

  - 名为 `ModelViewControl` 的 Windows 窗体类。

  - 名为 `DataBinding.cs` 的文件，其中包含 `ModelViewControl` 的其他部分定义。 要查看其内容，请在“解决方案资源管理器”中，打开文件的快捷菜单，然后选择“查看代码” 。

### <a name="about-the-ui-project"></a>关于 UI 项目

更新 DSL 定义文件以定义自己的 DSL 时，必须更新 `UI` 项目中的控件以显示 DSL。 与 `Dsl` 和 `DslPackage` 项目不同，示例 `UI` 项目不是从 `DslDefinitionl.dsl` 中生成的。 如果需要，可添加 .tt 文件以生成代码，尽管本演练中未对此进行介绍。

## <a name="update-the-dsl-definition"></a>更新 DSL 定义

下图是本演练中使用的 DSL 定义。

![DSL 定义](../modeling/media/dsl-wpf-1.png)

1. 在 DSL 设计器中打开 DslDefinition.dsl。

2. 删除 ExampleElement

3. 将 ExampleModel 域类重命名为 `Farm`。

     为其指定其他域属性（对于 Int32 类型，请指定 `Size`，对于 Boolean 类型，请指定 `IsOrganic`） 。

    > [!NOTE]
    > 如果删除根域类，然后创建新的根，必须重置编辑器根类属性。 在“DSL 资源管理器”中，选择“编辑器” 。 然后在“属性”窗口中，将“根类”设置为 `Farm`。

4. 使用“命名的域类”工具创建以下域类：

    - `Field` - 为此项提供名为 `Size` 的其他域属性。

    - `Animal` - 在“属性”窗口中，将“继承修饰符”设置为“抽象” 。

5. 使用“域类”工具创建以下类：

    - `Sheep`

    - `Goat`

6. 使用“继承”工具使 `Goat` 和 `Sheep` 从 `Animal` 中继承。

7. 使用“嵌入”工具在 `Farm` 下嵌入 `Field` 和 `Animal`。

8. 你可能需要整理关系图。 若要减少重复元素的数目，请使用叶元素的快捷菜单上的“Bring Subtree Here”命令。

9. 在解决方案资源管理器的工具栏中“转换所有模板”。

10. 生成 DSL 项目。

    > [!NOTE]
    > 在此阶段，生成其他项目时会出现错误。 但我们需要生成 DSL 项目，以便其程序集可供数据源向导使用。

## <a name="update-the-ui-project"></a>更新 UI 项目

现在，可创建一个新的用户控件来显示 DSL 模型中存储的信息。 要将用户控件连接到模型，最简单的方法是使用数据绑定。 ModelingBindingSource 数据绑定适配器类型专用于将 DSL 连接到非 VMSDK 接口。

### <a name="define-your-dsl-model-as-a-data-source"></a>将 DSL 模型定义为数据源

1. 在“数据”菜单上，选择“显示数据源” 。

     “数据源”窗口随即打开。

     选择“添加新数据源”。 “数据源配置”向导随即打开。

2. 依次选择“项目”、“下一步” 。

     展开“DSL”、“Company.FarmApp”，然后选择作为模型的根类的“场”  。 选择“完成”。

     在“解决方案资源管理器”中，UI 项目现在包含 Properties\DataSources\Farm.datasource 

     模型类的属性和关系显示在“数据源”窗口中。

     ![“数据源”窗口](../modeling/media/dslwpf-3.png)

### <a name="connect-your-model-to-a-form"></a>将模型连接到窗体

1. 在 UI 项目中，删除所有现有 .cs 文件。

2. 将名为 `FarmControl` 的新“用户控件”文件添加到 UI 项目 。

3. 在“数据源”窗口中，选择“场”的下拉菜单上的“详细信息”  。

    保留其他属性的默认设置。

4. 在设计视图中打开 FarmControl.cs。

    将“场”从“数据源”窗口拖动到 FarmControl。

    此时将显示一组控件，每个属性一个控件。 关系属性不生成控件。

5. 删除 farmBindingNavigator。 这也会在 `FarmControl` 设计器中自动生成，但它对此应用程序没有用。

6. 使用工具箱创建两个 DataGridView 实例，将它们命名为 `AnimalGridView` 和 `FieldGridView`。

   > [!NOTE]
   > 另一步是将“动物”和“字段”项从“数据源”窗口拖动到控件上。 此操作会自动在网格视图和数据源之间创建数据网格和绑定。 但是，此绑定对于 DSL 无法正常工作。 因此，最好手动创建数据网格和绑定。

7. 如果工具箱中不包含 ModelingBindingSource 工具，请添加它。 在“数据”选项卡的快捷菜单上，选择“选择项” 。 在“选择工具箱项”对话框中，从“.NET Framework”选项卡中选择“ModelingBindingSource”  。

8. 使用工具箱创建两个 ModelingBindingSource 实例，将它们命名为 `AnimalBinding` 和 `FieldBinding`。

9. 将每个 ModelingBindingSource 的 DataSource 属性设置为 farmBindingSource  。

     将 DataMember 属性设置为“Animals”或“Fields”  。

10. 将 `AnimalGridView` 的 DataSource 属性设置为 `AnimalBinding`，并将 `FieldGridView` 的设置为 `FieldBinding`。

11. 根据喜好调整“场”控件的布局。

    ModelingBindingSource 是一种适配器，它执行特定于 DSL 的多个函数：

- 它将更新包装在 VMSDK 存储事务中。

   例如，当用户从数据视图网格中删除行时，常规绑定将导致事务异常。

- 它确保当用户选择行时，“属性”窗口显示相应模型元素的属性，而不是数据网格行。

  ![DSL 绑定的架构](../modeling/media/dslwpf4.png)
  
  数据源和视图之间的链接架构。

### <a name="complete-the-bindings-to-the-dsl"></a>完成与 DSL 的绑定

1. 在 UI 项目的单独代码文件中添加以下代码：

    ```csharp
    using System.ComponentModel;
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Design;

    namespace Company.FarmApp
    {
      partial class FarmControl
      {
        public IContainer Components { get { return components; } }

        /// <summary>Binds the WinForms data source to the DSL model.
        /// </summary>
        /// <param name="nodelRoot">The root element of the model.</param>
        public void DataBind(ModelElement modelRoot)
        {
          WinFormsDataBindingHelper.PreInitializeDataSources(this);
          this.farmBindingSource.DataSource = modelRoot;
          WinFormsDataBindingHelper.InitializeDataSources(this);
        }
      }
    }
    ```

2. 在 DslPackage 项目中，编辑 DslPackage\DocView.tt 以更新以下变量定义 ：

    ```csharp
    string viewControlTypeName = "FarmControl";
    ```

## <a name="test-the-dsl"></a>测试 DSL

DSL 解决方案现在可以生成并运行，不过建议稍后再添加改进。

1. 生成并运行解决方案。

2. 在 Visual Studio 的实验实例中，打开“示例”文件。

3. 在“FarmApp 资源管理器”中，打开“场”根节点上的快捷菜单，然后选择“添加新的山羊”  。

     `Goat1` 会显示在“动物”视图中。

    > [!WARNING]
    > 必须使用“场”节点上的快捷菜单，而不是“动物”节点上的 。

4. 选择“场”根节点，并查看其属性。

     在窗体视图中，更改场的“名称”和“大小” 。

     当你离开窗体的每个字段时，“属性”窗口中的相应属性将更改。

## <a name="enhance-the-dsl"></a>增强 DSL

### <a name="make-the-properties-update-immediately"></a>立即更新属性

1. 在 FarmControl.cs 的设计视图中，选择一个简单的字段，例如 Name、Size 或 IsOrganic。

2. 在“属性”窗口中，展开“DataBindings”，并打开“(高级)” 。

     在“格式设置和高级绑定”对话框中的“数据源更新模式”下，选择“OnPropertyChanged”  。

3. 生成并运行解决方案。

     验证更改字段内容时，场模型的相应属性是否立即更改。

### <a name="provide-add-buttons"></a>提供“添加”按钮

1. 在 FarmControl.cs 的设计视图中，使用工具箱在窗体上创建按钮。

    编辑按钮的名称和文本，例如 `New Sheep`。

2. 打开按钮后面的代码（例如双击代码）。

    按如下所示编辑它：

   ```csharp
   private void NewSheepButton_Click(object sender, EventArgs e)
   {
     using (Transaction t = farm.Store.TransactionManager.BeginTransaction("Add sheep"))
     {
       elementOperations.MergeElementGroup(farm,
         new ElementGroup(new Sheep(farm.Partition)));
       t.Commit();
     }
   }

   // The following code is shared with other add buttons:
   private ElementOperations operationsCache = null;
   private ElementOperations elementOperations
   {
     get
     {
       if (operationsCache == null)
       {
         operationsCache = new ElementOperations(farm.Store, farm.Partition);
       }
       return operationsCache;
     }
   }
   private Farm farm
   {
     get { return this.farmBindingSource.DataSource as Farm; }
   }
   ```

    还需要插入以下指令：

   ```csharp

   using Microsoft.VisualStudio.Modeling;
   ```

3. 为“山羊”和“字段”添加类似的按钮。

4. 生成并运行解决方案。

5. 验证新按钮是否添加了项。 新项应同时显示在 FarmApp 资源管理器和相应的数据网格视图中。

    应能够在数据网格视图中编辑元素的名称。 也可从中删除它。

   ![示例数据网格视图](../modeling/media/dsl-wpf-2.png)

### <a name="about-the-code-to-add-an-element"></a>关于添加元素的代码

对于新元素按钮，使用以下替代代码稍微简单一些。

```csharp
private void NewSheepButton_Click(object sender, EventArgs e)
{
  using (Transaction t = farm.Store.TransactionManager.BeginTransaction("Add sheep"))
  {
    farm.Animals.Add(new Sheep(farm.Partition)); ;
    t.Commit();
  }
}
```

但是，此代码不会设置新项的默认名称。 它不会运行可能在 DSL 的元素合并指令中定义的任何自定义合并，也不运行任何已定义的自定义合并代码。

因此，我们建议你使用 <xref:Microsoft.VisualStudio.Modeling.ElementOperations> 来创建新元素。 有关详细信息，请参阅[自定义元素的创建和移动](../modeling/customizing-element-creation-and-movement.md)。

## <a name="see-also"></a>另请参阅

- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)
- [编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [Visual Studio 的建模 SDK - 特定于域的语言](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)
