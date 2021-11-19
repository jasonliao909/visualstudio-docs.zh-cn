---
title: 自定义“属性”窗口
description: 了解如何在 Visual Studio 中使用域特定语言 (DSL) 自定义属性窗口的外观和行为。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Domain-Specific Language, Properties window
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 0b69d16fdf3d1a4cd3d9540f186734f3cfdb8643
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671883"
---
# <a name="customize-the-properties-window"></a>自定义“属性”窗口

在 Visual Studio 中使用域特定语言 (DSL) 自定义属性窗口的外观和行为。 在 DSL 定义中，在每个域类上定义域属性。 默认情况下，在关系图或模型资源管理器中选择类的实例时，每个域属性都列在属性窗口中。 这样，即使尚未将域属性的值映射到关系图上的形状字段，也能够查看和编辑它们。

## <a name="names-descriptions-and-categories"></a>名称、说明和类别

**名称和显示名称**。 在域属性的定义中，属性的显示名称是运行时显示在属性窗口中的名称。 相比之下，名称用于编写程序代码以更新属性时。 名称必须是正确的 CLR 字母数字名称，但显示名称可以包含空格。

在 DSL 定义中设置属性的名称时，其显示名称将自动设置为名称的副本。 如果编写卡斯卡大小写的名称，例如“FuelGauge”，显示名称将自动包含一个空格：“Fuel Gauge”。 但是，可以将显示名称显式设置为其他值。

**说明**。 域属性的说明显示在两处：

- 当用户选择属性时，位于属性窗口底部。 可以使用它向用户说明属性表示什么。

- 在生成的程序代码中。 如果使用文档工具提取 API 文档，它将在 API 中显示为此属性的说明。

**类别**。 类别是属性窗口中的标题。

## <a name="expose-style-features"></a>公开样式特征

图形元素的一些动态功能可以表示或公开为域属性。 用户可以更新，程序代码可以更轻松地更新这样公开的功能。

在“DSL 定义”中右键单击形状类，指向“添加已公开”，然后选择功能。

在形状上，可以公开 FillColor、OutlineColor、TextColor、OutlineDashStyle、OutlineThickness 和 FillGradientMode 属性。      在连接器上，可以公开 ColorTextColor`,`  DashStyle 和 Thickness属性。 在关系图上，可以公开 FillColor 和 TextColor 属性。 

## <a name="forwarding-display-properties-of-related-elements"></a>转发：显示相关元素的属性

当 DSL 用户选择模型中的元素时，该元素的属性将显示在属性窗口中。 但是，也可以显示指定相关元素的属性。 如果定义了一组协同工作的元素，这很有用。 例如，可以定义主元素和可选的插件元素。 如果主元素映射到形状，而另一个元素不映射到形状，将所有属性视为位于一个元素上会很有用。

此效果称为“属性转发”，在某些情况下会自动发生。 在其他情况下，可以通过定义域类型描述符来实现属性转发。

### <a name="default-property-forwarding-cases"></a>默认属性转发用例

当用户在资源管理器中选择形状、连接器或元素时，以下属性将显示在属性窗口中：

- 在模型元素的域类上定义的域属性，包括在基类中定义的域属性。 一个例外是已将其 Is Browsable 设置为 `False` 的域属性。

- 通过多样性为 0..1 的关系链接的元素的名称。 这提供了一种查看选择性链接的元素的简便方法，即使未为关系定义连接器映射也可使用。

- 以元素为目标的嵌入关系的域属性。 由于嵌入关系通常不会显式显示，这让用户能够查看其属性。

- 在所选形状或连接器上定义的域属性。

### <a name="add-property-forwarding"></a>添加属性转发

若要转发属性，请定义域类型描述符。 如果两个域类之间具有域关系，可以使用域类型描述符将第一个类中的域属性设置为第二个域类中域属性的值。 例如，如果在 Book 域类与 Author 域类之间具有关系，可以使用域类型描述符，使得在用户选择书籍时，书籍 Author 的 Name 属性显示在属性窗口中。   

> [!NOTE]
> 属性转发仅在用户编辑模型时影响属性窗口。 它不会在接收类上定义域属性。 如果要在 DSL 定义的其他部分或程序代码中访问转发域属性，则必须访问转发元素。

以下过程假定你已创建 DSL。 前几个步骤汇总了先决条件。

#### <a name="forward-a-property-from-another-element"></a>从另一个元素转发属性

1. 创建至少包含两个类的 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 解决方案，在本例中这两个类分别称为 Book 和 Author。  Book 和 Author 之间应存在某种类型的关系。 

    源角色的多重性（Book 端的角色）应为 0..1 或 1..1，以便每个 Book 都对应一个 Author。  

2. 在 DSL 资源管理器中，右键单击“Book”域类，然后单击“新增 DomainTypeDescriptor”。  

    名为“自定义属性描述符的路径”的节点显示在“自定义类型描述符”节点下。 

