---
title: 域特定语言入门
description: 了解定义和使用通过 Visual Studio 的建模 SDK 创建的域特定语言 (DSL) 的基本概念。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 8c9e471f3e72568ceb60c3831357548201b69433
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664170"
---
# <a name="get-started-with-domain-specific-languages"></a>域特定语言入门

本主题介绍了定义和使用通过 Visual Studio 的建模 SDK 创建的域特定语言 (DSL) 的基本概念。

> [!NOTE]
> 安装 Visual Studio 的特定功能时，会自动安装文本模板转换 SDK 和 Visual Studio 建模 SDK。 有关更多详细信息，请参阅[这篇博客文章](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)。

如果你是 DSL 的初学者，建议浏览 DSL 工具实验室，可在此站点中找到：[可视化和建模 SDK](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)

## <a name="what-can-you-do-with-a-domain-specific-language"></a>使用域特定语言可以做什么？

域特定语言是一种表示法，通常用图表示，旨在用于特定目的。 相比之下，UML 等语言是通用的。 在 DSL 中，可以定义模型元素的类型及其关系，以及它们在屏幕上的呈现方式。

设计 DSL 后，可以将其作为 Visual Studio 集成扩展 (VSIX) 包的一部分进行分发。 用户在 Visual Studio 中使用 DSL：

![家谱关系图、工具箱和资源管理器](../modeling/media/familyt_instance.png)

表示法只是 DSL 的一部分。 VSIX 包与表示法一起包含一些工具，用户可以应用这些工具来帮助他们编辑和生成模型中的材料。

DSL 的主要应用之一是生成程序代码、配置文件和其他工件。 尤其是在将创建产品的多个变体的大型项目和产品系列中，从 DSL 生成许多可变方面可以明显提高可靠性，并快速响应需求变化。

本概述的其余部分是一个演练，介绍了在 Visual Studio 中创建和使用域特定语言的基本操作。

## <a name="prerequisites"></a>先决条件

若要定义 DSL，必须安装以下组件：

