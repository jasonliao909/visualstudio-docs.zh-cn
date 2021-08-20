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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122061319"
---
# <a name="create-a-windows-forms-based-domain-specific-language"></a>创建Windows窗体的Domain-Specific语言

可以使用"Windows窗体"来显示 DSL 模型 (域) 语言的状态，而不是使用 DSL 关系图。 本主题逐步介绍如何使用可视化Windows建模 SDK 将窗体绑定到 DSL Visual Studio DSL。

下图显示了 DSL Windows窗体 UI 和模型资源管理器：

![VISUAL STUDIO 中的 DSL 实例](../modeling/media/dsl-wpf-2.png)

## <a name="create-a-windows-forms-dsl"></a>创建 Windows 窗体 DSL

最小 **WinForm 设计器** DSL 模板创建一个最小 DSL，你可以修改该 DSL 以满足自己的要求。

1. 从"最小 **WinForm 设计器"模板创建** DSL。

    本演练假定以下名称：

    - 解决方案和 DSL 名称： `FarmApp`
    - 命名空间：`Company.FarmApp`

2. 试验模板提供的初始示例：

   1. 转换所有模板。

   2. 使用 **Ctrl** + **F5** (生成并运行) 。

   3. 在 Visual Studio试验实例中， `Sample` 打开调试项目中的 文件。

        请注意，它显示在窗体Windows窗体控件中。

        还可以在资源管理器中查看模型的元素。

        在窗体或资源管理器中添加一些元素，请注意它们显示在另一个显示中。

   在主实例Visual Studio，请注意有关 DSL 解决方案的以下几点：

- `DslDefinition.dsl` 不包含关系图元素。 这是因为你将不使用 DSL 关系图来查看此 DSL 的实例模型。 相反，你将将Windows窗体绑定到模型，窗体上的元素将显示模型。

- 除了 和 项目外，解决方案还包含名为 UI 项目的第三个项目，该项目包含 Windows `Dsl` `DslPackage` `UI.` 窗体控件的定义。 `DslPackage` 依赖于 `UI` ， `UI` 并且依赖于 `Dsl` 。

- 在 `DslPackage` 项目中， `UI\DocView.cs` 包含显示项目中Windows窗体控件的代码 `UI` 。

- 该项目 `UI` 包含绑定到 DSL 的窗体控件的工作示例。 但是，更改 DSL 定义后，它将不起作用。 项目 `UI` 包含：

  - 名为 Windows Forms 类 `ModelViewControl` 。

  - 一个名为 `DataBinding.cs` 的文件，其中包含 的其他部分定义 `ModelViewControl` 。 若要查看其内容，请 **解决方案资源管理器，打开** 文件的快捷菜单，然后选择"查看 **代码"。**

### <a name="about-the-ui-project"></a>关于 UI 项目

更新 DSL 定义文件以定义自己的 DSL 时，必须更新项目中的 控件以显示 `UI` DSL。 与 `Dsl` 和 `DslPackage` 项目不同，示例 `UI` 项目不是从 生成的 `DslDefinitionl.dsl` 。 如果需要，可以添加 .tt 文件以生成代码，尽管本演练中未对此进行介绍。

## <a name="update-the-dsl-definition"></a>更新 DSL 定义

下图是本演练中使用的 DSL 定义。

![DSL 定义](../modeling/media/dsl-wpf-1.png)

1. 在 DSL 设计器中打开 DslDefinition.dsl。

2. 删除 **ExampleElement**

3. 将 **ExampleModel 域** 类重命名为 `Farm` 。

     为它提供名为 `Size` **Int32** 类型和布尔类型的其他 `IsOrganic` **域属性**。

    > [!NOTE]
    > 如果删除根域类，然后创建新的根，必须重置编辑器根类属性。 在 **DSL 资源管理器中**，选择"编辑器 **"。** 然后，在属性窗口中，将 **"根类"** 设置为 `Farm` 。

