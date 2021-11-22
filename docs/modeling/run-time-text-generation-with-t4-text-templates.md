---
title: 使用 T4 文本模板的运行时文本生成
description: 了解如何使用 Visual Studio 运行时文本模板，在运行时在应用程序中生成文本字符串。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- Preprocessed Text Template project item
- TextTemplatingFilePreprocessor custom tool
- text templates, TransformText() method
- text templates, generating files at run time
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 0599c7739388b44bcbb0c6413a0ee4213ecd3797
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663903"
---
# <a name="run-time-text-generation-with-t4-text-templates"></a>使用 T4 文本模板的运行时文本生成

可以使用 Visual Studio 运行时文本模板，在运行时在应用程序中生成文本字符串。 执行应用程序的计算机不必有 Visual Studio。 运行时模板有时称为”预处理文本模板”，因为在编译时，模板会生成在运行时执行的代码。

每个模板都是显示在生成的字符串以及程序代码片段中的文本的组合。 程序片段为字符串的可变部分提供值，并控制条件和重复部分。

例如，以下模板可用于创建 HTML 报表的应用程序。

```html
<#@ template language="C#" #>
<html><body>
<h1>Sales for Previous Month</h2>
<table>
    <# for (int i = 1; i <= 10; i++)
       { #>
         <tr><td>Test name <#= i #> </td>
             <td>Test value <#= i * i #> </td> </tr>
    <# } #>
 </table>
This report is Company Confidential.
</body></html>
```

请注意，该模板是一个 HTML 页，其中的变量部分已替换为程序代码。 可以通过编写 HTML 页的静态原型来开始设计此类页。 然后，可以将表和其他变量部分替换为生成内容且随时变化的程序代码。

在应用程序中使用模板，可以更方便地查看输出的最终形式，而在一长串写语句中不能。 可以更容易且更可靠地对输出形式进行更改。

## <a name="creating-a-run-time-text-template-in-any-application"></a>在任何应用程序中创建运行时文本模板

### <a name="to-create-a-run-time-text-template"></a>创建运行时文本模板

1. 在“解决方案资源管理器”中，在你的项目的快捷菜单上，选择“添加” > “新建项目”。

2. 在“添加新项”对话框中，选择“运行时文本模板”。 （在 Visual Basic 中，查看“常用项” > “常规”的下方。）

3. 键入模板文件的名称。

    > [!NOTE]
    > 模板文件名将用作生成的代码中的类名。 因此，它不得包含空格或标点。

4. 选择“添加”。

    将创建一个扩展名为 .tt 的新文件。 其“自定义工具”属性设置为“TextTemplatingFilePreprocessor”。 它包含以下各行：

    ```
    <#@ template language="C#" #>
    <#@ assembly name="System.Core" #>
    <#@ import namespace="System.Linq" #>
    <#@ import namespace="System.Text" #>
    <#@ import namespace="System.Collections.Generic" #>
    ```

## <a name="converting-an-existing-file-to-a-run-time-template"></a>将现有文件转换为运行时模板

创建模板的一种好方法是转换输出的现有示例。 例如，如果应用程序将生成 HTML 文件，则可以首先创建一个纯 HTML 文件。 请确保其正常运行且其外观正确。 然后将其包含在 Visual Studio 项目中，并将其转换为模板。

### <a name="to-convert-an-existing-text-file-to-a-run-time-template"></a>将现有文本文件转换为运行时模板

1. 将该文件包含在 Visual Studio 项目中。 在“解决方案资源管理器”中，从项目的快捷菜单中选择“添加” > “现有项”。

2. 将该文件的“自定义工具”属性设置为“TextTemplatingFilePreprocessor”。 在“解决方案资源管理器”中，从该文件的快捷菜单中选择“属性”。

    > [!NOTE]
    > 如果已设置该属性，请确保它是“TextTemplatingFilePreprocessor”，而不是“TextTemplatingFileGenerator”。 如果包含已有扩展名 .tt 的文件，则可能出现这种情况。

3. 将文件扩展名更改为 .tt。 尽管此步骤是可选的，但它有助于避免在不正确的编辑器中打开文件。

4. 从文件名的主要部分中删除所有空格或标点。 例如，“My Web Page.tt”不正确，但“MyWebPage.tt”正确。 文件名将用作生成的代码中的类名。

5. 在文件开头插入以下行。 如果使用的是 Visual Basic 项目，请将“C#”替换为“VB”。

    `<#@ template language="C#" #>`

## <a name="the-content-of-the-run-time-template"></a>运行时模板的内容

### <a name="template-directive"></a>模板指令

使模板的第一行与创建文件时的内容相同：

`<#@ template language="C#" #>`

语言参数将取决于项目的语言。

### <a name="plain-content"></a>纯内容

编辑 .tt 文件以包含你希望应用程序生成的文本。 例如：