| 组件 | 链接 |
|-|-|
| Visual Studio | [http://go.microsoft.com/fwlink/?LinkId=185579](https://visualstudio.microsoft.com) |
| [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] | [https://go.microsoft.com/fwlink/?linkid=2166172](../extensibility/visual-studio-sdk.md) |
| Visual Studio 的建模 SDK | |

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="create-a-dsl-solution"></a>创建 DSL 解决方案

若要创建新的域特定语言，请使用域特定语言项目模板创建新的 Visual Studio 解决方案。

1. 在 **“文件”** 菜单上，指向 **“新建”** ，再单击 **“项目”** 。

2. 在“项目类型”下展开“其他项目类型”节点，然后单击“扩展性”。

3. 单击“特定于域的语言设计器”。

     ![“创建 DSL”对话框](../modeling/media/create_dsldialog.png)

4. 在“名称”框中，键入 FamilyTree。 单击 **“确定”** 。

     将打开“域特定语言向导”，并显示模板 DSL 解决方案列表。

     单击每个模板以查看说明。

     模板是有用的起点。 每个模板都提供了一个可正常工作的完整 DSL，你可以对其进行编辑以满足需求。 通常，可以选择最接近你要创建的内容的模板。

5. 对于本演练，请选择“最小语言”模板。

6. 在相应的向导页中输入 DSL 的文件扩展名。 这是包含 DSL 的实例的文件将使用的扩展名。

    - 选择与你的计算机（或想要在其中安装 DSL 的任何计算机）中的任何应用程序都不关联的扩展名。 例如，docx 和 htm 是不可接受的文件扩展名 。

    - 如果你输入的扩展名已用作 DSL，则该向导将向你发出警告。 请考虑使用不同的文件扩展名。 还可以重置 Visual Studio SDK 实验实例以清除旧的实验设计器。 依次单击“开始”、“所有程序”、“Microsoft Visual Studio 2010 SDK”、“工具”，然后单击“重置 Microsoft Visual Studio 2010 实验实例”    。

7. 检查其他页面，然后单击“完成”。

     将生成包含两个项目的解决方案。 它们名为 Dsl 和 DslPackage。 随即打开名为 DslDefinition.dsl 的关系图文件。

    > [!NOTE]
    > 在这两个项目的文件夹中可以看到的大部分代码都是从 DslDefinition.dsl 生成的。 因此，对 DSL 所做的大多数修改都是在此文件中进行的。

用户界面现在类似于下图。

![dsl 设计器](../modeling/media/dsl_designer.png)

此解决方案将定义域特定语言。 有关详细信息，请参阅[特定于域的语言工具用户界面的概述](../modeling/overview-of-the-domain-specific-language-tools-user-interface.md)。

## <a name="the-important-parts-of-the-dsl-solution"></a>DSL 解决方案的重要部分

请注意新解决方案的以下方面：

- **Dsl\DslDefinition.dsl** 这是创建 DSL 解决方案时看到的文件。 解决方案中的几乎所有代码都是从此文件生成的，对 DSL 定义进行的大多数更改都在此处进行。 有关详细信息，请参阅[使用 DSL 定义关系图](../modeling/working-with-the-dsl-definition-diagram.md)。

- **Dsl 项目** 此项目包含定义域特定语言的代码。

- **DslPackage 项目** 此项目包含允许 DSL 实例在 Visual Studio 中打开和编辑的代码。

## <a name="running-the-dsl"></a><a name="Debugging"></a> 运行 DSL

可以在创建 DSL 解决方案后立即运行它。 稍后，可以逐步修改 DSL 定义，每次更改后再次运行解决方案。

### <a name="to-experiment-with-the-dsl"></a>试验 DSL

1. 在“解决方案资源管理器”工具栏中，单击“转换所有模板” 。 这会从 DslDefinition.dsl 重新生成大部分源代码。

    > [!NOTE]
    > 每当更改 DslDefinition.dsl 时，都必须在重新生成解决方案之前单击“转换所有模板”。 可以自动化执行此步骤。 有关详细信息，请参阅[如何自动转换所有模板](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\))。

2. 按“F5” ，或在“调试”  菜单上，单击“开始调试” 。

     DSL 生成并安装在 Visual Studio 的实验实例中。

     启动 Visual Studio 的实验实例。 实验实例从注册表的单独子树中获取其设置，其中注册了 Visual Studio 扩展以用于调试目的。 Visual Studio 的普通实例无权访问其中注册的扩展。

3. 在 Visual Studio 的实验实例中，从“解决方案资源管理器”打开名为 Test 的模型文件。

     \- 或 -

     右键单击调试项目，指向“添加”，然后单击“项”。 在“添加项”对话框中，选择 DSL 的文件类型。

     模型文件以空白关系图打开。

     工具箱将打开并显示与该关系图类型相对应的工具。

4. 使用工具在关系图上创建形状和连接器。

    1. 若要创建形状，请从“示例形状”工具拖到关系图上。

    2. 若要连接两个形状，请单击“示例连接器”工具，单击第一个形状，然后单击第二个形状。

5. 单击形状的标签以更改它们。

实验 Visual Studio 类似于以下示例：

![Visual Studio 中的域特定语言示例树](../modeling/media/dsl_min.png)

### <a name="the-content-of-a-model"></a>模型的内容

作为 DSL 实例的文件的内容称为模型。 模型包含模型<em>元素</em>以及元素之间的链接。 DSL 定义指定模型中可以存在哪些类型的模型元素和链接。 例如，在从最小语言模板创建的 DSL 中，有一种类型的模型元素和一种类型的链接。

DSL 定义可以指定模型在关系图上的显示方式。 可以从各种样式的形状和连接器中选择。 可以指定某些形状显示在其他形状内。

编辑模型时，可以在“资源管理器”视图中以树的形式查看模型。 向关系图添加形状时，模型元素也会显示在资源管理器中。 即使没有关系图，也可使用资源管理器。

如果在 Visual Studio 的调试实例中看不到资源管理器，请在“视图”菜单上指向“其他窗口”，然后单击“\<Your Language> 资源管理器”。

### <a name="the-api-of-your-dsl"></a>DSL 的 API

DSL 会生成一个 API，用于读取和更新作为 DSL 实例的模型。 API 的一个应用是从模型生成文本文件。 有关详细信息，请参阅[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)。

在调试解决方案中，打开扩展名为“.tt”的模板文件。 这些示例演示如何从模型生成文本，并允许测试 DSL 的 API。 其中一个示例用 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 编写，另一个用 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 编写。

在每个模板文件下是它生成的文件。 在解决方案资源管理器中展开模板文件，并打开生成的文件。

模板文件包含一小段代码，其中列出了模型中的所有元素。

生成的文件包含结果。

更改模型文件时，重新生成文件后，将在生成的文件中看到相应的更改。

#### <a name="to-regenerate-text-files-after-you-change-the-model-file"></a>更改模型文件后重新生成文本文件

1. 在 Visual Studio 的实验实例中，保存模型文件。

2. 确保每个 .tt 文件中的文件名参数是指你用于实验的模型文件。 保存 .tt 文件。

3. 在“解决方案资源管理器”的工具栏中，单击“转换所有模板” 。

     \- 或 -

     右键单击要重新生成的模板，然后单击“运行自定义工具”。

可以将任意数目的文本模板文件添加到项目中。 每个模板生成一个结果文件。

> [!NOTE]
> 更改 DSL 定义时，示例文本模板代码将不起作用，除非更新它。

有关详细信息，请参阅[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)和[编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)。

## <a name="customizing-the-dsl"></a>自定义 DSL

若要修改 DSL 定义，请关闭实验实例，并更新主 Visual Studio 实例中的定义。

> [!NOTE]
> 修改 DSL 定义后，可能会丢失使用早期版本创建的测试模型中的信息。  例如，调试解决方案包含名为 Sample 的文件，其中包含一些形状和连接器。 开始开发 DSL 定义后，它们将不可见，并且将在保存文件时丢失。

你可以对 DSL 进行各种扩展。 以下示例将让你对可能性有一个印象。

每次更改后，保存 DSL 定义，在“解决方案资源管理器”中单击“转换所有模板”，然后按 F5 以试验更改后的 DSL。

### <a name="rename-the-types-and-tools"></a>重命名类型和工具

重命名现有域类和关系。 例如，从基于最小语言模板创建的 Dsl 定义开始，可以执行以下重命名操作，使 DSL 表示家谱。

#### <a name="to-rename-domain-classes-relationships-and-tools"></a>重命名域类、关系和工具

1. 在 DslDefinition 关系图中，将 ExampleModel 重命名为 FamilyTreeModel，将 ExampleElement 重命名为 Person，将 Targets 重命名为 Parents，将 Sources 重命名为 Children。 可以单击每个标签进行更改。

     ![DSL 定义关系图 &#45; 家谱模型](../modeling/media/familyt_person.png)

2. 重命名元素和连接器工具。

    1. 单击“解决方案资源管理器”下的选项卡，打开“DSL 资源管理器”窗口。 如果看不到该窗口，则在“视图”菜单上，指向“其他窗口”，然后单击“DSL 资源管理器”  。 DSL 资源管理器仅在 DSL 定义关系图为活动窗口时可见。

    2. 打开“属性”窗口并定位它，以便可以同时查看 DSL 资源管理器和属性。

    3. 在 DSL 资源管理器中，依次展开“编辑器”、“工具箱选项卡”、\<your DSL> 和“工具”。

    4. 单击 ExampleElement。 这是用于创建元素的工具箱项。

    5. 在“属性”窗口中，将“Name”属性更改为“Person” 。

         请注意，Caption 属性也会更改。

    6. 同样，将 ExampleConnector 工具的名称更改为 ParentLink。 更改 Caption 属性，不将其作为 Name 属性的副本。 例如，输入“父链接”。

3. 重新生成 DSL。

    1. 保存 DSL 定义文件。

    2. 在“解决方案资源管理器”的工具栏中，单击“转换所有模板”

    3. 按 F5。 等到 Visual Studio 的实验实例出现。

4. 在 Visual Studio 实验实例中的调试解决方案中，打开测试模型文件。 将元素从工具箱拖到该文件上。 请注意，DSL 资源管理器中的工具标题和类型名称已更改。

5. 保存模型文件。

6. 打开 .tt 文件，将出现的旧类型和属性名称替换为新名称。

7. 请确保 .tt 文件中指定的文件名指定测试模型。

8. 保存 .tt 文件。 打开生成的文件，查看在 .tt 文件中运行代码的结果。 验证结果是否正确。

### <a name="add-domain-properties-to-classes"></a>将域属性添加到类
 向域类添加属性，例如，表示某人的出生年份和死亡年份。

 若要使新属性在关系图上可见，必须将修饰器添加到显示模型元素的形状。 还必须将属性映射到修饰器。

##### <a name="to-add-properties-and-display-them"></a>添加和显示属性

1. 添加属性。

   1. 在 DSL 定义关系图中，右键单击 Person 域类，指向“添加”，然后单击“域属性”。

   2. 键入新属性名称的列表，例如 Birth 和 Death。 在键入每个名称后按 Enter。

2. 添加将在形状中显示属性的修饰器。

   1. 沿着从 Person 域类扩展到关系图另一侧的灰色线。 这是关系图元素映射。 它将域类链接到形状类。

   2. 右键单击此形状类，指向“添加”，然后单击“文本修饰器” 。

   3. 添加两个名称为 BirthDecorator 和 DeathDecorator 的修饰器。

   4. 选择每个新修饰器，然后在“属性”窗口中设置“位置”字段。 这决定了域属性值将在形状上显示的位置。 例如，设置 InnerBottomLeft 和 InnerBottomRight。

        ![隔离舱形状定义](../modeling/media/familyt_compartment.png)

3. 将修饰器映射到属性。

   1. 打开“DSL 详细信息”窗口。 它通常位于“输出”窗口旁边的选项卡中。 如果看不到该窗口，则在“视图”菜单上，指向“其他窗口”，然后单击“DSL 详细信息”  。

   2. 在 DSL 定义关系图上，单击将 Person 域类连接到形状类的线。

   3. 在“DSL 详细信息”中的“修饰器映射”选项卡上，单击未映射修饰器上的复选框。 在“显示属性”中，选择要将其映射到的域属性。 例如，将 BirthDecorator 映射到 Birth。

4. 保存 DSL，单击“转换所有模板”，然后按 F5。

5. 在示例模型关系图中，验证现在能否单击选择的位置，并在其中键入值。 此外，当你选择 Person 形状时，“属性”窗口会显示新的属性 Birth 和 Death。

6. 在 .tt 文件中，可以添加获取每个人的属性的代码。

   ![家谱关系图、工具箱和资源管理器](../modeling/media/familyt_instance.png)

### <a name="define-new-classes"></a>定义新类
 可以向模型添加域类和关系。 例如，可以创建一个新类来表示城镇，并创建一个新关系来表示一个人住在一个城镇。

 为了使模型关系图上的不同类型保持独特，可以将域类映射到不同类型的形状，或映射到具有不同几何和颜色的形状。

##### <a name="to-add-and-display-a-new-domain-class"></a>添加并显示新域类

1. 添加域类，并使其成为模型根的子元素。

    1. 在 DSL 定义关系图中，单击“嵌入关系”工具，单击根类 FamilyTreeModel，然后单击关系图的空白部分。

         出现一个新域类，它通过嵌入关系连接到 FamilyTreeModel。

         设置其名称，例如 Town。

        > [!NOTE]
        > 每个域类（模型的根除外）都必须至少是一个嵌入关系的目标，或必须继承自作为嵌入目标的类。 因此，使用嵌入关系工具创建域类通常很方便。

    2. 将域属性添加到新类，例如 Name。

2. 添加 Person 与 Town 之间的引用关系。

    1. 单击“引用关系”工具，单击“Person”，然后单击“Town”。

         ![DSL 定义片段：家谱根目录](../modeling/media/familyt_root.png)

        > [!NOTE]
        > 引用关系表示从模型树的一个部分到另一个部分的交叉引用。

3. 添加一个形状来表示模型关系图上的城镇。

    1. 将几何形状从工具箱拖到关系图中，然后将其重命名，例如 TownShape。

    2. 在“属性”窗口中，设置新形状的外观字段，例如“填充颜色”和“几何”。

    3. 添加一个修饰器以显示城镇的名称，并将其重命名为 NameDecorator。 设置其 Position 属性。

4. 将 Town 域类映射到 TownShape。

    1. 单击“关系图元素映射”工具，单击 Town 域类，然后单击 TownShape 形状类。

    2. 在“DSL 详细信息”窗口的“修饰器映射”选项卡中，在选中映射连接器的情况下，检查 NameDecorator 并将“显示属性”设置为 Name  。

5. 创建连接器以显示 Person 和 Towns 之间的关系。

    1. 将连接器从工具箱拖到关系图中。 将其重命名并设置其外观属性。

    2. 使用“关系图元素映射”工具将新连接器链接到 Person 和 Town 之间的关系。

         ![添加了形状映射的家谱定义](../modeling/media/familyt_shapemap.png)

6. 创建一个用于创建新 Town 的元素工具。

    1. 在“DSL 资源管理器”中，依次展开“编辑器”、“工具箱选项卡” 。

    2. 右键单击 \<your DSL>，然后单击“添加新元素工具”。

    3. 设置新工具的 Name 属性，并将其 Class 属性设置为 Town。

    4. 设置“工具箱图标”属性。 单击 [...]，在“文件名”字段中选择一个图标文件。

7. 创建用于在城镇与人员之间进行链接的连接器工具。

    1. 右键单击 \<your DSL>，然后单击“添加新连接器工具”。

    2. 设置新工具的 Name 属性。

    3. 在 ConnectionBuilder 属性中，选择包含 Person-Town 关系名称的生成器。

    4. 设置“工具箱图标”。

8. 保存 DSL 定义，单击“转换所有模板”，然后按 F5。

9. 在 Visual Studio 的实验实例中，打开测试模型文件。 使用新工具来创建城镇以及城镇和人员之间的链接。 请注意，只能在正确类型的元素之间创建链接。

10. 创建列出每个人居住的城镇的代码。 文本模板是可以运行此类代码的位置之一。 例如，可以修改调试解决方案中的现有 Sample.tt 文件，使其包含以下代码：

    ```
    <#@ template inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" debug="true" #>
    <#@ output extension=".txt" #>
    <#@ FamilyTree processor="FamilyTreeDirectiveProcessor" requires="fileName='Sample.ftree'" #>

    <#
      foreach (Person person in this.FamilyTreeModel.People)
      {
    #>
        <#= person.Name #><#if (person.Town != null) {#> of <#= person.Town.Name #> <#}#>

    <#
          foreach (Person child in person.Children)
      {
    #>
                <#= child.Name #>
    <#
      }
      }
    #>

    ```

     保存 *.tt 文件时，它将创建一个包含人员及其住所列表的附属文件。 有关详细信息，请参阅[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)。

## <a name="validation-and-commands"></a>验证和命令
 可以通过添加验证约束来进一步开发此 DSL。 这些约束是可以定义的方法，可确保模型处于正确的状态。 例如，可以定义一个约束以确保孩子的出生日期晚于其父母的出生日期。 如果 DSL 用户尝试保存违反了任何约束的模型，则验证功能将显示警告。 有关详细信息，请参阅[域特定语言中的验证](../modeling/validation-in-a-domain-specific-language.md)。

 还可以定义用户可以调用的菜单命令。 命令可以修改模型。 它们还可以与 Visual Studio 中的其他模型和外部资源交互。 有关详细信息，请参阅[如何：修改标准菜单命令](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)。

## <a name="deploying-the-dsl"></a>部署 DSL
 若要允许其他用户使用域特定语言，请分发 Visual Studio 扩展 (VSIX) 文件。 这是在生成 DSL 解决方案时创建的。

 找到解决方案的 bin 文件夹中的 .vsix 文件。 将其复制到要在其上安装它的计算机。 在该计算机上，双击该 VSIX 文件。 DSL 可用于该计算机上的所有 Visual Studio 实例。

 你可以使用相同的过程在自己的计算机上安装 DSL，这样就不必使用 Visual Studio 的实验实例。

 有关详细信息，请参阅[部署域特定语言解决方案](msi-and-vsix-deployment-of-a-dsl.md)。

## <a name="removing-old-experimental-dsls"></a><a name="Reset"></a> 删除旧的实验性 DSL
 如果已创建不再需要的实验性 DSL，可以通过重置 Visual Studio 实验实例将它们从你的计算机中删除。

 这将从你的计算机中删除所有实验性 DSL 和其他实验性 Visual Studio 扩展。 这些是已在调试模式下执行的扩展。

 此过程不会删除已通过执行 VSIX 文件完全安装的 DSL 或其他 Visual Studio 扩展。

#### <a name="to-reset-the-visual-studio-experimental-instance"></a>重置 Visual Studio 实验实例

1. 依次单击“开始”、“所有程序”、“Microsoft Visual Studio 2010 SDK”、“工具”，然后单击“重置 Microsoft Visual Studio 2010 实验实例”    。

2. 重新生成仍想要使用的任何实验性 DSL 或其他实验性 Visual Studio 扩展。

## <a name="see-also"></a>另请参阅

- [了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)
- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)