4. 使用 **命名域类** 工具创建以下域类：

    - `Field` - 为此提供名为 的附加域属性 `Size` 。

    - `Animal`- 在"属性窗口中，将 **"继承修饰符"设置为**"**抽象"。**

5. 使用 **域类** 工具创建以下类：

    - `Sheep`

    - `Goat`

6. 使用 **继承** 工具从 `Goat` 创建 `Sheep` 和继承 `Animal` 。

7. 使用嵌入 **工具** 在 下 `Field` 嵌入 `Animal` 和 `Farm` 。

8. 可能需要整理关系图。 若要减少重复元素的数量，请使用叶元素快捷菜单上的 **"将子树** 引入此处"命令。

9. **在模板的工具栏** 中转换所有解决方案资源管理器。

10. 生成 **Dsl** 项目。

    > [!NOTE]
    > 在此阶段，其他项目不会在没有错误的情况下生成。 但是，我们想要生成 Dsl 项目，以便其程序集可供数据源向导使用。

## <a name="update-the-ui-project"></a>更新 UI 项目

现在，可以创建一个新的用户控件，该控件将显示 DSL 模型中存储的信息。 将用户控件连接到模型的最简单方法是通过数据绑定。 名为 **ModelingBindingSource 的数据绑定适配器** 类型专门用于将 DLL 连接到非 VMSDK 接口。

### <a name="define-your-dsl-model-as-a-data-source"></a>将 DSL 模型定义为数据源

1. 在"**数据"菜单** 上，选择"**显示数据源"。**

     “数据源”窗口随即打开。

     选择 **"添加新数据源"。** " **数据源配置向导"随即** 打开。

2. 选择 **"对象"，** 然后选择"**下一步"。**

     展开 **Dsl** **、Company.FarmApp，** 然后选择 **"场**"，这是模型的根类。 选择“完成”。

     在解决方案资源管理器中 **，UI** 项目现在包含 **Properties\DataSources\Farm.datasource**

     模型类的属性和关系显示在"数据源"窗口中。

     !["数据源"窗口](../modeling/media/dslwpf-3.png)

### <a name="connect-your-model-to-a-form"></a>连接模型到窗体

1. 在 **UI 项目中** ，删除所有现有的 .cs 文件。

2. 将名为 **的新用户控件** 文件 `FarmControl` 添加到 **UI** 项目。

3. 在"**数据源"窗口中** 的"场"上的下拉菜单 **中，选择**"详细信息 **"。**

    保留其他属性的默认设置。

4. 在设计视图中打开 FarmControl.cs。

    将 **"场** "从"数据源"窗口拖到 FarmControl 上。

    将显示一组控件，每个属性一个控件。 关系属性不生成控件。

5. 删除 **farmBindingNavigator**。 这也会在设计器中自动生成，但它 `FarmControl` 对此应用程序没有用。

6. 使用工具箱创建 **DataGridView** 的两个实例，并命名它们 `AnimalGridView` 和 `FieldGridView` 。

   > [!NOTE]
   > 另一步是将"动物"和"字段"项从"数据源"窗口拖动到控件上。 此操作会自动在网格视图和数据源之间创建数据网格和绑定。 但是，此绑定对于 DSL 无法正常工作。 因此，最好手动创建数据网格和绑定。

7. 如果工具箱不包含 **ModelingBindingSource** 工具，请添加它。 在"数据"选项卡的 **快捷菜单上**，选择"**选择项"。** 在"**选择工具箱项"** 对话框中，从"工具箱"选项卡中选择"modelingBindingSource.NET Framework"。  

8. 使用工具箱创建 **ModelingBindingSource** 的两个实例，并命名它们 `AnimalBinding` 和 `FieldBinding` 。

9. 将每个 **ModelingBindingSource** 的 **DataSource** 属性设置为 **farmBindingSource**。

     将 **DataMember** 属性设置为 **"动物"或**"**字段"。**

10. 将 **的 DataSource** 属性 `AnimalGridView` 设置为 `AnimalBinding` ，将 的 DataSource 属性设置为  `FieldGridView` `FieldBinding` 。