3. 右键单击“自定义类型描述符”节点，然后单击“新增 PropertyPath”。 

    新的属性路径显示在“自定义属性描述符的路径”节点下。

4. 选择新的属性路径，在“属性”窗口中将“属性的路径”设置为相应模型元素的路径。 

    可以通过单击此属性右边的向下箭头，在树视图中编辑路径。 有关域路径详细信息，请参阅[域路径语法](../modeling/domain-path-syntax.md)。 编辑后，路径应类似于 BookReferencesAuthor.Author/!Author。

5. 将“属性”设置为 Author 的 Name 域属性。  

6. 将“显示名称”设置为“作者姓名”。 

7. 转换所有模板，生成并运行 DSL。

8. 在模型图中，创建书籍和作者，然后使用引用关系链接它们。 选择 book 元素，应可在属性窗口中看到作者名称和书籍的各种属性。 更改链接作者的姓名，或将书籍链接到其他作者，并观察书籍的作者姓名是否发生变化。

## <a name="custom-property-editors"></a>自定义属性编辑器

属性窗口为每个域属性的类型提供适当的默认编辑体验。 例如，对于枚举类型，用户会看到下拉列表；对于数值属性，用户可以输入数字。 这仅适用于内置类型。 如果指定外部类型，用户将能够看到属性的值，但不能对其进行编辑。

但是，你可以指定以下编辑器和类型：

1. 与标准类型一同使用的另一个编辑器。 例如，可以指定字符串属性的文件路径编辑器。

2. 域属性的外部类型及其相应编辑器。

3. .NET 编辑器（如文件路径编辑器），你也可以创建自己的自定义属性编辑器。

   外部类型与具有默认编辑器的类型（如字符串）之间的转换。

   在 DSL 中，外部类型是不属于简单类型（例如布尔型或 Int32）的任何类型）或字符串的任何类型。

### <a name="define-a-domain-property-that-has-an-external-type"></a>定义具有外部类型的域属性

1. 在解决方案资源管理器中，在 Dsl 项目中添加对包含外部类型的程序集 (DLL) 的引用。 

    程序集可以是 .NET 程序集，也可以是由你提供的程序集。

2. 将类型添加到“域类型”列表（如果尚未这样做）。

   1. 打开 DslDefinition.dsl，在 DSL 资源管理器中右键单击根节点，然后单击“新增外部类型”。 

        “域类型”节点下会显示一个新条目。

       > [!WARNING]
       > 菜单项位于 DSL 根节点上，而不是“域类型”节点上。

   2. 在属性窗口中设置新类型的名称和命名空间。

3. 以常见方式将域属性添加到域类。

    在属性窗口中，在“类型”字段中从下拉列表中选择外部类型。

   在此阶段，用户可以查看属性的值，但不能对其进行编辑。 显示的值是从 `ToString()` 函数获取的。 可以编写用于设置属性值的程序代码，例如在命令或规则中编写。

### <a name="set-a-property-editor"></a>设置属性编辑器

将 CLR 属性添加到域属性，格式如下：

```csharp
[System.ComponentModel.Editor (
   typeof(AnEditor),
   typeof(System.Drawing.Design.UITypeEditor))]
```

可以使用属性窗口中的“自定义属性”条目在属性上设置特性。

`AnEditor` 的类型必须派生自第二个参数中指定的类型。 第二个参数应为 <xref:System.Drawing.Design.UITypeEditor> 或 <xref:System.ComponentModel.ComponentEditor>。 有关详细信息，请参阅 <xref:System.ComponentModel.EditorAttribute>。

可以指定自己的编辑器或 .NET 编辑器，例如 <xref:System.Windows.Forms.Design.FileNameEditor> 或 <xref:System.Drawing.Design.ImageEditor>。 例如，使用以下过程创建一个属性，让用户可以在其中输入文件名。

#### <a name="define-a-file-name-domain-property"></a>定义文件名域属性

1. 在 DSL 定义中向域类添加域属性。

2. 选择新属性。 在属性窗口中的“自定义属性”字段中，输入以下属性。 若要输入此属性，请单击省略号 [...]，然后分别输入属性名称和参数：

    ```csharp
    [System.ComponentModel.Editor (
       typeof(System.Windows.Forms.Design.FileNameEditor)
       , typeof(System.Drawing.Design.UITypeEditor))]

    ```

3. 将域属性的“类型”保留为其默认设置“字符串”。

4. 若要测试编辑器，请验证用户能否打开文件名编辑器来编辑域属性。

    1. 按 CTRL+F5 或 F5。 在调试解决方案中，打开测试文件。 创建域类的元素并选择它。

    2. 在属性窗口中，选择域属性。 值字段显示省略号 [...]。

    3. 单击省略号。 将显示一个文件对话框。 选择一个文件并关闭对话框。 文件路径现在是域属性的值。

