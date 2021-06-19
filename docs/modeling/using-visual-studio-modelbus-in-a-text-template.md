---
title: 在文本模板中使用 ModelBus
description: 了解如何解析对访问目标模型的引用（如果编写文本模板来读取包含Visual Studio ModelBus模型）。
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2afe8de66b109793a4e15e8320c3f498a08b25ec
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388381"
---
# <a name="using-visual-studio-modelbus-in-a-text-template"></a>在文本模板中使用 Visual Studio ModelBus

如果编写文本模板来读取包含引用Visual Studio ModelBus，可能需要解析引用以访问目标模型。 在这种情况下，必须调整文本模板和引用的域特定语言，以 (DLL) ：

- 作为引用目标的 DSL 必须具有配置为从文本模板访问的 ModelBus 适配器。 如果还从其他代码访问 DSL，则除了标准 ModelBus 适配器外，还需要重新配置的适配器。

     适配器管理器必须从 [VsTextTemplatingModelingAdapterManager](/previous-versions/ee844317(v=vs.140)) 继承，并且必须具有 属性 `[HostSpecific(HostName)]` 。

- 模板必须继承自 [ModelBusEnabledTextTransformation](/previous-versions/ee844263(v=vs.140))。

> [!NOTE]
> 如果要读取不包含 ModelBus 引用的 DSL 模型，可以使用 DSL 项目中生成的指令处理器。 有关详细信息，请参阅 [从文本模板 访问模型](../modeling/accessing-models-from-text-templates.md)。

有关文本模板详细信息，请参阅使用 T4 文本模板设计 [时代码生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)。

## <a name="create-a-model-bus-adapter-for-access-from-text-templates"></a>创建用于从文本模板访问的模型总线适配器

若要解析文本模板中的 ModelBus 引用，目标 DSL 必须具有兼容的适配器。 文本模板在独立于文档编辑器Visual Studio AppDomain 中执行，因此适配器必须加载模型，而不是通过 DTE 访问它。

1. 如果目标 DSL 解决方案没有 **ModelBusAdapter** 项目，则使用 Modelbus 扩展向导创建一个：

    1. 下载并安装Visual Studio ModelBus扩展（如果尚未这样做）。 有关详细信息，请参阅可视化[效果和建模 SDK。](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)

    2. 打开 DSL 定义文件。 右键单击设计图面，然后单击"**启用模型总线"。**

    3. 在对话框中，选择 **"我想向 ModelBus 公开此 DSL"。** 如果希望此 DSL 公开其模型和使用对其他 DSL 的引用，可以选择这两个选项。

    4. 单击 **“确定”** 。 新项目“ModelBusAdapter”随即添加到 DSL 解决方案中。

    5. 单击 **"转换所有模板"。**

    6. 重新生成解决方案。

2. 如果要从文本模板和其他代码（如 命令）访问 DSL，请复制 **ModelBusAdapter** 项目：

    1. 在Windows 资源管理器，复制并粘贴包含 **ModelBusAdapter.csproj 的文件夹**。

    2. 例如，将项目 (重命名为 **T4ModelBusAdapter.csproj**) 。

    3. 在 **解决方案资源管理器** 中，右键单击解决方案节点，指向"**添加**"，然后单击"现有 **项目"。** 找到新的适配器项目 **T4ModelBusAdapter.csproj**。

    4. 在 `*.tt` 新项目的每个文件中，更改 命名空间。

    5. 右键单击项目中的新项目 **解决方案资源管理器** 然后单击"属性 **"。** 在属性编辑器中，更改生成的程序集的名称和默认命名空间。

    6. 在 DslPackage 项目中，添加对新适配器项目的引用，以便具有对两个适配器的引用。

    7. 在 DslPackage\source.extension.tt，添加引用新适配器项目的行。

        ```
        <MefComponent>|T4ModelBusAdapter|</MefComponent>
        ```

    8. **转换所有模板** 并重新生成解决方案。 不应发生生成错误。