```html
<html><body>
<h1>Sales for January</h2>
<!-- table to be inserted here -->
This report is Company Confidential.
</body></html>
```

### <a name="embedded-program-code"></a>嵌入的程序代码

可以在 `<#` 和 `#>` 之间插入程序代码。 例如：

```csharp
<table>
    <# for (int i = 1; i <= 10; i++)
       { #>
         <tr><td>Test name <#= i #> </td>
             <td>Test value <#= i * i #> </td> </tr>
    <# } #>
 </table>
```

```vb
<table>
<#
    For i As Integer = 1 To 10
#>
    <tr><td>Test name <#= i #> </td>
      <td>Test value <#= i*i #> </td></tr>
<#
    Next
#>
</table>
```

请注意，在 `<# ... #>` 之间插入语句，在 `<#= ... #>` 之间插入表达式。 有关详细信息，请参阅[编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)。

## <a name="using-the-template"></a>使用模板

### <a name="the-code-built-from-the-template"></a>从模板生成的代码

保存 .tt 文件后，将生成附属 .cs 或 .vb 文件。 若要在“解决方案资源管理器”中查看此文件，请展开 .tt 节点。 在 Visual Basic 项目中，首先选择“解决方案资源管理器”工具栏中的“显示所有文件”。

请注意，附属文件包含一个分部类，其中包含名为 `TransformText()` 的方法。 可以从应用程序中调用此方法。

### <a name="generating-text-at-run-time"></a>在运行时生成文本

在应用程序代码中，可以使用如下所示的调用来生成模板的内容：

```csharp
MyWebPage page = new MyWebPage();
String pageContent = page.TransformText();
System.IO.File.WriteAllText("outputPage.html", pageContent);
```

```vb
Dim page = New My.Templates.MyWebPage
Dim pageContent = page.TransformText()
System.IO.File.WriteAllText("outputPage.html", pageContent)
```

若要将生成的类放入特定的命名空间中，请设置文本模板文件的“自定义工具命名空间”属性。

### <a name="debugging-runtime-text-templates"></a>调试运行时文本模板

使用与普通代码相同的方式调试和测试运行时文本模板。

可以在文本模板中设置断点。 如果在调试模式下从 Visual Studio 启动应用程序，则可以按常规方式单步执行代码并评估监视表达式。

### <a name="passing-parameters-in-the-constructor"></a>在构造函数中传递参数

通常，模板必须从应用程序的其他部分导入一些数据。 为了使此过程变得简单，模板生成的代码是一个分部类。 可以在项目的另一个文件中创建同一类的另一部分。 该文件可以包含具有参数、属性和函数的构造函数，该构造函数可通过嵌入在模板中的代码和应用程序的其余部分进行访问。

例如，可以创建单独的文件 MyWebPageCode.cs：

```csharp
partial class MyWebPage
{
    private MyData m_data;
    public MyWebPage(MyData data) { this.m_data = data; }}
```

在模板文件 MyWebPage.tt 中，可以编写：

```html
<h2>Sales figures</h2>
<table>
<# foreach (MyDataItem item in m_data.Items)
   // m_data is declared in MyWebPageCode.cs
   { #>
      <tr><td> <#= item.Name #> </td>
          <td> <#= item.Value #> </td></tr>
<# } // end of foreach
#>
</table>
```

若要在应用程序中使用此模板，请执行以下操作：

```csharp
MyData data = ...;
MyWebPage page = new MyWebPage(data);
String pageContent = page.TransformText();
System.IO.File.WriteAllText("outputPage.html", pageContent);
```

#### <a name="constructor-parameters-in-visual-basic"></a>Visual Basic 中的构造函数参数

在 Visual Basic 中，单独的文件 MyWebPageCode.vb 包含：

```vb
Namespace My.Templates
  Partial Public Class MyWebPage
    Private m_data As MyData
    Public Sub New(ByVal data As MyData)
      m_data = data
    End Sub
  End Class
End Namespace
```

模板文件可能包含：

```html
<#@ template language="VB" #>
<html><body>
<h1>Sales for January</h2>
<table>
<#
    For Each item In m_data.Items
#>
    <tr><td>Test name <#= item.Name #> </td>
      <td>Test value <#= item.Value #> </td></tr>
<#
    Next
#>
</table>
This report is Company Confidential.
</body></html>
```

可以通过在构造函数中传递参数来调用模板：

```vb
Dim data = New My.Templates.MyData
    ' Add data values here ....
Dim page = New My.Templates.MyWebPage(data)
Dim pageContent = page.TransformText()
System.IO.File.WriteAllText("outputPage.html", pageContent)
```

#### <a name="passing-data-in-template-properties"></a>在模板属性中传递数据

将数据传递到模板的替代方法是将公共属性添加到分部类定义中的模板类。 应用程序可以在调用 `TransformText()` 之前设置属性。

还可以将字段添加到分部定义中的模板类。 这样，你将能够在模板的后续执行之间传递数据。