### <a name="define-your-own-property-editor"></a>定义自己的属性编辑器

可以定义自己的编辑器。 这样做可以允许用户编辑你定义的类型，或以特殊方式编辑标准类型。 例如，可以允许用户输入表示公式的字符串。

通过编写派生自 <xref:System.Drawing.Design.UITypeEditor> 的类来定义编辑器。 类必须重写：

- <xref:System.Drawing.Design.UITypeEditor.EditValue%2A>，以便与用户交互并更新属性值。

- <xref:System.Drawing.Design.UITypeEditor.GetEditStyle%2A>，用于指定编辑器是打开对话框还是提供下拉菜单。

还可以提供将在属性网格中显示的属性值的图形表示形式。 若要执行此操作，请重写 `GetPaintValueSupported` 和 `PaintValue`。  有关详细信息，请参阅 <xref:System.Drawing.Design.UITypeEditor>。

> [!NOTE]
> 在 Dsl 项目的单独代码文件中添加代码。

例如：

```csharp
internal class TextFileNameEditor : System.Windows.Forms.Design.FileNameEditor
{
  protected override void InitializeDialog(System.Windows.Forms.OpenFileDialog openFileDialog)
  {
    base.InitializeDialog(openFileDialog);
    openFileDialog.Filter = "Text files(*.txt)|*.txt|All files (*.*)|*.*";
    openFileDialog.Title = "Select a text file";
  }
}
```

若要使用此编辑器，请将域属性的“自定义属性”设置为：

```csharp
[System.ComponentModel.Editor (
   typeof(MyNamespace.TextFileNameEditor)
   , typeof(System.Drawing.Design.UITypeEditor))]
```

有关详细信息，请参阅 <xref:System.Drawing.Design.UITypeEditor>。

## <a name="provide-a-drop-down-list-of-values"></a>提供值的下拉列表

你可以提供值列表供用户选择。

> [!NOTE]
> 此方法提供可在运行时更改的值的列表。 如果要提供不会更改的列表，请考虑改为使用枚举类型作为域属性的类型。

若要定义标准值列表，请向域属性添加具有以下格式的 CLR 属性：

```csharp
[System.ComponentModel.TypeConverter
(typeof(MyTypeConverter))]
```

定义一个从 <xref:System.ComponentModel.TypeConverter> 派生的类。 在 Dsl 项目的单独文件中添加代码。 例如：

```csharp
/// <summary>
/// Type converter that provides a list of values
/// to be displayed in the property grid.
/// </summary>
/// <remarks>This type converter returns a list
/// of the names of all "ExampleElements" in the
/// current store.</remarks>
public class MyTypeConverter : System.ComponentModel.TypeConverter
{
  /// <summary>
  /// Return true to indicate that we return a list of values to choose from
  /// </summary>
  /// <param name="context"></param>
  public override bool GetStandardValuesSupported
    (System.ComponentModel.ITypeDescriptorContext context)
  {
    return true;
  }

  /// <summary>
  /// Returns true to indicate that the user has
  /// to select a value from the list
  /// </summary>
  /// <param name="context"></param>
  /// <returns>If we returned false, the user would
  /// be able to either select a value from
  /// the list or type in a value that is not in the list.</returns>
  public override bool GetStandardValuesExclusive
      (System.ComponentModel.ITypeDescriptorContext context)
  {
    return true;
  }

  /// <summary>
  /// Return a list of the values to display in the grid
  /// </summary>
  /// <param name="context"></param>
  /// <returns>A list of values the user can choose from</returns>
  public override StandardValuesCollection GetStandardValues
      (System.ComponentModel.ITypeDescriptorContext context)
  {
    // Try to get a store from the current context
    // "context.Instance"  returns the element(s) that
    // are currently selected i.e. whose values are being
    // shown in the property grid.
    // Note that the user could have selected multiple objects,
    // in which case context.Instance will be an array.
    Store store = GetStore(context.Instance);

    List<string> values = new List<string>();

    if (store != null)
    {
      values.AddRange(store.ElementDirectory
        .FindElements<ExampleElement>()
        .Select<ExampleElement, string>(e =>
      {
        return e.Name;
      }));
    }
    return new StandardValuesCollection(values);
  }

  /// <summary>
  /// Attempts to get to a store from the currently selected object(s)
  /// in the property grid.
  /// </summary>
  private Store GetStore(object gridSelection)
  {
    // We assume that "instance" will either be a single model element, or
    // an array of model elements (if multiple items are selected).

    ModelElement currentElement = null;

    object[] objects = gridSelection as object[];
    if (objects != null && objects.Length > 0)
    {
      currentElement = objects[0] as ModelElement;
    }
    else
    {
        currentElement = gridSelection as ModelElement;
    }

    return (currentElement == null) ? null : currentElement.Store;
  }

}
```

## <a name="see-also"></a>另请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
