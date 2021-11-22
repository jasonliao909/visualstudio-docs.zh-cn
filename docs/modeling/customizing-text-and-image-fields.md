---
title: 自定义文本和图像字段
description: 了解如何自定义文本和图像文件。 并了解在形状中定义文本修饰器后，它以 TextField 表示。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 13cde2406402f6afc2d61deca4e6e95e838e5dff
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671888"
---
# <a name="customizing-text-and-image-fields"></a>自定义文本和图像字段
在形状中定义文本修饰器后，它以 TextField 表示。 有关 TextField 和其他 ShapeField 的初始化示例，请在 DSL 解决方案中查看 Dsl\GeneratedCode\Shapes.cs。

 TextField 是一个对象，其管理形状内的区域，如分配给标签的空间。 一个 TextField 实例在同一类的多个形状之间共享。 TextField 实例不单独存储每个实例的标签文本：相反，`GetDisplayText(ShapeElement)` 方法会将形状视为一个参数，并可以查找依赖于形状及其模型元素的当前状态的文本。

## <a name="how-the-appearance-of-a-text-field-is-determined"></a>如何确定文本字段的外观
 调用 `DoPaint()` 方法以在屏幕上显示该字段。 可以替代默认值 `DoPaint(),`，也可以替代它所调用的某些方法。 以下默认方法简化版本可帮助了解如何替代默认行为：

```csharp
// Simplified version:
public override void DoPaint(DiagramPaintEventArgs e, ShapeElement parentShape)
{
  string text = GetDisplayText(shape);
  StringFormat format = GetStringFormat(parentShape);
  Brush brush = GetTextBrush(e.View, shape);
  using (Font font = GetFont(shape))
  {
    e.Graphics.DrawString(text, font, brush, format);
  }
}
// StringFormat determines whether the string is centered etc.
// To customize statically for all instances of this shape field,
// assign to DefaultStringFormat.
// To customize dynamically or per shape, override this:
public virtual StringFormat GetStringFormat(ShapeElement shape)
{ return DefaultStringFormat; }

// Override to customize the displayed string:
public virtual string GetDisplayText(ShapeElement shape)
{ return this.GetValue(shape).ToString(); }

// Brush determines the text color.
// To change the brush for every field, change the shape's styleset.
// To customize to a brush in the style set, override GetTextBrushId.
// To change the brush to non-standard color, override this.
// Should take account of whether selected.
public virtual Brush GetTextBrush(DiagramClientView view, ShapeElement shape)
{ return shape.StyleSet.GetBrush(this.GetTextBrushId(view, shape)); }

// Brush ID selects a brush from a StyleSet.
// Either return a member of DiagramBrushes
// or add your own brush to the shape or application's styleset.
// Override this to change dynamically or per instance.
// To change statically, just assign to default values.
public virtual StyleSetResourceId GetTextBrushId(DiagramClientView view, ShapeElement shape)
{ return IsSelected(view, shape) ? (view.Focused ? DefaultSelectedTextBrushId
: DefaultInactiveSelectedTextBrushId ) : DefaultTextBrushId ;
}

// Font determines the shape and size of the text.
// To change the font for every field, change the shape's styleset.
// To customize to a font in the style set, override GetFontId.
// To change the font to a non-standard font, override this.
public virtual Font GetFont(ShapeElement shape)
{ return shape.StyleSet.GetFont(GetFontId(shape)); }

// Selects a font from a styleset.
// Either return a member of DiagramFonts or
// add your own font to the shape or application's styleset.
// To change statically for all instances of this field,
// assign to DefaultFontId.
// To change per shape or dynamically, override this.
public virtual StyleSetResourceId GetFontId(ShapeElement parentShape)
{ return DefaultFontId; }
```

 还有一些其他 `Get` 方法和 `Default` 属性对，如 `DefaultMultipleLine/GetMultipleLine()`。 可以为默认属性指定一个值，以更改形状字段的所有实例的值。 若要使不同形状实例之间的值不同，或依赖于形状或其模型元素的状态，请替代 `Get` 方法。