### <a name="use-partial-classes-for-code"></a>对代码使用分部类

许多开发人员倾向于避免在模板中编写太多代码。 相反，可以在与模板文件同名的分部类中定义方法。 从模板调用这些方法。 通过这种方式，模板可以更清晰地显示目标输出字符串的外观。 有关结果外观的讨论可以从创建它所显示的数据的逻辑中分离出来。

### <a name="assemblies-and-references"></a>程序集和引用

如果希望模板代码引用 .NET 或其他程序集（如 System.Xml.dll），请按常规方式将其添加到项目的“引用”。

如果要以与 `using` 语句相同的方式导入命名空间，则可以使用 `import` 指令执行此操作：

```
<#@ import namespace="System.Xml" #>
```

这些指令必须置于文件的开头，紧跟在 `<#@template` 指令之后。

### <a name="shared-content"></a>共享内容

如果你有在多个模板之间共享的文本，则可以将其放入单独的文件中，并将其包含在应显示它的每个文件中：

```
<#@include file="CommonHeader.txt" #>
```

所含内容可以包含程序代码和纯文本的任何组合，并且可以包含其他 include 指令和其他指令。

include 指令可以在模板文件或包含文件的文本中的任何位置使用。

### <a name="inheritance-between-run-time-text-templates"></a>运行时文本模板之间的继承

可以通过编写基类模板（可以是抽象的）在运行时模板之间共享内容。 使用 `<@#template#>` 指令的 `inherits` 参数引用另一个运行时模板类。

#### <a name="inheritance-pattern-fragments-in-base-methods"></a>继承模式：基方法中的片段

在下面的示例使用的模式中，请注意以下几点：

- 基类 `SharedFragments` 定义类功能块 `<#+ ... #>` 中的方法。

- 基类不包含自由文本。 相反，所有文本块都出现在类功能方法内。

- 派生类调用 `SharedFragments` 中定义的方法。

- 应用程序调用派生类的 `TextTransform()` 方法，但不转换基类 `SharedFragments`。

- 基类和派生类都是运行时文本模板；也就是说，“自定义工具”属性设置为“TextTemplatingFilePreprocessor”。

SharedFragments.tt：

```
<#@ template language="C#" #>
<#+
protected void SharedText(int n)
{
#>
   Shared Text <#= n #>
<#+
}
// Insert more methods here if required.
#>
```

MyTextTemplate1.tt：

```
<#@ template language="C#" inherits="SharedFragments" #>
begin 1
   <# SharedText(2); #>
end 1
```

MyProgram.cs：

```csharp
...
MyTextTemplate1 t1  = new MyTextTemplate1();
string result = t1.TransformText();
Console.WriteLine(result);
```

结果输出：

```
begin 1
    Shared Text 2
end 1
```

#### <a name="inheritance-pattern-text-in-base-body"></a>继承模式：基体中的文本

在使用模板继承的此替代方法中，大量文本在基本模板中定义。 派生模板提供适合基本内容的数据和文本片段。

AbstractBaseTemplate1.tt：

```
<#@ template language="C#" #>

Here is the description for this derived template:
  <#= this.Description #>

Here is the fragment specific to this derived template:
<#
  this.PushIndent("  ");
  SpecificFragment(42);
  this.PopIndent();
#>
End of common template.
<#+
  // State set by derived class before calling TextTransform:
  protected string Description = "";
  // 'abstract' method to be defined in derived classes:
  protected virtual void SpecificFragment(int n) { }
#>
```

DerivedTemplate1.tt：

```
<#@ template language="C#" inherits="AbstractBaseTemplate1" #>
<#
  // Set the base template properties:
  base.Description = "Description for this derived class";

  // Run the base template:
  base.TransformText();

#>
End material for DerivedTemplate1.

<#+
// Provide a fragment specific to this derived template:

protected override void SpecificFragment(int n)
{
#>
   Specific to DerivedTemplate1 : <#= n #>
<#+
}
#>
```

应用程序代码：

```csharp
...
DerivedTemplate1 t1 = new DerivedTemplate1();
string result = t1.TransformText();
Console.WriteLine(result);
```

**结果输出：**

```
Here is the description for this derived template:
  Description for this derived class

Here is the fragment specific to this derived template:
     Specific to DerivedTemplate1 : 42
End of common template.
End material for DerivedTemplate1.
```

## <a name="related-topics"></a>相关主题

设计时模板：若要使用模板生成成为应用程序一部分的代码，请参阅[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)。

运行时模板可用于任何在编译时确定模板及其内容的应用程序。 但是，如果要编写从在运行时更改的模板生成文本的 Visual Studio 扩展，请参阅[在 VS 扩展中调用文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)。

## <a name="see-also"></a>另请参阅

- [代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)
- [编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)
- [T4 工具箱](http://olegsych.com/T4Toolbox/)
