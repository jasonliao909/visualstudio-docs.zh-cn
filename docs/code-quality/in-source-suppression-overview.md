---
title: 禁止显示代码分析违规情况
ms.date: 05/10/2021
description: 了解如何在代码中禁止显示代码Visual Studio。 了解如何使用 SuppressMessageAttribute 属性进行源内抑制。
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

指示警告不适用通常很有用。 这向团队成员指示已评审代码，并且可以禁止显示警告。 本文介绍使用 IDE 取消代码分析冲突Visual Studio方式。

::: moniker range=">=vs-2019"

## <a name="suppress-violations-using-the-editorconfig-file"></a>使用 EditorConfig 文件禁止冲突

在 **EditorConfig 文件中**，将严重性设置为 `none` ，例如 `dotnet_diagnostic.CA1822.severity = none` 。 若要添加 EditorConfig 文件，请参阅 [将 EditorConfig 文件添加到项目](../ide/create-portable-custom-editor-options.md#add-and-remove-editorconfig-files)。

::: moniker-end

## <a name="suppress-violations-in-source-code"></a>禁止显示源代码中的冲突

可以使用预处理器指令、#pragma 警告[ (C#) ](/dotnet/csharp/language-reference/preprocessor-directives#pragma-warning)或禁用[ (Visual Basic) ](/dotnet/visual-basic/language-reference/directives/disable-enable)指令在代码中取消冲突，以仅禁止显示特定代码行的警告。 或者，可以使用 [SuppressMessage 属性](#in-source-suppression-and-the-suppressmessage-attribute)。

- 从 **代码编辑器**

  将光标置于具有冲突的代码行中，然后按 **Ctrl** + **Period (.)** 打开"**快速操作"** 菜单。 选择 **"取消 CAXXXX"，** 然后选择 **"源** "或"源 (**属性) "**。

  如果在" **源"中选择**，则会看到预处理器指令的预览，该指令将添加到代码中。

  ::: moniker range="vs-2017"
  :::image type="content" source="media/suppress-diagnostic-from-editor.png" alt-text="从快速操作菜单取消诊断":::
  ::: moniker-end
  ::: moniker range=">=vs-2019"
  :::image type="content" source="media/vs-2019/suppress-diagnostic-from-editor.png" alt-text="从快速操作菜单取消诊断":::

  如果在" **源" (属性**) ，则会看到将添加到代码中的 [SuppressMessage](#in-source-suppression-and-the-suppressmessage-attribute) 属性的预览。

  :::image type="content" source="media/vs-2019/suppress-diagnostic-from-editor-attribute.png" alt-text="使用属性禁止从快速操作菜单进行诊断":::
  ::: moniker-end

- 从 **错误列表中**

  选择要取消的规则，然后右键单击并选择"在源 **中**  >  **禁止显示"。**

  - 如果取消 **"在源中"，"** 预览更改"对话框将打开，并#pragma [C#](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning) Visual Basic#Disable [添加到](/dotnet/visual-basic/language-reference/directives/directives)源代码的警告指令的预览。 

    ![在代码#pragma添加警告的预览](media/pragma-warning-preview.png)

  在"**预览更改"** 对话框中，选择"应用 **"。**

  > [!NOTE]
  > 如果未在"取消"菜单中看到"取消"解决方案资源管理器，**则** 冲突可能来自生成，而不是实时分析。 " **错误列表** "显示实时代码分析和生成中的诊断或规则冲突。 例如，由于生成诊断可能过时，因此，如果已编辑代码来修复冲突，但尚未重新生成，则不能从错误列表 取消这些 **诊断**。 实时分析或 IntelliSense 中的诊断始终与当前源一样最新，可以从错误 **列表 取消。** 若要从 *所选* 内容中排除生成诊断，将"错误 **列表**"源筛选器从"生成 **+ IntelliSense"** 切换为"**仅 IntelliSense"。** 然后，选择要取消的诊断，然后按前面所述继续。
  >
  > ![错误列表中源筛选器Visual Studio](media/error-list-filter.png)

## <a name="suppress-violations-using-a-global-suppression-file"></a>使用全局抑制文件抑制冲突

全局 [抑制文件使用](#global-level-suppressions) [SuppressMessage 属性](#in-source-suppression-and-the-suppressmessage-attribute)。

- 从"**错误列表"** 中，选择要取消的规则，然后右键单击并选择"抑制  >  **文件"中的"禁止显示"。** " **预览更改** "对话框随即打开，其中显示了添加到全局抑制 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 文件的属性预览。

  ![将 SuppressMessage 属性添加到抑制文件的预览](media/preview-changes-in-suppression-file.png)

- 在代码编辑器中，将光标置于具有冲突的代码行中，然后按"快速操作和 **重构" (** 或按 **Ctrl** + **Period (.)**) 打开"**快速操作**"菜单。 选择 **"取消 CAXXXX"，** 然后在" **抑制文件"中选择**。 你会看到将创建 [或修改的](#global-level-suppressions) 全局抑制文件的预览。

::: moniker range=">=vs-2019"

- 在"**分析"** 菜单中，**选择菜单** 栏上的"分析生成和抑制活动问题  >  "，以禁止显示所有当前冲突。 这有时称为"基线"。

::: moniker-end
::: moniker range="vs-2017"

- 在"**分析"** 菜单中，**选择"分析** Code Analysis"菜单栏上的"禁止显示活动问题"，  >  以禁止显示所有当前冲突。 这有时称为"基线"。
::: moniker-end

## <a name="suppress-violations-using-project-settings"></a>使用项目设置禁止冲突

在 **解决方案资源管理器** 中，打开项目的属性 (右键单击该项目并选择"**属性" (** 或按 Alt + **Enter**) 并使用"Code Analysis"**选项卡配置** 选项。 例如，可以禁用实时代码分析或禁用 .NET 分析器。

## <a name="suppress-violations-using-a-rule-set"></a>使用规则集禁止冲突

在规则 **集编辑器中**，清除其名称旁边的复选框，或将"**操作"** 设置为"无 **"。**

## <a name="in-source-suppression-and-the-suppressmessage-attribute"></a>源内抑制和 SuppressMessage 属性

ISS (源) <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 使用 属性来禁止显示警告。 属性可以放置在生成警告的代码段附近。 可以通过键入属性将属性添加到源文件，或者可以使用"错误列表"中的警告上的快捷菜单 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 自动添加它。 

属性是一个条件属性，它包含在托管代码程序集的 IL 元数据中，CODE_ANALYSIS编译符号 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 在编译时定义。

在 C++/CLI 中，使用标头SUPPRESS_MESSAGE CA SUPPRESS MESSAGE 或 \_ \_ CA GLOBAL \_ \_ 命令来添加 属性。

> [!NOTE]
> 不应在发布版本上使用源内抑制，以防止意外交付源内抑制元数据。 此外，由于源内抑制的处理成本，应用程序的性能可能会下降。

::: moniker range="vs-2017"

> [!NOTE]
> 如果将项目迁移到 2017 Visual Studio，可能会突然面临大量代码分析警告。 如果还没有准备好修复警告，可以通过选择"分析运行状态"和"禁止Code Analysis  >  **取消显示所有警告**。
>
> ![运行代码分析并禁止显示Visual Studio](media/suppress-active-issues.png)

::: moniker-end

::: moniker range=">=vs-2019"

> [!NOTE]
> 如果将项目迁移到 2019 Visual Studio，可能会突然面临大量代码分析警告。 如果还没有准备好修复警告，可以通过选择"分析生成"和"禁止活动问题"来  >  **取消显示所有这些警告**。

::: moniker-end

### <a name="suppressmessage-attribute"></a>SuppressMessage 特性

在 **"错误** 列表"中选择代码分析警告的上下文或右键单击菜单时，会向代码或项目的全局抑制文件添加 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性。

<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute>属性采用以下格式：

```vb
<Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")>
```

```csharp
[Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")]
```

```cpp
CA_SUPPRESS_MESSAGE("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")
```

属性的属性包括：

- **类别** - 定义规则的类别。 有关代码分析规则类别的信息，请参阅 [托管代码警告](/dotnet/fundamentals/code-analysis/quality-rules/index)。

- **CheckId** - 规则的标识符。 支持包括规则标识符的短名称和长名称。 短名称为 CAXXXX;长名称为 CAXXXX：FriendlyTypeName。

- **理由** - 用于记录取消消息原因的文本。

- **MessageId** - 每条消息的问题的唯一标识符。

- **范围** - 要禁止显示警告的目标。 如果未指定目标，则设置为属性的目标。 支持 [的范围](xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope) 包括：

  - [`module`](#module-suppression-scope) - 此范围禁止显示针对程序集的警告。 它是应用于整个项目的全局抑制。

  - `resource` - (旧版 [FxCop](../code-quality/static-code-analysis-for-managed-code-overview.md)) 此范围禁止在写入到属于模块程序集的模块的一部分的资源文件的诊断信息 (警告) 。 在仅分析源文件的 Roslyn 分析器诊断的 C#/VB编译器中不读取/遵守此范围。

  - `type` - 此范围禁止显示针对类型的警告。

  - `member` - 此范围禁止显示针对成员发出的警告。

  - `namespace` - 此范围禁止显示针对命名空间本身的警告。 它不会禁止显示针对命名空间中的类型的警告。

  - `namespaceanddescendants`- (编译器版本 3.x 或更高版本以及 Visual Studio 2019) 此范围禁止命名空间及其所有子代符号中的警告。 旧 `namespaceanddescendants` 分析将忽略该值。

- **目标** - 一个标识符，用于指定要禁止显示警告的目标。 它必须包含完全限定的项名称。

在全局抑制文件中Visual Studio警告时，可以通过向全局抑制文件 添加抑制来 `SuppressMessage` [查看 的示例](../code-quality/use-roslyn-analyzers.md#suppress-violations)。 抑制属性及其必需属性显示在预览窗口中。

### <a name="suppressmessage-usage"></a>SuppressMessage 用法

Code Analysis属性应用到的级别取消显示 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 警告。 例如，可以在程序集、模块、类型、成员或参数级别应用 属性。 这样做的目的是将抑制信息与发生冲突的代码紧密耦合。

抑制的一般形式包括规则类别和规则标识符，其中包含规则名称的可选可读表示形式。 例如：

`[SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`

如果出于严格的性能原因来最小化源内抑制元数据，可以省略规则名称。 规则类别及其规则 ID 共同构成了足够唯一的规则标识符。 例如：

`[SuppressMessage("Microsoft.Design", "CA1039")]`

出于可维护性原因，不建议省略规则名称。

### <a name="suppress-selective-violations-within-a-method-body"></a>取消方法主体中的选择性冲突

抑制特性可以应用于方法，但不能嵌入在方法体中。 这意味着，如果将 属性添加到 方法，将禁止特定规则 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 的所有冲突。

在某些情况下，你可能想要禁止显示特定冲突实例，例如，这样以后的代码不会自动从代码分析规则中免除。 某些代码分析规则允许通过使用 属性的 属性 `MessageId` 来 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 这样做。 通常，特定符号冲突的旧规则 (局部变量或参数) 属性 `MessageId` 。 [CA1500：VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md) 就是此类规则的一个示例。 但是，针对非符号 (代码冲突的旧) 不遵守 `MessageId` 属性。 此外，.NET Compiler Platform (分析器) "Roslyn"属性 `MessageId` 。

若要禁止与规则的特定符号冲突，请为属性的 `MessageId` 属性指定符号 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 名称。 以下示例显示的代码与[CA1500：VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md)的两个冲突一个针对变量，一 &mdash; `name` 个针对 `age` 变量。 仅禁止显示 `age` 符号冲突。

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

### <a name="global-level-suppressions"></a>全局级抑制

托管代码分析工具检查在程序集、模块、类型、成员或参数 `SuppressMessage` 级别应用的属性。 它还针对资源和命名空间触发冲突。 这些冲突必须在全局级别应用，并且具有作用域和目标。 例如，以下消息禁止显示命名空间冲突：

`[module: SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "MyNamespace")]`

> [!NOTE]
> 禁止显示具有作用域的 `namespace` 警告时，会禁止显示针对命名空间本身的警告。 它不会禁止对命名空间中的类型显示警告。

可以通过指定显式范围来表示任何抑制。 这些抑制必须位于全局级别。 不能通过修饰类型来指定成员级抑制。

全局级抑制是禁止显示引用编译器生成的代码的消息的唯一方法，这些代码未映射到显式提供的用户源。 例如，下面的代码将抑制针对编译器发出的构造函数的冲突：

`[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="Microsoft.Tools.FxCop.Type..ctor()")]`

> [!NOTE]
> `Target` 始终包含完全限定的项名称。

#### <a name="global-suppression-file"></a>全局抑制文件

全局抑制文件保留全局级抑制或未指定目标的抑制。 例如，程序集级违规的抑制存储在此文件中。 此外，ASP.NET 抑制存储在此文件中，因为项目级设置不适用于窗体后面的代码。 第一次在"错误列表"窗口中选择"禁止显示"命令的"in **Project Suppress File"** 选项时，会创建全局抑制文件并 **添加到项目中。**

#### <a name="module-suppression-scope"></a>模块抑制范围

可以使用模块范围禁止显示整个程序集的代码 **质量** 冲突。

例如 _，GlobalSuppressions_ 项目文件中的以下属性将禁止显示项目项目的 ConfigureAwait ASP.NET Core冲突：

`[assembly: System.Diagnostics.CodeAnalysis.SuppressMessage("Reliability", "CA2007:Consider calling ConfigureAwait on the awaited task", Justification = "ASP.NET Core doesn't use thread context to store request context.", Scope = "module")]`

### <a name="generated-code"></a>生成的代码

托管代码编译器和某些第三方工具会生成代码，以便加快代码开发速度。 在源文件中出现的编译器生成的代码通常使用 属性 `GeneratedCodeAttribute` 进行标记。

对于源代码分析，可以在文件中禁止显示生成的代码中 `.editorconfig` 的消息。 有关详细信息，请参阅排除 [生成的代码](/dotnet/fundamentals/code-analysis/configuration-options#exclude-generated-code)。

对于旧版代码分析，可以选择是否禁止显示生成的代码的代码分析警告和错误。 若要了解如何禁止显示此类警告和错误，请参阅 [如何：禁止显示生成的代码的警告](../code-quality/how-to-suppress-code-analysis-warnings-for-generated-code.md)。

> [!NOTE]
> 当代码分析 `GeneratedCodeAttribute` 应用于整个程序集或单个参数时，代码分析将忽略它。

## <a name="see-also"></a>另请参阅

- <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope>
- <xref:System.Diagnostics.CodeAnalysis>
- [使用代码分析器](../code-quality/use-roslyn-analyzers.md)
