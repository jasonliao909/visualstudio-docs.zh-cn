---
title: 域特定语言入门
description: 了解如何定义和使用域特定语言 (DSL) 使用用于 Visual Studio 的建模 SDK 创建的基本概念。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122061293"
---
# <a name="get-started-with-domain-specific-languages"></a>域特定语言入门

本主题介绍如何定义和使用通过用于 Visual Studio 的建模 SDK 创建的域特定语言 (DSL) 的基本概念。

> [!NOTE]
> 安装 Visual Studio 的特定功能时，将自动安装文本模板转换 sdk 和 Visual Studio 建模 sdk。 有关更多详细信息，请参阅[这篇博客文章](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)。

如果你不熟悉 Dsl，我们建议你通过 **DSL 工具实验室**，你可以在此网站中找到： [可视化和建模 SDK](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)

## <a name="what-can-you-do-with-a-domain-specific-language"></a>使用 Domain-Specific 语言可以做些什么？

域特定语言是一种通常为图形的表示法，用于特定目的。 与此相反，UML 等语言是通用的。 在 DSL 中，可以定义模型元素的类型及其关系，以及如何在屏幕上显示它们。

设计 DSL 后，可以将其作为 Visual Studio 集成扩展 (的一部分进行分发，) 包。 用户使用 Visual Studio 中的 DSL：

![家谱关系图、工具箱和资源管理器](../modeling/media/familyt_instance.png)

该表示法仅属于 DSL。 与表示法一起使用，VSIX 包包含一些工具，用户可以应用这些工具来帮助他们从模型中编辑和生成材料。

Dsl 的一个主体应用程序是生成程序代码、配置文件和其他项目。 尤其是在大型项目和产品系列中，将在其中创建产品的多个变体，同时从 Dsl 生成许多可变方面可大大提高可靠性，并快速响应需求变化。

本概述的其余部分是一个演练，其中介绍了在 Visual Studio 中创建和使用域特定语言的基本操作。

## <a name="prerequisites"></a>必备条件

若要定义 DSL，必须安装以下组件：