3. 在新的适配器项目中，添加对以下程序集的引用：

    - Microsoft.VisualStudio.TextTemplating.11.0
    - Microsoft.VisualStudio.TextTemplating.Modeling.11.0

4. 在 AdapterManager.tt：

    - 更改 AdapterManagerBase 的声明，以便它继承自 [VsTextTemplatingModelingAdapterManager](/previous-versions/ee844317(v=vs.140))。

         `public partial class <#= dslName =>AdapterManagerBase :`

         `Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager { ...`

    - 在文件末尾附近，替换 AdapterManager 类前的 HostSpecific 属性。 删除以下行：

         `[DslIntegration::HostSpecific(DslIntegrationShell::VsModelingAdapterManager.HostName)]`

         插入以下行：

         `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

         此属性筛选 modelbus 使用者搜索适配器时可用的适配器集。

5. **转换所有模板** 并重新生成解决方案。 不应发生生成错误。

## <a name="write-a-text-template-that-can-resolve-modelbus-references"></a>编写可解析 ModelBus 引用的文本模板

通常，从从"源"DSL 读取和生成文件的模板开始。 此模板使用源 DSL 项目中生成的 指令，以从文本模板 访问模型中所述的方式读取 [源模型文件](../modeling/accessing-models-from-text-templates.md)。 但是，源 DSL 包含对"目标"DSL 的 ModelBus 引用。 因此，需要启用模板代码来解析引用并访问目标 DSL。 因此，必须按照以下步骤调整模板：

- 将模板的基类更改为 [ModelBusEnabledTextTransformation](/previous-versions/ee844263(v=vs.140))。

- 在 `hostspecific="true"` 模板指令中包括 。

- 添加对目标 DSL 及其适配器的程序集引用，并启用 ModelBus。

- 不需要作为目标 DSL 的一部分生成的 指令。

```
<#@ template debug="true" hostspecific="true" language="C#"
inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>
<#@ SourceDsl processor="SourceDslDirectiveProcessor" requires="fileName='Sample.source'" #>
<#@ output extension=".txt" #>
<#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>
<#@ assembly name = "Company.TargetDsl.Dsl.dll" #>
<#@ assembly name = "Company.TargetDsl.T4ModelBusAdapter.dll" #>
<#@ assembly name = "System.Core" #>
<#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>
<#@ import namespace="Company.TargetDsl" #>
<#@ import namespace="Company.TargetDsl.T4ModelBusAdapters" #>
<#@ import namespace="System.Linq" #>
<#
  SourceModelRoot source = this.ModelRoot; // Usual access to source model.
  // In the source DSL Definition, the root element has a model reference:
  using (TargetAdapter adapter = this.ModelBus.CreateAdapter(source.ModelReference) as TargetAdapter)
  {if (adapter != null)
   {
      // Get the root of the target model:
      TargetRoot target = adapter.ModelRoot;
    // The source DSL Definition has a class "SourceElement" embedded under the root.
    // (Let's assume they're all in the same model file):
    foreach (SourceElement sourceElement in source.Elements)
    {
      // In the source DSL Definition, each SourceElement has a MBR property:
      ModelBusReference elementReference = sourceElement.ReferenceToTarget;
      // Resolve the target model element:
      TargetElement element = adapter.ResolveElementReference<TargetElement>(elementReference);
#>
     The source <#= sourceElement.Name #> is linked to: <#= element.Name #> in target model: <#= target.Name #>.
<#
    }
  }}
  // Other useful code: this.Host.ResolvePath(filename) gets an absolute filename
  // from a path that is relative to the text template.
