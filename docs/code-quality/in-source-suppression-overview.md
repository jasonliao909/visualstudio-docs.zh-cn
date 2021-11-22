---
title: 禁止显示代码分析违规情况
ms.date: 05/10/2021
description: 了解如何在 Visual Studio 中禁止显示代码分析违规情况。 了解如何使用 SuppressMessageAttribute 特性进行源内禁止显示。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- source suppression, code analysis
- code analysis, source suppression
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-code-analysis
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.openlocfilehash: a509aa12f59298af97245647bd971a7272ffcaef
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129968171"
---
# <a name="suppress-code-analysis-violations"></a>禁止显示代码分析违规情况

指示警告不适用通常很有用。 这向团队成员指示已评审代码，并且可以禁止显示警告。 本文介绍使用 Visual Studio IDE 禁止显示代码分析违规情况的不同方法。

::: moniker range=">=vs-2019"

## <a name="suppress-violations-using-the-editorconfig-file"></a>使用 EditorConfig 文件禁止显示违规情况

在 EditorConfig 文件中，将严重性设置为 `none`，例如 `dotnet_diagnostic.CA1822.severity = none`。 若要添加 EditorConfig 文件，请参阅[将 EditorConfig 文件添加到项目](../ide/create-portable-custom-editor-options.md#add-and-remove-editorconfig-files)。

::: moniker-end

## <a name="suppress-violations-in-source-code"></a>禁止显示源代码中的违规情况

可以使用预处理器指令、[#pragma 警告 (C#)](/dotnet/csharp/language-reference/preprocessor-directives#pragma-warning) 或[禁用 (Visual Basic)](/dotnet/visual-basic/language-reference/directives/disable-enable) 指令禁止显示代码中的违规情况以禁止显示仅特定代码行的警告。 也可以使用 [SuppressMessage 特性](#in-source-suppression-and-the-suppressmessage-attribute)。

- 从“代码编辑器”中

  将光标放在有冲突的代码行中，然后按 Ctrl+句点 (.) 打开“快速操作”菜单  。 选择“禁止显示 CAXXXX”，然后选择“在源中”或“在源中(特性)”。

  如果选择“在源中”，则会看到将添加到代码的预处理器指令的预览。

  ::: moniker range="vs-2017"
  :::image type="content" source="media/suppress-diagnostic-from-editor.png" alt-text="从“快速操作”菜单中禁止显示诊断":::
  ::: moniker-end
  ::: moniker range=">=vs-2019"
  :::image type="content" source="media/vs-2019/suppress-diagnostic-from-editor.png" alt-text="从“快速操作”菜单中禁止显示诊断":::

  如果选择“在源中(特性)”，则会看到将添加到代码的 [SuppressMessage 特性](#in-source-suppression-and-the-suppressmessage-attribute)的预览。

  :::image type="content" source="media/vs-2019/suppress-diagnostic-from-editor-attribute.png" alt-text="使用特性从“快速操作”菜单中禁止显示诊断":::
  ::: moniker-end

- 从“错误列表”中

  选择要禁止显示的规则，然后右键单击并选择“禁止显示” > “在源中” 。

  - 如果“在源中”禁止显示，将打开“预览更改”对话框，并显示添加到源代码中的 C# [#pragma warning](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning) 或 Visual Basic [#Disable warning](/dotnet/visual-basic/language-reference/directives/directives) 指令的预览 。

    ![在代码文件中添加 #pragma warning 的预览](media/pragma-warning-preview.png)

  在“预览更改”对话框中，选择“应用” 。

  > [!NOTE]
  > 如果在“解决方案资源管理器”中没有看到“禁止显示”菜单选项，则冲突可能来自生成而非实时分析 。 “错误列表”显示来自实时代码分析和生成的诊断或规则冲突。 由于生成诊断可能已过时（例如已编辑代码以修复冲突，但尚未重新生成），无法从“错误列表”中禁止显示这些诊断。 来自实时分析或 IntelliSense 的诊断始终是当前源的最新诊断，可以从“错误列表”中禁止显示。 若要从所选内容中排除“生成”诊断，请将“错误列表”源筛选器从“生成 + IntelliSense”切换到“仅 IntelliSense”  。 然后，选择要禁止显示的诊断并按前面所述继续操作。
  >
  > ![Visual Studio 中的错误列表源筛选器](media/error-list-filter.png)

## <a name="suppress-violations-using-a-global-suppression-file"></a>使用全局禁止显示文件禁止显示违规情况

[全局禁止显示文件](#global-level-suppressions)使用 [SuppressMessage 特性](#in-source-suppression-and-the-suppressmessage-attribute)。

- 从“错误列表”中选择要禁止显示的规则，然后右键单击并选择“禁止显示” > “在禁止显示文件中”。 将打开“预览更改”对话框，并显示添加到全局禁止显示文件的 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性的预览。

  ![向禁止显示文件添加 SuppressMessage 属性的预览](media/preview-changes-in-suppression-file.png)

- 从“代码编辑器”将光标放在有违规情况的代码行中，然后按“快速操作和重构”（或按 Ctrl+句点 (.)）打开“快速操作”菜单   。 选择“禁止显示 CAXXXX”，然后选择“在禁止显示文件中”。 你会看到将创建或修改的[全局禁止显示文件](#global-level-suppressions)的预览。

::: moniker range=">=vs-2019"

- 从“分析”菜单中，在菜单栏上选择“分析” > “生成并禁止显示待处理的问题”，以禁止显示所有当前违规情况。 有时这称为“基线”。

::: moniker-end
::: moniker range="vs-2017"

- 从“分析”菜单中，在菜单栏上选择“分析” > “运行代码分析并禁止显示待处理的问题”，以禁止显示所有当前违规情况。 有时这称为“基线”。
::: moniker-end

## <a name="suppress-violations-using-project-settings"></a>使用项目设置禁止显示违规情况

从“解决方案资源管理器”中，打开项目的属性（右键单击该项目）并选择“属性”（或按 Alt + Enter）并使用“代码分析”选项卡配置选项。 例如，可以禁用实时代码分析或禁用 .NET 分析器。

## <a name="suppress-violations-using-a-rule-set"></a>使用规则集禁止显示违规情况

从“规则集编辑器”中，清除其名称旁边的复选框，或将“操作”设置为“无”。

## <a name="in-source-suppression-and-the-suppressmessage-attribute"></a>源内禁止显示和 SuppressMessage 特性

源内禁止显示 (ISS) 使用 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性来禁止显示警告。 该特性可以放置在生成警告的代码段附近。 可以通过键入 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性将其添加到源文件，也可以使用“错误列表”中的警告上的快捷菜单自动添加它。

<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性是一个条件特性，它包含在托管代码程序集的 IL 元数据中，CODE_ANALYSIS 编译符号在编译时定义。

在 C++/CLI 中，在头文件中使用宏 CA\_SUPPRESS\_MESSAGE 或 CA\_GLOBAL\_SUPPRESS_MESSAGE 来添加特性。

> [!NOTE]
> 不应在发布版本上使用源内禁止显示，以防止意外传送源内禁止显示元数据。 此外，由于源内禁止显示的处理成本，应用程序的性能可能会下降。

::: moniker range="vs-2017"

> [!NOTE]
> 如果将项目迁移到 Visual Studio 2017，可能会突然看到大量代码分析警告。 如果尚未准备好处理警告，可选择“分析” > “运行代码分析并禁止显示待处理的问题”来禁止显示所有警告 。
>
> ![在 Visual Studio 中运行代码分析并禁止显示问题](media/suppress-active-issues.png)

::: moniker-end

::: moniker range=">=vs-2019"

> [!NOTE]
> 如果将项目迁移到 Visual Studio 2019，可能会突然看到大量代码分析警告。 如果尚未准备好处理警告，可选择“分析” > “生成并禁止显示待处理的问题”来禁止显示所有警告 。

::: moniker-end

### <a name="suppressmessage-attribute"></a>SuppressMessage 特性

从“错误列表”中的代码分析警告的上下文或右键单击菜单中选择“禁止显示”时，<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性会添加到代码中或项目的全局禁止显示文件。

<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性采用以下格式：

```vb
<Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")>
```

```csharp
[Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")]
```

```cpp
CA_SUPPRESS_MESSAGE("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")
```

该特性的属性包括：

- **类别** - 定义规则的类别。 有关代码分析规则类别的信息，请参阅[托管代码警告](/dotnet/fundamentals/code-analysis/quality-rules/index)。

- **CheckId** - 规则的标识符。 支持包括规则标识符的短名称和长名称。 短名称为 CAXXXX；长名称为 CAXXXX:FriendlyTypeName。

- **理由** - 用于记录禁止显示消息的原因的文本。

- **MessageId** - 每条消息的问题的唯一标识符。

- **范围** - 要禁止显示警告的目标。 如果未指定目标，则设置为特性的目标。 支持的[范围](xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope)包括以下内容：

  - [`module`](#module-suppression-scope) - 此范围禁止显示针对程序集的警告。 它是应用于整个项目的全局禁止显示。

  - `resource` -（仅[旧版 FxCop](../code-quality/static-code-analysis-for-managed-code-overview.md)）此范围禁止显示在写入到属于模块（程序集）一部分的资源文件中的诊断信息的警告。 在仅分析源文件的 Roslyn 分析器诊断的 C#/VB 编译器中不读取/遵守此范围。

  - `type` - 此范围禁止显示针对类型的警告。

  - `member` - 此范围禁止显示针对成员的警告。

  - `namespace` - 此范围禁止显示针对命名空间本身的警告。 它不会禁止显示针对命名空间中的类型的警告。

  - `namespaceanddescendants`-（需要编译器版本 3.x 或更高版本以及 Visual Studio 2019）此范围禁止显示命名空间及其所有后代符号中的警告。 旧版分析将忽略 `namespaceanddescendants` 值。

- **目标** - 一个标识符，用于指定要禁止显示警告的目标。 它必须包含完全限定的项名称。

在 Visual Studio 中看到警告时，可以通过[向全局禁止显示文件添加禁止显示](../code-quality/use-roslyn-analyzers.md#suppress-violations)来查看 `SuppressMessage` 的示例。 禁止显示特性及其必需属性显示在预览窗口中。

### <a name="suppressmessage-usage"></a>SuppressMessage 用法

代码分析警告在应用 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性的级别禁止显示。 例如，可以在程序集、模块、类型、成员或参数级别应用该特性。 这样做的目的是将禁止显示信息与发生违规情况的代码紧密耦合。

禁止显示的一般形式包括规则类别和规则标识符，其中包含规则名称的可选人工可读取的表示形式。 例如：

`[SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`

如果出于严格的性能原因来最小化源内禁止显示元数据，可以省略规则名称。 规则类别及其规则 ID 共同构成了足够唯一的规则标识符。 例如：

`[SuppressMessage("Microsoft.Design", "CA1039")]`

出于可维护性原因，不建议省略规则名称。

### <a name="suppress-selective-violations-within-a-method-body"></a>禁止显示方法主体中的选择性违规情况

禁止显示特性可以应用于方法，但不能嵌入在方法主体中。 这意味着，如果将 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性添加到方法，将禁止显示特定规则的所有违规情况。

在某些情况下，你可能想要禁止显示特定违规情况的实例，例如，这样以后的代码不会自动从代码分析规则中免除。 某些代码分析规则允许通过使用 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性的 `MessageId` 属性来这样做。 通常，针对特定符号（局部变量或参数）的违规情况的旧规则遵守 `MessageId` 属性。 [CA1500:VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md) 就是此类规则的一个示例。 但是，针对可执行代码（非符号）的违规情况的旧规则不遵守 `MessageId` 属性。 此外，.NET Compiler Platform（“Roslyn”）分析器不遵守 `MessageId` 属性。

若要禁止规则的特定符号违规情况，请为 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性的 `MessageId` 属性指定符号名称。 以下示例显示了存在两次 [CA1500:VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md) 违规情况的代码 &mdash; 一次是针对 `name` 变量，另一次是针对 `age` 变量。 仅禁止显示 `age` 符号的违规情况。

```vb
Public Class Animal
    Dim age As Integer
    Dim name As String

    <CodeAnalysis.SuppressMessage("Microsoft.Maintainability", "CA1500:VariableNamesShouldNotMatchFieldNames", MessageId:="age")>
    Sub PrintInfo()
        Dim age As Integer = 5
        Dim name As String = "Charlie"

        Console.WriteLine("Age {0}, Name {1}", age, name)
    End Sub

End Class
```

```csharp
public class Animal
{
    int age;
    string name;

    [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Maintainability", "CA1500:VariableNamesShouldNotMatchFieldNames", MessageId = "age")]
    private void PrintInfo()
    {
        int age = 5;
        string name = "Charlie";

        Console.WriteLine($"Age {age}, Name {name}");
    }
}
```

### <a name="global-level-suppressions"></a>全局级禁止显示

托管代码分析工具检查在程序集、模块、类型、成员或参数级别应用的 `SuppressMessage` 特性。 它还针对资源和命名空间触发违规情况。 这些违规情况必须在全局级别应用，并且具有范围和目标。 例如，以下消息禁止显示命名空间违规情况：

`[module: SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "MyNamespace")]`

> [!NOTE]
> 禁止显示具有 `namespace` 范围的警告时，会禁止显示针对命名空间本身的警告。 它不会禁止显示针对命名空间中的类型的警告。

可以通过指定显式范围来表示任何禁止显示。 这些禁止显示必须位于全局级别。 不能通过修饰类型来指定成员级别的禁止显示。

全局级别的禁止显示是禁止显示引用编译器生成的代码的消息的唯一方法，这些代码未映射到显式提供的用户源。 例如，下面的代码将抑制针对编译器发出的构造函数的冲突：

`[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="Microsoft.Tools.FxCop.Type..ctor()")]`

> [!NOTE]
> `Target` 始终包含完全限定的项名称。

#### <a name="global-suppression-file"></a>全局禁止显示文件

全局禁止显示文件保留全局级别的禁止显示或未指定目标的禁止显示。 例如，程序集级别的违规情况的禁止显示存储在此文件中。 此外，一些 ASP.NET 禁止显示存储在此文件中，因为项目级别的设置不适用于窗体后面的代码。 第一次在“错误列表”窗口中选择“禁止显示”命令的“在项目禁止显示文件中”选项时，会创建一个全局禁止显示文件并将其添加到你的项目中。

#### <a name="module-suppression-scope"></a>模块禁止显示范围

可以使用模块范围禁止显示整个程序集的代码质量违规情况。

例如，GlobalSuppressions 项目文件中的以下特性将禁止显示 ASP.NET Core 项目的 ConfigureAwait 违规情况：

`[assembly: System.Diagnostics.CodeAnalysis.SuppressMessage("Reliability", "CA2007:Consider calling ConfigureAwait on the awaited task", Justification = "ASP.NET Core doesn't use thread context to store request context.", Scope = "module")]`

### <a name="generated-code"></a>生成的代码

托管代码编译器和某些第三方工具会生成代码，以便加快代码开发速度。 在源文件中出现的编译器生成的代码通常使用 `GeneratedCodeAttribute` 特性进行标记。

对于源代码分析，可以在 `.editorconfig` 文件中禁止显示生成的代码中的消息。 有关详细信息，请参阅[排除生成的代码](/dotnet/fundamentals/code-analysis/configuration-options#exclude-generated-code)。

对于旧版代码分析，可以选择是否禁止显示生成的代码的代码分析警告和错误。 有关如何禁止显示此类警告和错误的信息，请参阅[如何：禁止显示生成的代码的警告](../code-quality/how-to-suppress-code-analysis-warnings-for-generated-code.md)。

> [!NOTE]
> 当 `GeneratedCodeAttribute` 应用于整个程序集或单个参数时，代码分析会忽略它。

## <a name="see-also"></a>另请参阅

- <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope>
- <xref:System.Diagnostics.CodeAnalysis>
- [使用代码分析器](../code-quality/use-roslyn-analyzers.md)