11. 根据喜好调整"场"控件的布局。

    **ModelingBindingSource** 是一个适配器，可执行多个特定于 DSL 的函数：

- 它将更新包装在 VMSDK 存储事务中。

   例如，当用户从数据视图网格中删除某行时，常规绑定将导致事务异常。

- 它可确保在用户选择某一行时，属性窗口显示相应模型元素的属性，而不是显示数据网格行。

  ![DSL 绑定的架构](../modeling/media/dslwpf4.png)
  
  数据源和视图之间的链接架构。

### <a name="complete-the-bindings-to-the-dsl"></a>完成到 DSL 的绑定

1. 在 **UI** 项目的单独代码文件中添加以下代码：

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

2. 在 **DslPackage** 项目中，编辑 **DslPackage\DocView.tt** 以更新以下变量定义：

    ```csharp
    string viewControlTypeName = "FarmControl";
    ```

## <a name="test-the-dsl"></a>测试 DSL

现在，可以生成并运行 DSL 解决方案，但以后可能需要添加更多改进。

1. 生成并运行解决方案。

2. 在 Visual Studio 的实验实例中，打开 **示例** 文件。

3. 在 **FarmApp 资源管理器** 中，打开 **场** 根节点上的快捷菜单，然后选择 " **添加新 Goat**"。

     `Goat1` 显示在 " **动物** " 视图中。

    > [!WARNING]
    > 必须使用 **场** 节点上的快捷菜单，而不是 " **动物** " 节点。

4. 选择 **场** 根节点并查看其属性。

     在窗体视图中，更改场的 **名称** 或 **大小** 。

     离开窗体中的每个字段时，相应的属性更改属性窗口中。

## <a name="enhance-the-dsl"></a>增强 DSL

### <a name="make-the-properties-update-immediately"></a>立即更新属性

1. 在 FarmControl 的 "设计" 视图中，选择 "名称"、"大小" 或 "IsOrganic" 等简单字段。

2. 在属性窗口中 **，展开 "** databinding" 并打开 **(高级)**"。

     在 " **格式设置和高级绑定** " 对话框的 " **数据源更新模式**" 下，选择 " **OnPropertyChanged**"。

3. 生成并运行解决方案。

     验证在更改字段内容时，场模型的相应属性会立即更改。

### <a name="provide-add-buttons"></a>提供 "添加" 按钮

1. 在 FarmControl 的 "设计" 视图中，使用 "工具箱" 来创建窗体上的按钮。

    编辑按钮的名称和文本（例如） `New Sheep` 。

2. 打开按钮后面的代码 (例如，双击它) 。

    按如下所示对其进行编辑：

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

3. 为 "Goats" 和 "字段" 添加类似的按钮。

4. 生成并运行解决方案。

5. 验证 "新建" 按钮是否添加项。 新项应同时出现在 "FarmApp 资源管理器" 和相应的数据网格视图中。

    您应该能够在数据网格视图中编辑元素的名称。 你还可以从此处删除它。

   ![示例数据网格视图](../modeling/media/dsl-wpf-2.png)

### <a name="about-the-code-to-add-an-element"></a>关于要添加元素的代码

对于新元素按钮，以下替代代码稍微简单一些。

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

但是，此代码不会设置新项的默认名称。 它不会运行你可能在 DSL 的 **元素合并指令** 中定义的任何自定义的合并，并且它不会运行可能已定义的任何自定义合并代码。

因此，我们建议你使用 <xref:Microsoft.VisualStudio.Modeling.ElementOperations> 来创建新元素。 有关详细信息，请参阅 [自定义元素创建和移动](../modeling/customizing-element-creation-and-movement.md)。

## <a name="see-also"></a>请参阅

- [如何定义 Domain-Specific 语言](../modeling/how-to-define-a-domain-specific-language.md)
- [编写代码以自定义 Domain-Specific 语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [Visual Studio 的建模 SDK - 特定于域的语言](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)