#>
```

 执行此文本模板时， `SourceDsl` 指令将加载文件 `Sample.source` 。 模板可以访问该模型的元素，从 开始 `this.ModelRoot` 。 代码可以使用该 DSL 的域类和属性。

 此外，模板可以解析 ModelBus 引用。 当引用指向目标模型时，程序集指令允许代码使用该模型的 DSL 的域类和属性。

- 如果不使用 DSL 项目生成的指令，则还应包含以下内容。

    ```
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.11.0" #>
    <#@ assembly name = "Microsoft.VisualStudio.TextTemplating.Modeling.11.0" #>
    ```

- 使用 `this.ModelBus` 获取对 ModelBus 的访问权限。

## <a name="walkthrough-testing-a-text-template-that-uses-modelbus"></a>演练：测试使用 ModelBus 的文本模板
 本演练将执行以下步骤：

1. 构造两个 DSL。 一个 *DSL（使用者*）具有 `ModelBusReference` 一个属性，该属性可以引用另一个 DSL， *即提供程序*。

2. 在提供程序中创建两个 ModelBus 适配器：一个适配器供文本模板访问，另一个适配器用于普通代码。

3. 在单个实验项目中创建 DSL 的实例模型。

4. 将一个模型中的域属性设置为指向另一个模型。

5. 编写一个双击处理程序，以打开指向的模型。

6. 编写一个文本模板，该模板可以加载第一个模型，遵循对另一个模型的引用，并读取其他模型。

### <a name="construct-a-dsl-that-is-accessible-to-modelbus"></a>构造 ModelBus 可访问的 DSL

1. 创建新的 DSL 解决方案。 对于此示例，请选择"任务流"解决方案模板。 将语言名称设置为 `MBProvider` ，将文件扩展名设置为".provide"。

2. 在 DSL 定义关系图中，右键单击关系图中不在顶部附近的空白部分，然后单击"**启用模型总线"。**

   如果未看到"启用 **Modelbus"，** 请下载并安装 VMSDK ModelBus 扩展。

3. 在"**启用 Modelbus"** 对话框中，选择"**向 ModelBus 公开此 DSL"，** 然后单击"确定 **"。**

    新项目 `ModelBusAdapter` 将添加到解决方案中。

现在，你有一个可通过 ModelBus 通过文本模板访问的 DSL。 可以在命令、事件处理程序或规则代码中解析对它的引用，所有这些操作均在模型文件编辑器的 AppDomain 中运行。 但是，文本模板在单独的 AppDomain 中运行，在编辑模型时无法访问该模型。 如果要从文本模板访问对此 DSL 的 ModelBus 引用，则必须有单独的 ModelBusAdapter。

### <a name="create-a-modelbus-adapter-that-is-configured-for-text-templates"></a>创建为文本模板配置的 ModelBus 适配器

1. 在文件资源管理器，复制并粘贴包含 *ModelBusAdapter.csproj 的文件夹*。

    将文件夹 **命名 T4ModelBusAdapter**。

    重命名项目文件 *T4ModelBusAdapter.csproj*。

2. 在解决方案资源管理器，将 T4ModelBusAdapter 添加到 MBProvider 解决方案。 右键单击解决方案节点，指向"**添加"，** 然后单击"**现有项目"。**

3. 右键单击 T4ModelBusAdapter 项目节点，然后单击"属性"。 在项目属性窗口中，将" **程序集名称"和** " **默认命名空间"更改为** `Company.MBProvider.T4ModelBusAdapters` 。

4. 在 T4ModelBusAdapter 的每个 *.tt 文件中，将"T4"插入命名空间的最后一部分，使行如下所示。

    `namespace <#= CodeGenerationUtilities.GetPackageNamespace(this.Dsl) #>.T4ModelBusAdapters`

5. 在 `DslPackage` 项目中，向 添加项目引用 `T4ModelBusAdapter` 。

6. 在 DslPackage\source.extension.tt，在 下添加以下行 `<Content>` 。

    `<MefComponent>|T4ModelBusAdapter|</MefComponent>`

7. 在项目中 `T4ModelBusAdapter` ，添加对 的引用 **：Microsoft.VisualStudio.TextTemplating.Modeling.11.0**