## <a name="static-customizations"></a>静态自定义
 如果要更改此形状字段的每个实例，请首先确定是否可以在 DSL 定义中设置属性。 例如，可以在“属性”窗口中设置字体大小和样式。

 如果不要更改，则替代形状类的 `InitializeShapeFields` 方法，并将值分配给文本字段的相应 `Default...` 属性。

> [!WARNING]
> 若要替代 `InitializeShapeFields()`，必须在 DSL 定义中将形状类的“Generates Double Derived”属性设置为 `true`。

 在此示例中，形状具有一个文本字段，该字段将用于用户注释。 我们想要使用标准注释字体。 由于它是样式集中的标准字体，因此可以设置默认字体 ID：

```csharp

 partial class ExampleShape
{   protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);
      // Find and update comment field:
      TextField commentField = ShapeElement.FindShapeField(shapeFields, "CommentDecorator") as TextField;
      // Use the standard font for comments:
      commentField.DefaultFontId = DiagramFonts.CommentText;
```

## <a name="dynamic-customizations"></a>动态自定义
 若要使外观因形状或其模型元素的状态而异，请派生你自己的 `TextField` 子类并替代一个或多个 `Get...` 方法。 还必须替代形状的 InitializeShapeFields 方法，并将 TextField 的实例替换为你自己的类的实例。

 以下示例使文本字段的字体依赖于形状的模型元素的布尔域属性的状态。

 若要运行此示例代码，请使用“最小语言”模板创建新的 DSL 解决方案。 将布尔域属性 `AlternateState` 添加到 ExampleElement 域类。 向 ExampleShape 类添加一个图标修饰器，并将其图像设置为位图文件。 单击“转换所有模板”。 在 DSL 项目中添加一个新的代码文件，并插入以下代码。

 若要测试代码，请按 F5，然后在调试解决方案中，打开示例关系图。 此时应显示图标的默认状态。 选择该形状，然后在“属性”窗口中，更改 AlternateState 属性的值。 元素名称的字体将随之更改。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
...

  partial class ExampleShape
  {
    /// <summary>
    /// Compose a list of the fields in this shape.
    /// Called once for each shape class.
    /// </summary>
    protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);
      // Replace the text field for NameDecorator:
      TextField oldField = ShapeElement.FindShapeField(shapeFields, "NameDecorator") as TextField;
      shapeFields.Remove(oldField);
      // Replace with my text field based on DSL Definition values:
      MyTextField newField = new MyTextField(oldField);
      shapeFields.Add(newField);
    }
  }
  /// <summary>
  /// Dynamic font depends on state of model element.
  /// </summary>
  public class MyTextField : TextField
  {
    public MyTextField(TextField prototype)
      : base(prototype.Name)
    {
      DefaultText = prototype.DefaultText;
      DefaultFocusable = prototype.DefaultFocusable;
      DefaultAutoSize = prototype.DefaultAutoSize;
      AnchoringBehavior.MinimumHeightInLines = prototype.AnchoringBehavior.MinimumHeightInLines;
      AnchoringBehavior.MinimumWidthInCharacters = prototype.AnchoringBehavior.MinimumWidthInCharacters;
      DefaultAccessibleState = prototype.DefaultAccessibleState;
    }

    public override System.Drawing.Font GetFont(ShapeElement parentShape)
    {
      // Access the Boolean domain property of the model element:
      if ((parentShape.ModelElement as ExampleElement).AlternateState)
        return new System.Drawing.Font("Callisto", 14.0f,
               System.Drawing.FontStyle.Italic |
               System.Drawing.FontStyle.Bold);
      else
        return base.GetFont(parentShape);
    }

  }