| 组件 | 链接 |
|-|-|
| Visual Studio | [http://go.microsoft.com/fwlink/?LinkId=185579](https://visualstudio.microsoft.com) |
| [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] | [https://go.microsoft.com/fwlink/?linkid=2166172](../extensibility/visual-studio-sdk.md) |
| Visual Studio 的建模 SDK | |

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="create-a-dsl-solution"></a>创建 DSL 解决方案

若要创建新的域特定语言，请使用 "Domain-Specific 语言" 项目模板创建一个新的 Visual Studio 解决方案。

1. 在 **“文件”** 菜单上，指向 **“新建”** ，再单击 **“项目”** 。

2. 在 " **Project 类型**" 下，展开 "**其他 Project 类型**" 节点，然后单击 "**扩展性**"。

3. 单击 " **特定于域的语言设计器**"。

     ![“创建 DSL”对话框](../modeling/media/create_dsldialog.png)

4. 在 " **名称** " 框中，键入 **FamilyTree**。 单击“确定”。

     " **域特定语言向导** " 将打开，并显示模板 DSL 解决方案列表。

     单击每个模板以查看说明，

     这些模板非常有用。 每个用户提供了一个完整的工作 DSL，你可以根据需要进行编辑。 通常，你可以选择最接近你要创建的模板的模板。

5. 对于本演练，请选择 **最小语言** 模板。

6. 在相应的向导页中输入 DSL 的文件扩展名。 这是包含 DSL 的实例的文件将使用的扩展名。

    - 选择与您的计算机中的任何应用程序或要在其中安装 DSL 的任何计算机都不关联的扩展插件。 例如， **.docx** 和 **htm** 将是不接受的文件扩展名。

    - 如果你输入的扩展名已用作 DSL，则该向导将向你发出警告。 请考虑使用不同的文件扩展名。 还可以重置 Visual Studio SDK 实验实例以清除旧的实验设计器。 依次单击 "**开始**"、"**所有程序**"、 **Microsoft Visual Studio 2010 SDK**、**工具**，然后 **重置 Microsoft Visual Studio 2010 实验实例**。

7. 检查其他页面，然后单击 " **完成**"。

     生成包含两个项目的解决方案。 它们被命名为 Dsl 和 DslPackage。 随即打开一个名为 Dsldefinition.dsl 的关系图文件。

    > [!NOTE]
    > 在两个项目的文件夹中可以看到的大多数代码都是从 Dsldefinition.dsl 生成的。 出于此原因，在此文件中对 DSL 进行的大部分修改都是如此。

用户界面现在类似于下图。

![dsl 设计器](../modeling/media/dsl_designer.png)

此解决方案将定义域特定语言。 有关详细信息，请参阅 [Domain-Specific 语言工具用户界面概述](../modeling/overview-of-the-domain-specific-language-tools-user-interface.md)。

## <a name="the-important-parts-of-the-dsl-solution"></a>DSL 解决方案的重要部分

请注意新解决方案的以下方面：

- **Dsl\DslDefinition.dsl** 这是创建 DSL 解决方案时看到的文件。 此文件中几乎所有的代码都是从该文件生成的，而对 DSL 定义所做的大多数更改都在此处进行。 有关详细信息，请参阅使用 [DSL 定义关系图](../modeling/working-with-the-dsl-definition-diagram.md)。

- **Dsl 项目** 此项目包含定义域特定语言的代码。

- **DslPackage 项目** 此项目包含允许在 Visual Studio 中打开和编辑 DSL 实例的代码。

## <a name="running-the-dsl"></a><a name="Debugging"></a> 运行 DSL

一旦创建 DSL 解决方案，就可以运行它。 稍后，你可以逐步修改 DSL 定义，并在每次更改后再次运行解决方案。

### <a name="to-experiment-with-the-dsl"></a>试验 DSL

1. 单击 "**解决方案资源管理器**" 工具栏中的 "**转换所有模板**"。 这将从 Dsldefinition.dsl 重新生成大部分源代码。

    > [!NOTE]
    > 更改 *dsldefinition.dsl* 时，必须单击 " **转换所有模板** "，然后重新生成解决方案。 可以自动化执行此步骤。 有关详细信息，请参阅 [如何自动转换所有模板](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\))。

2. 按“F5” ，或在“调试”  菜单上，单击“开始调试” 。

     DSL 构建并安装在 Visual Studio 的实验实例中。

     开始 Visual Studio 的实验实例。 实验实例从注册表的单独子树获取其设置，其中 Visual Studio 扩展注册用于调试目的。 Visual Studio 的普通实例无法访问在此处注册的扩展。

3. 在 Visual Studio 的实验实例中，从 **解决方案资源管理器** 中打开名为 **Test** 的模型文件。

     \- 或 -

     右键单击 "调试" 项目，指向 " **添加**"，然后单击 " **项**"。 在 " **添加项目** " 对话框中，选择 DSL 的文件类型。

     该模型文件将作为空白关系图打开。

     工具箱随即打开，并显示适用于关系图类型的工具。

4. 使用这些工具可以在关系图上创建形状和连接线。

    1. 若要创建形状，请从示例形状工具拖动到关系图上。

    2. 若要连接两个形状，请单击 "示例连接线" 工具，单击第一个形状，然后单击第二个形状。

5. 单击形状的标签可对其进行更改。

实验性 Visual Studio 将类似于以下示例：

![Visual Studio 中的域特定语言示例树](../modeling/media/dsl_min.png)

### <a name="the-content-of-a-model"></a>模型的内容

作为 DSL 实例的文件的内容称为 *模型*。 模型包含 *模型*<em>元素</em>和元素之间的 *链接*。 DSL 定义指定模型中可以存在的模型元素和链接的类型。 例如，在从最小语言模板创建的 DSL 中，有一种类型的模型元素和一种类型的链接。

DSL 定义可以指定模型在关系图上的显示方式。 可以从各种形状和连接符样式中进行选择。 您可以指定某些形状显示在其他形状内。

编辑模型时，可以在 " **资源管理器** " 视图中查看作为树的模型。 将形状添加到关系图中时，模型元素也会显示在资源管理器中。 即使没有关系图，也可使用资源管理器。

如果在调试实例中看不到资源管理器Visual Studio，请在"视图"菜单上指向"其他 **Windows"，** 然后单击"资源管理器 *\<Your Language>* **"。**

### <a name="the-api-of-your-dsl"></a>DSL 的 API

DSL 会生成一个 API，用于读取和更新作为 DSL 实例的模型。 API 的一个应用程序是从模型生成文本文件。 有关详细信息，请参阅[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)。

在调试解决方案中，打开扩展名为".tt"的模板文件。 这些示例演示如何从模型生成文本，并允许测试 DSL 的 API。 其中一个示例用 编写 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ，另一个在 中 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 编写。

在每个模板文件下是它生成的文件。 展开模板文件解决方案资源管理器，然后打开生成的文件。

模板文件包含一段短段代码，其中列出了模型的所有元素。

生成的文件包含结果。

更改模型文件时，重新生成文件后，将在生成的文件中看到相应的更改。

#### <a name="to-regenerate-text-files-after-you-change-the-model-file"></a>更改模型文件后重新生成文本文件

1. 在 Visual Studio试验实例中，保存模型文件。

2. 确保每个 .tt 文件的文件名参数引用用于试验的模型文件。 保存 .tt 文件。

3. 在 **的工具栏中单击** "转换所有 **模板** 解决方案资源管理器" 。

     \- 或 -

     右键单击要重新生成的模板，然后单击"**运行自定义工具"。**

可以将任意数目的文本模板文件添加到项目。 每个模板都会生成一个结果文件。

> [!NOTE]
> 更改 DSL 定义时，示例文本模板代码将不起作用，除非更新它。

有关详细信息，请参阅从语言 [生成代码Domain-Specific编写](../modeling/generating-code-from-a-domain-specific-language.md) 代码 [以自定义Domain-Specific语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)。

## <a name="customizing-the-dsl"></a>自定义 DSL

若要修改 DSL 定义，请关闭实验实例，并更新主实例Visual Studio定义。

> [!NOTE]
> 修改 DSL 定义后，可能会丢失使用早期版本创建的测试模型中的信息。  例如，调试解决方案包含名为 Sample 的文件，其中包含一些形状和连接器。 开始开发 DSL 定义后，它们将不可见，并且将在保存文件时丢失。

你可以对 DSL 进行各种扩展。 以下示例将让你对可能性有一个印象。

每次更改后，保存 DSL 定义，单击 **解决方案资源管理器"** 转换所有模板 **"，然后** 按 **F5** 试验更改后的 DSL。

### <a name="rename-the-types-and-tools"></a>重命名类型和工具

重命名现有域类和关系。 例如，从从最小语言模板创建的 Dsl 定义开始，可以执行以下重命名操作，使 DSL 表示系列树。

#### <a name="to-rename-domain-classes-relationships-and-tools"></a>重命名域类、关系和工具

1. 在 DslDefinition 关系图中，将 **ExampleModel** 重命名为 **FamilyTreeModel，** 将 **ExampleElement** 重命名为 **Person，** 将 **目标** 重命名 **为"父** 对象"，将"**源"** 重命名为 **"子级"。** 可以单击每个标签来更改它。

     ![DSL 定义关系图&#45;系列树模型](../modeling/media/familyt_person.png)

2. 重命名元素和连接器工具。

    1. 单击"DSL 资源管理器"窗口，单击"解决方案资源管理器"。 如果看不到它，请在"视图"菜单上指向"其他 **Windows然后单击****"DSL 资源管理器"。** DSL 资源管理器仅在 DSL 定义关系图为活动窗口时可见。

    2. 打开属性窗口并定位它，以便可以同时查看 DSL 资源管理器和属性。

    3. 在 DSL 资源管理器中，展开"**编辑器"、"****工具箱"选项卡** *\<your DSL>* 、，然后展开"**工具"。**

    4. 单击 **"示例""删除"。** 这是用于创建元素的工具箱项。

    5. 在属性窗口，将 **Name 属性** 更改为 **Person**。

         请注意 **，Caption** 属性也会更改。

    6. 同样，将 **ExampleConnector** 工具的名称更改为 **ParentLink**。 更改 **Caption** 属性，以便它不是 Name 属性的副本。 例如，输入"**父链接"。**

3. 重新生成 DSL。

    1. 保存 DSL 定义文件。

    2. 单击 **模板工具栏中的** "转换所有模板解决方案资源管理器

    3. 按 F5。 请等待，直到显示 Visual Studio实例。

4. 在 Visual Studio 实验实例的调试解决方案中，打开测试模型文件。 将元素从工具箱拖动到该工具箱上。 请注意，DSL 资源管理器中的工具标题和类型名称已更改。

5. 保存模型文件。

6. 打开 .tt 文件，将旧类型和属性名称的出现替换为新名称。

7. 请确保 .tt 文件中指定的文件名指定测试模型。

8. 保存 .tt 文件。 打开生成的 文件，查看在 .tt 文件中运行代码的结果。 验证是否正确。

### <a name="add-domain-properties-to-classes"></a>将域属性添加到类
 向域类添加属性，例如，表示某人的出生日期和出生年数。

 若要使新属性在关系图上可见，必须将 *修饰* 器添加到显示模型元素的形状。 还必须将属性映射到修饰器。

##### <a name="to-add-properties-and-display-them"></a>添加和显示属性

1. 添加属性。

   1. 在 DSL 定义关系图中，右键单击 **Person** 域类，指向"**添加**"，然后单击"**域属性"。**

   2. 键入新属性名称的列表，例如 **"出生"** 和"**死"。** 在每个 **键后按 Enter。**

2. 添加修饰器，用于显示形状中的属性。

   1. 遵循从 Person 域类扩展到关系图另一侧的灰色线。 这是关系图元素映射。 它将域类链接到形状类。

   2. 右键单击此形状类，指向"**添加"，** 然后单击"**文本修饰器"。**

   3. 添加两个名称为 的修饰器，如 **BirthDecorator** 和 **BirthDecorator**。

   4. 选择每个新的修饰器，然后属性窗口设置 **"位置"** 字段。 这将确定域属性值在形状上的显示位置。 例如，设置 **InnerBottomLeft 和** **InnerBottomRight**。

        ![隔离舱形状定义](../modeling/media/familyt_compartment.png)

3. 将修饰器映射到属性。

   1. 打开“DSL 详细信息”窗口。 它通常位于"输出"窗口旁边的选项卡中。 如果看不到它，请在"视图"菜单上指向"其他Windows"，**然后单击****"DSL 详细信息"。**

   2. 在 DSL 定义关系图上，单击将 **Person** 域类连接到形状类的行。

   3. 在 **DSL 详细信息** 中，在"修饰器 **地图** 选项卡上，单击未映射修饰器上的复选框。 在 **"显示** 属性"中，选择要将其映射到的域属性。 例如，将 **BirthDecorator 映射到** **Birth**。

4. 保存 DSL，单击"转换所有模板"，然后按 F5。

5. 在示例模型关系图中，验证现在能否单击选择的位置，并键入值。 此外，选择"人员 **"形状时** ，属性窗口显示新的属性"出生日期和体重"。

6. 在 .tt 文件中，可以添加获取每个人属性的代码。

   ![家谱关系图、工具箱和资源管理器](../modeling/media/familyt_instance.png)

### <a name="define-new-classes"></a>定义新类
 可以将域类和关系添加到模型。 例如，可以创建一个新类来表示城市，创建一个新关系来表示一个人在市县中生活。

 若要使模型关系图上的不同类型不同，可以将域类映射到不同类型的形状，或映射到具有不同几何图形和颜色的形状。

##### <a name="to-add-and-display-a-new-domain-class"></a>添加和显示新的域类

1. 添加域类，使其成为模型根的子级。

    1. 在 DSL 定义关系图中，单击 **"嵌入** 关系"工具，单击根类 **FamilyTreeModel**，然后单击关系图的空部分。

         将出现一个新的域类，该类通过嵌入关系连接到 FamilyTreeModel。

         设置其名称，例如 **"城市"。**

        > [!NOTE]
        > 每个域类（模型根除外）都必须是至少一个嵌入关系的目标，或者必须继承自作为嵌入目标的类。 因此，使用嵌入关系工具创建域类通常很方便。

    2. 将域属性添加到新类，例如 **Name**。

2. 在"人员"和"城市"之间添加引用关系。

    1. 单击" **引用关系"** 工具，单击"人员"，然后单击"城市"。

         ![DSL 定义片段：家谱根目录](../modeling/media/familyt_root.png)

        > [!NOTE]
        > 引用关系表示从模型树的一部分到另一部分的交叉引用。

3. 添加一个形状，用于表示模型关系图上的轮廓。

    1. 将"**几何形状**"从工具箱拖动到关系图，并将其重命名，例如 **"城市""Shape"。**

    2. 在属性窗口中，设置新形状的"外观"字段，例如"填充颜色和几何图形"。

    3. 添加修饰器以显示该县的名称，并将其重命名为 NameDecorator。 设置其 Position 属性。

4. 将"城市"域类映射到"市/县"。

    1. 单击" **关系图元素地图"** 工具，然后单击"城市"域类，然后单击"市县"形状类。

    2. 在 **"DSL 详细信息地图** 窗口的"修饰器"选项卡中，选中"NameDecorator"，将"显示属性 **"** 设置为"名称"。

5. 创建一个连接器，用于显示 Person 和用户之间的关系。

    1. 将"连接器"从工具箱拖动到关系图。 重命名它并设置其外观属性。

    2. 使用 **"关系图元素地图** "工具将新连接器链接到"人员"和"城市"之间的关系。

         ![添加了形状映射的家谱定义](../modeling/media/familyt_shapemap.png)

6. 创建用于创建新城市的元素工具。

    1. 在 **DSL 资源管理器中**，展开 **"编辑器"，然后** 展开"**工具箱选项卡"。**

    2. 右键单击 *\<your DSL>* ，然后单击"**添加新元素工具"。**

    3. 设置 **新工具** 的 Name 属性，将 **"Class"** 属性设置为"城市"。

    4. 设置工具箱 **图标** 属性。 单击 **"[...]** **"，在 "文件名"** 字段中，选择一个图标文件。

7. 创建一个连接器工具，用于建立人员与人员之间的链接。

    1. 右键单击 *\<your DSL>* ，然后单击"**添加新连接器工具"。**

    2. 设置新工具的 Name 属性。

    3. 在 **ConnectionBuilder** 属性中，选择包含关系名称Person-Town生成器。

    4. 设置工具箱 **图标**。

8. 保存 DSL 定义，单击 **"转换所有模板"，** 然后按 **F5**。

9. 在 Visual Studio 试验实例中，打开测试模型文件。 使用新工具在居民和人员之间创建省/市/县和链接。 请注意，只能在正确的元素类型之间创建链接。

10. 创建列出每个人所住城市的代码。 文本模板是可运行此类代码的地方之一。 例如，可以在调试解决方案中修改 Sample.tt 文件，以便它包含以下代码：

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

     保存 *.tt 文件时，它将创建一个附属文件，其中包含人员及其居民的列表。 有关详细信息，请参阅从语言 [语言](../modeling/generating-code-from-a-domain-specific-language.md)Domain-Specific代码。

## <a name="validation-and-commands"></a>验证和命令
 可以通过添加验证约束进一步开发此 DSL。 这些约束是你可以定义的方法，用于确保模型的状态正确。 例如，可以定义一个约束，以确保子项的出生日期晚于其父母的出生日期。 如果 DSL 用户尝试保存违反任何约束的模型，验证功能将显示警告。 有关详细信息，请参阅在语言 [中Domain-Specific验证](../modeling/validation-in-a-domain-specific-language.md)。

 还可以定义用户可调用的菜单命令。 命令可以修改模型。 它们还可以与资源中的其他模型Visual Studio外部资源进行交互。 有关详细信息，请参阅 [如何：修改标准菜单命令](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)。

## <a name="deploying-the-dsl"></a>部署 DSL
 若要允许其他用户使用特定于域的语言，请分发 VSIX Visual Studio扩展 (扩展) 文件。 这是在生成 DSL 解决方案时创建的。

 在解决方案的 bin 文件夹中找到 .vsix 文件。 将其复制到要安装的计算机。 在计算机中，双击 VSIX 文件。 DSL 可用于该计算机上所有 Visual Studio实例。

 可以使用同一过程在你自己的计算机上安装 DSL，这样就不需要使用 Visual Studio。

 有关详细信息，请参阅[部署域特定语言解决方案](msi-and-vsix-deployment-of-a-dsl.md)。

## <a name="removing-old-experimental-dsls"></a><a name="Reset"></a> 删除旧的实验性 DSL
 如果已创建不再需要的实验性 DSL，则可以通过重置实验性实例Visual Studio删除它们。

 这会从计算机中删除所有实验性 DSL 和其他试验Visual Studio扩展。 这些扩展已在调试模式下执行。

 此过程不会删除通过执行 VSIX Visual Studio完全安装的 DSL 或其他扩展。

#### <a name="to-reset-the-visual-studio-experimental-instance"></a>重置 Visual Studio 试验实例

1. 单击 **"开始**"，**单击"** 所有程序 **"，Microsoft Visual Studio 2010 SDK** **、"工具**"，然后重置 Microsoft Visual Studio **2010 试验实例**。

2. 重新生成任何试验性 DSL 或其他Visual Studio仍然想要使用的试验性扩展。

## <a name="see-also"></a>请参阅

- [了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)
- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)