8. 打开 T4ModelBusAdapter\AdapterManager.tt：

   1. 将 AdapterManagerBase 的基类更改为 [VsTextTemplatingModelingAdapterManager](/previous-versions/ee844317(v=vs.140))。 此部分文件现在类似于以下内容。

       ```
       namespace <#= CodeGenerationUtilities.GetPackageNamespace(this.Dsl) #>.T4ModelBusAdapters
       {
           /// <summary>
           /// Adapter manager base class (double derived pattern) for the <#= dslName #> Designer
           /// </summary>
           public partial class <#= dslName #>AdapterManagerBase
           : Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager
           {
       ```

   2. 在文件末尾附近，将以下附加属性插入到类 AdapterManager 的前面。

        `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

        结果如下所示。

       ```
       /// <summary>
       /// ModelBus modeling adapter manager for a <#= dslName #>Adapter model adapter
       /// </summary>
       [Mef::Export(typeof(DslIntegration::ModelBusAdapterManager))]
       [Mef::ExportMetadata(DslIntegration::CompositionAttributes.AdapterIdKey,<#= dslName #>Adapter.AdapterId)]
       [DslIntegration::HostSpecific(DslIntegrationShell::VsModelingAdapterManager.HostName)]
       [Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]
       public partial class <#= dslName #>AdapterManager : <#= dslName #>AdapterManagerBase
       {
       }
       ```

9. 单击 "解决方案资源管理器的标题栏中的" **转换所有模板** "。

10. 按 **F5**。

11. 验证 DSL 是否正常工作。 在实验性项目中，打开 `Sample.provider` 。 关闭 Visual Studio 的实验实例。

    现在，可以在文本模板中和普通代码中解析对此 DSL 的 ModelBus 引用。

### <a name="construct-a-dsl-with-a-modelbus-reference-domain-property"></a>使用 ModelBus Reference 域属性构造 DSL

1. 使用最小语言解决方案模板创建新的 DSL。 将语言命名为 MBConsumer，并将文件扩展名设置为 ". 占用"。

2. 在 DSL 项目中，添加对 MBProvider DSL 程序集的引用。 右键单击  `MBConsumer\Dsl\References` ，然后单击 " **添加引用**"。 在 " **浏览** " 选项卡中，找到 `MBProvider\Dsl\bin\Debug\Company.MBProvider.Dsl.dll`

    这使您可以创建使用其他 DSL 的代码。 如果要创建对多个 Dsl 的引用，还可以添加它们。

3. 在 DSL 定义关系图中，右键单击关系图，然后单击 " **启用 ModelBus**"。 在对话框中，选择 " **启用此 DSL" 以使用 ModelBus**。

4. 在类中 `ExampleElement` ，添加一个新的域属性 `MBR` ，然后在属性窗口中，将其类型设置为 `ModelBusReference` 。

5. 右键单击关系图上的 "域" 属性，然后单击 " **编辑 ModelBusReference 特定属性**"。 在对话框中，选择 **一个模型元素**。

    将文件对话框筛选器设置为以下项。

    `Provider File|*.provide`

    "&#124;" 后的子字符串是 "文件选择" 对话框的筛选器。 可以通过使用 * 将其设置为允许任何文件。\*

    在 " **模型元素类型** " 列表中，输入提供程序 DSL 中一个或多个域类的名称 (例如 MBProvider) 。 它们可以是抽象类。 如果将列表留空，用户可以设置对任何元素的引用。

6. 关闭对话框并 **转换所有模板**。

   您已经创建了一个 DSL，其中包含对另一个 DSL 中的元素的引用。

### <a name="create-a-modelbus-reference-to-another-file-in-the-solution"></a>创建对解决方案中的另一个文件的 ModelBus 引用

1. 在 MBConsumer 解决方案中，按 CTRL + F5。 Visual Studio 的实验实例将在 **MBConsumer\Debugging** 项目中打开。

2. 添加示例的副本。提供给 **MBConsumer\Debugging** 项目。 这是必需的，因为 ModelBus 引用必须引用同一解决方案中的文件。

   1. 右键单击 "调试" 项目，指向 " **添加**"，然后单击 " **现有项**"。

   2. 在 " **添加项** " 对话框中，将 "筛选器" 设置为 " **所有文件" (" \* \*)**"。

   3. 导航到 `MBProvider\Debugging\Sample.provide` ，然后单击 " **添加**"。

3. 打开 `Sample.consume`。

4. 单击一个示例形状，然后在 "属性窗口中，单击 MBR 属性中的" **[...]** "。 在对话框中，单击 " **浏览** " 并选择 `Sample.provide` 。 在 "元素" 窗口中，展开 "类型" 任务，然后选择其中一个元素。

5. 保存文件。  (尚未关闭 Visual Studio 的实验实例。 ) 

   您已经创建了一个模型，其中包含对另一个模型中的元素的 ModelBus 引用。

### <a name="resolve-a-modelbus-reference-in-a-text-template"></a>解析文本模板中的 ModelBus 引用

1. 在 Visual Studio 的实验实例中，打开示例文本模板文件。 按如下所示设置其内容。

    ```
    <#@ template debug="true" hostspecific="true" language="C#"
    inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>
    <#@ MBConsumer processor="MBConsumerDirectiveProcessor" requires="fileName='Sample.consume'" #>
    <#@ output extension=".txt" #>
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>
    <#@ assembly name = "Company.MBProvider.Dsl.dll" #>
    <#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>
    <#@ import namespace="Company.MBProvider" #>
    <#
      // Property provided by the Consumer directive processor:
      ExampleModel consumerModel = this.ExampleModel;
      // Iterate through Consumer model, listing the elements:
      foreach (ExampleElement element in consumerModel.Elements)
      {
    #>
       <#= element.Name #>
    <#
        if (element.MBR != null)
      using (ModelBusAdapter adapter = this.ModelBus.CreateAdapter(element.MBR))
      {
              // If we allowed multiple types or DSLs in the MBR, discover type here.
        Task task = adapter.ResolveElementReference<Task>(element.MBR);
    #>
            <#= element.Name #> is linked to Task: <#= task==null ? "(null)" : task.Name #>
    <#
          }
      }
    #>

    ```

     请注意以下内容：

    - `hostSpecific` `inherits` `template` 必须设置指令的和特性。

    - 使用者模型通过该 DSL 中生成的指令处理器以常规方式进行访问。

    - 程序集和导入指令必须能够访问 ModelBus 以及提供程序 DSL 的类型。

    - 如果知道许多 Mbr 链接到同一个模型，则最好只调用 CreateAdapter 一次。

2. 保存模板。 验证生成的文本文件是否如下所示。

    ```
    ExampleElement1
    ExampleElement2
         ExampleElement2 is linked to Task: Task2
    ```

### <a name="resolve-a-modelbus-reference-in-a-gesture-handler"></a>解析笔势处理程序中的 ModelBus 引用

1. 如果 Visual Studio 的实验实例正在运行，则关闭它。

2. 添加一个名为 *MBConsumer\Dsl\Custom.cs* 的文件，并将其内容设置为以下内容：

    ```csharp
    namespace Company.MB2Consume
    {
      using Microsoft.VisualStudio.Modeling.Integration;
      using Company.MB3Provider;

      public partial class ExampleShape
      {
        public override void OnDoubleClick(Microsoft.VisualStudio.Modeling.Diagrams.DiagramPointEventArgs e)
        {
          base.OnDoubleClick(e);
          ExampleElement element = this.ModelElement as ExampleElement;
          if (element.MBR != null)
          {
            IModelBus modelbus = this.Store.GetService(typeof(SModelBus)) as IModelBus;
            using (ModelBusAdapter adapter = modelbus.CreateAdapter(element.MBR))
            {
              Task task = adapter.ResolveElementReference<Task>(element.MBR);
              // Open a window on this model:
              ModelBusView view = adapter.GetDefaultView();
              view.Show();
              view.SetSelection(element.MBR);
            }
          }
        }
      }
    }
    ```

3. 按 **Ctrl** + **F5**。

4. 在 Visual Studio 的实验实例中，打开 `Debugging\Sample.consume` 。

5. 双击一个形状。

    如果已在该元素上设置了 MBR，则会打开引用的模型，并选择被引用的元素。

## <a name="see-also"></a>另请参阅

- [使用 Visual Studio Modelbus 集成模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)
- [代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