```

## <a name="style-sets"></a>样式集
 前面的示例演示了如何将文本字段更改为任何可用的字体。 但是，更可取的方法是将其更改为与形状或应用程序关联的一组样式中的一个。 为此，请替代 <xref:Microsoft.VisualStudio.Modeling.Diagrams.TextField.GetFontId%2A> 或 GetTextBrushId ()。

 另外，请考虑通过替代 <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.InitializeResources%2A> 来更改形状的样式集。 这会更改所有形状字段的字体和画笔。

## <a name="customizing-image-fields"></a>自定义图像字段
 当你在形状中定义图像修饰器并定义图像形状时，该形状的显示区域由 ImageField 管理。 有关 ImageField 和其他 ShapeField 的初始化示例，请在 DSL 解决方案中查看 Dsl\GeneratedCode\Shapes.cs。

 ImageField 是一个对象，其管理形状内的区域，如分配给修饰器的空间。 一个 ImageField 实例在同一形状类的多个形状之间共享。 ImageField 实例不单独存储每个形状的图像：相反，`GetDisplayImage(ShapeElement)` 方法会将形状视为一个参数，并可以查找依赖于形状及其模型元素的当前状态的图像。

 如果需要特殊的行为，如可变图像，则可以创建你自己的派生自 ImageField 的类。

#### <a name="to-create-a-subclass-of-imagefield"></a>创建 ImageField 的子类

1. 在 DSL 定义中设置父形状类的“Generates Double Derived”属性。

2. 替代形状类的 `InitializeShapeFields` 方法。

    - 在 DSL 项目中创建新的代码文件，并为形状类编写分部类定义。 替代其中的方法定义。

3. 在 DSL\GeneratedCode\Shapes.cs. 中查看 `InitializeShapeFields` 的代码。

     在重写方法中，调用基方法，然后创建你自己的图像字段类的实例。 使用此项可以替换 `shapeFields` 列表中的常规图像字段。

## <a name="dynamic-icons"></a>动态图标
 此示例使图标更改依赖于形状的模型元素的状态。

> [!WARNING]
> 此示例演示如何生成动态图像修饰器。 但是，如果你只想在一个或两个图像之间切换（具体取决于模型变量的状态），则更简单的做法是创建多个图像修饰器，在形状上的同一位置找到它们，然后将可见性筛选器设置为依赖于模型变量的特定值。 若要设置此筛选器，请在 DSL 定义中选择形状映射，打开“DSL 详细信息”窗口，然后单击“修饰器”选项卡。

 若要运行此示例代码，请使用“最小语言”模板创建新的 DSL 解决方案。 将布尔域属性 `AlternateState` 添加到 ExampleElement 域类。 向 ExampleShape 类添加一个图标修饰器，并将其图像设置为位图文件。 单击“转换所有模板”。 在 DSL 项目中添加一个新的代码文件，并插入以下代码。

 若要测试代码，请按 F5，然后在调试解决方案中，打开示例关系图。 此时应显示图标的默认状态。 选择该形状，然后在“属性”窗口中，更改 AlternateState 属性的值。 该图标随后会在该形状上显示旋转 90 度。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
...
partial class ExampleShape
{
    /// <summary>
    /// Compose a list of the fields in this shape.
    /// Called once for each shape class.
    /// </summary>
    /// <param name="shapeFields"></param>
    protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);

      // Replace the image field:
      ShapeField oldField = ShapeElement.FindShapeField(shapeFields, "IconDecorator");
      shapeFields.Remove(oldField);
      // Must keep the same name:
      MyImageField newField = new MyImageField(oldField.Name);
      shapeFields.Add(newField);
      newField.DefaultImage = (oldField as ImageField).DefaultImage.Clone() as System.Drawing.Image;
    }
  }

  public class MyImageField : ImageField
  {
    public MyImageField(string tag) : base(tag) { }

    /// <summary>
    /// Get the image for this field in the given shape.
    /// </summary>
    public override System.Drawing.Image GetDisplayImage(ShapeElement parentShape)
    {
      ExampleElement element = parentShape.ModelElement as ExampleElement;
      if (element.AlternateState == true)
        return AlternateImage;
      else
        return base.GetDisplayImage(parentShape);
    }

    private System.Drawing.Image alternateImage;
    public System.Drawing.Image AlternateImage
    {
      get
      {
        if (alternateImage == null)
        {
          // Alternate image is a copy of the default, rotated by 90 degrees:
          alternateImage = this.DefaultImage.Clone() as System.Drawing.Image;
          alternateImage.RotateFlip(System.Drawing.RotateFlipType.Rotate90FlipNone);
        }
        return alternateImage;
      }
    }
  }
}
```

## <a name="see-also"></a>另请参阅

- [定义形状和连接线](../modeling/defining-shapes-and-connectors.md)
- [在图表上设置背景图像](../modeling/setting-a-background-image-on-a-diagram.md)
- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)