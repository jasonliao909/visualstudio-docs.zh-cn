---
title: 将主机连接到生成的指令处理器
description: 了解如何扩展自定义主机，以便它支持调用指令处理器的文本模板。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- walkthroughs [text templates], connecting host to processor
- text templates, custom directive hosts
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
dev_langs:
- CSharp
- VB
ms.openlocfilehash: ed51688e5b65e34d7067963dbf7b839b1f022768
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388316"
---
# <a name="walkthrough-connect-a-host-to-a-generated-directive-processor"></a>演练：将主机连接到生成的指令处理器

可以编写自己的主机来处理文本模板。 演练：创建自定义文本模板主机 中演示 [了基本的自定义主机](../modeling/walkthrough-creating-a-custom-text-template-host.md)。 可以扩展该主机以添加函数，例如生成多个输出文件。

本演练将扩展自定义主机，以便它支持调用指令处理器的文本模板。 定义域特定语言时，它会为域 *模型* 生成指令处理器。 指令处理器使用户可以更轻松地编写访问模型的模板，减少在模板中编写程序集和导入指令的需求。

> [!NOTE]
> 本演练基于演练[：创建自定义文本模板主机 。](../modeling/walkthrough-creating-a-custom-text-template-host.md) 首先执行该演练。

本演练包含以下任务：

- 使用 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 生成基于域模型的指令处理器。

- 将自定义文本模板主机连接到生成的指令处理器。

- 使用生成的指令处理器测试自定义主机。

## <a name="prerequisites"></a>先决条件

若要定义 DSL，必须安装以下组件：

| 组件 | 链接 |
|-|-|
| Visual Studio | [http://go.microsoft.com/fwlink/?LinkId=185579](https://visualstudio.microsoft.com/) |
| [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] | [http://go.microsoft.com/fwlink/?LinkId=185580](/azure/devops/integrate/index) |
| Visual Studio 可视化和建模 SDK | |

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

此外，还必须在演练：创建自定义文本模板主机 中创建 [自定义文本模板转换](../modeling/walkthrough-creating-a-custom-text-template-host.md)。

## <a name="use-domain-specific-language-tools-to-generate-a-directive-processor"></a>使用 Domain-Specific 语言工具生成指令处理器

在此演练中，你将使用 Domain-Specific 设计器向导为解决方案 DSLMinimalTest 创建特定于域的语言。

1. 创建具有以下特征的特定于域的语言解决方案：

   - 名称：DSLMinimalTest

   - 解决方案模板：最小语言

   - 文件扩展名：最小值

   - 公司名称：Fabrikam

   有关创建域特定语言解决方案的信息，请参阅 [如何：](../modeling/how-to-create-a-domain-specific-language-solution.md)创建域Domain-Specific解决方案。

2. 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

   > [!IMPORTANT]
   > 此步骤生成指令处理器，并将该处理器的密钥添加到注册表中。

3. 在“调试”菜单上，单击“启动调试”。

    将打开第二Visual Studio实例。

4. 在实验性生成 **中，解决方案资源管理器，** 双击文件 **sample.min**。

    该文件将在设计器中打开。 请注意，该模型有两个元素：ExampleElement1 和 ExampleElement2，以及它们之间的链接。

5. 关闭第二个 Visual Studio。

6. 保存解决方案，然后关闭Domain-Specific设计器。

## <a name="connect-a-custom-text-template-host-to-a-directive-processor"></a>将自定义文本模板主机连接到指令处理器

生成指令处理器后，将连接指令处理器和在演练：创建自定义文本模板主机 中创建的 [自定义文本模板主机](../modeling/walkthrough-creating-a-custom-text-template-host.md)。

1. 打开 CustomHost 解决方案。

2. 在“项目”菜单上，单击“添加引用”。

     " **添加引用** "对话框随即打开，并显示 **".NET"** 选项卡。

3. 添加以下引用：

    - Microsoft.VisualStudio.Modeling.Sdk.11.0

    - Microsoft.VisualStudio.Modeling.Sdk.Diagrams.11.0

    - Microsoft.VisualStudio.TextTemplating.11.0

    - Microsoft.VisualStudio.TextTemplating.Interfaces.11.0

    - Microsoft.VisualStudio.TextTemplating.Modeling.11.0

    - Microsoft.VisualStudio.TextTemplating.VSHost.11.0

4. 在 Program.cs 或 Module1.vb 的顶部，添加以下代码行：

    ```csharp
    using Microsoft.Win32;
    ```

    ```vb
    Imports Microsoft.Win32
    ```

5. 找到 属性的代码， `StandardAssemblyReferences` 并将其替换为以下代码：

    > [!NOTE]
    > 在此步骤中，将添加对主机将支持的生成的指令处理器所需的程序集的引用。

    ```csharp
    //the host can provide standard assembly references
    //the engine will use these references when compiling and
    //executing the generated transformation class
    //--------------------------------------------------------------
    public IList<string> StandardAssemblyReferences
    {
        get
        {
            return new string[]
            {
                //if this host searches standard paths and the GAC
                //we can specify the assembly name like this:
                //"System"
                //since this host only resolves assemblies from the
                //fully qualified path and name of the assembly
                //this is a quick way to get the code to give us the
                //fully qualified path and name of the System assembly
                //---------------------------------------------------------
                typeof(System.Uri).Assembly.Location,
                            typeof(System.Uri).Assembly.Location,
                typeof(Microsoft.VisualStudio.Modeling.ModelElement).Assembly.Location,
                typeof(Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape).Assembly.Location,
                typeof(Microsoft.VisualStudio.TextTemplating.VSHost.ITextTemplating).Assembly.Location,
                typeof(Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation).Assembly.Location

            };
        }
    }
    ```

6. 找到函数 的代码， `ResolveDirectiveProcessor` 并将其替换为以下代码：

    > [!IMPORTANT]
    > 此代码包含对要连接到的已生成指令处理器的名称的硬编码引用。 你可以轻松地使这更通用，在这种情况下，它会查找注册表中列出的所有指令处理器，并尝试查找匹配项。 在这种情况下，主机将处理任何生成的指令处理器。

    ```csharp
    //the engine calls this method based on the directives the user has
            //specified it in the text template
            //this method can be called 0, 1, or more times
            //---------------------------------------------------------------------
            public Type ResolveDirectiveProcessor(string processorName)
            {
                //check the processor name, and if it is the name of the processor the
                //host wants to support, return the type of the processor
                //---------------------------------------------------------------------
                if (string.Compare(processorName, "DSLMinimalTestDirectiveProcessor", StringComparison.InvariantCultureIgnoreCase) == 0)
                {
                    try
                    {
                        string keyName = @"Software\Microsoft\VisualStudio\10.0Exp_Config\TextTemplating\DirectiveProcessors\DSLMinimalTestDirectiveProcessor";
                        using (RegistryKey specificKey = Registry.CurrentUser.OpenSubKey(keyName))
                        {
                            if (specificKey != null)
                            {
                                List<string> names = new List<String>(specificKey.GetValueNames());
                                string classValue = specificKey.GetValue("Class") as string;
                                if (!string.IsNullOrEmpty(classValue))
                                {
                                    string loadValue = string.Empty;
                                    System.Reflection.Assembly processorAssembly = null;
                                    if (names.Contains("Assembly"))
                                    {
                                        loadValue = specificKey.GetValue("Assembly") as string;
                                        if (!string.IsNullOrEmpty(loadValue))
                                        {
                                            //the assembly must be installed in the GAC
                                            processorAssembly = System.Reflection.Assembly.Load(loadValue);
                                        }
                                    }
                                    else if (names.Contains("CodeBase"))
                                    {
                                        loadValue = specificKey.GetValue("CodeBase") as string;
                                        if (!string.IsNullOrEmpty(loadValue))
                                        {
                                            //loading local assembly
                                            processorAssembly = System.Reflection.Assembly.LoadFrom(loadValue);
                                        }
                                    }
                                    if (processorAssembly == null)
                                    {
                                        throw new Exception("Directive Processor not found");
                                    }
                                    Type processorType = processorAssembly.GetType(classValue);
                                    if (processorType == null)
                                    {
                                        throw new Exception("Directive Processor not found");
                                    }
                                    return processorType;
                                }
                            }
                        }
                    }
                    catch (Exception e)
                    {
                        //if the directive processor can not be found, throw an error
                        throw new Exception("Directive Processor not found");
                    }
                }

                //if the directive processor is not one this host wants to support
                throw new Exception("Directive Processor not supported");
            }
    ```

7. 在“文件”  菜单上，单击“全部保存” 。

8. 在“生成”菜单中，单击“生成解决方案”。

## <a name="test-the-custom-host-with-the-directive-processor"></a>使用指令处理器测试自定义主机

若要测试自定义文本模板主机，首先必须编写一个调用生成的指令处理器的文本模板。 然后运行自定义主机，将文本模板的名称传递给它，并验证指令是否得到正确处理。

### <a name="create-a-text-template-to-test-the-custom-host"></a>创建文本模板以测试自定义主机

1. 创建文本文件，并命名它 `TestTemplateWithDP.tt` 。 可以使用任何文本编辑器（如记事本）来创建文件。

2. 向文本文件中添加以下内容：

    > [!NOTE]
    > 文本模板的编程语言不需要与自定义主机的编程语言匹配。

    ```csharp
    Text Template Host Test

    <#@ template debug="true" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>
    <# //this is the call to the examplemodel directive in the generated directive processor #>
    <#@ DSLMinimalTest processor="DSLMinimalTestDirectiveProcessor" requires="fileName='<Your Path>\Sample.min'" provides="ExampleModel=ExampleModel" #>
    <# //uncomment this line to test that the host allows the engine to set the extension #>
    <# //@ output extension=".htm" #>

    <# //uncomment this line if you want to see the generated transformation class #>
    <# //System.Diagnostics.Debugger.Break(); #>
    <# //this code uses the results of the examplemodel directive #>
    <#
        foreach ( ExampleElement box in this.ExampleModel.Elements )
        {
            WriteLine("Box: {0}", box.Name);

            foreach (ExampleElement linkedTo in box.Targets)
            {
                WriteLine("Linked to: {0}", linkedTo.Name);
            }

            foreach (ExampleElement linkedFrom in box.Sources)
            {
                WriteLine("Linked from: {0}", linkedFrom.Name);
            }

            WriteLine("");
        }
    #>
    ```

    ```vb
    Text Template Host Test

    <#@ template debug="true" language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>

    <# 'this is the call to the examplemodel directive in the generated directive processor #>
    <#@ DSLMinimalTest processor="DSLMinimalTestDirectiveProcessor" requires="fileName='<Your Path>\Sample.min'" provides="ExampleModel=ExampleModel" #>

    <# 'Uncomment this line to test that the host allows the engine to set the extension. #>
    <# '@ output extension=".htm" #>

    <# 'Uncomment this line if you want to see the generated transformation class. #>
    <# 'System.Diagnostics.Debugger.Break() #>

    <# 'this code uses the results of the examplemodel directive #>

    <#
       For Each box as ExampleElement In Me.ExampleModel.Elements

           WriteLine("Box: {0}", box.Name)

            For Each LinkedTo as ExampleElement In box.Targets
                WriteLine("Linked to: {0}", LinkedTo.Name)
            Next

            For Each LinkedFrom as ExampleElement In box.Sources
                WriteLine("Linked from: {0}", LinkedFrom.Name)
            Next

            WriteLine("")

       Next
    #>
    ```

3. 在代码中，将 替换为第一个过程中创建的设计特定语言中 \<YOUR PATH> Sample.min 文件的路径。

4. 保存并关闭该文件。

### <a name="test-the-custom-host"></a>测试自定义主机

1. 打开命令提示符窗口。

2. 为自定义宿主键入可执行文件的路径，但暂不要按 Enter。

     例如，键入：

     `<YOUR PATH>CustomHost\bin\Debug\CustomHost.exe`

    > [!NOTE]
    > 可以浏览到 CustomHost.exe 中的文件 **Windows 资源管理器，然后将** 该文件拖到命令提示符窗口中，而不是键入地址。

3. 键入一个空格。

4. 键入文本模板文件的路径，然后按 Enter。

     例如，键入：

     `<YOUR PATH>TestTemplateWithDP.txt`

    > [!NOTE]
    > 可以浏览到 TestTemplateWithDP.txt 中的文件 **Windows 资源管理器，然后将** 该文件拖到命令提示符窗口中，而不是键入地址。

     自定义主机应用程序运行并启动文本模板转换过程。

5. 在 **Windows 资源管理器** 中，浏览到包含文件文件夹TestTemplateWithDP.txt。

     文件夹还包含文件TestTemplateWithDP1.txt。

6. 打开此文件可以查看文本模板转换的结果。

     生成的文本输出结果将显示，应如下所示：

    ```
    Text Template Host Test

    Box: ExampleElement1
    Linked to: ExampleElement2

    Box: ExampleElement2
    Linked from: ExampleElement1
    ```

## <a name="see-also"></a>另请参阅

- [演练：创建自定义文本模板宿主](../modeling/walkthrough-creating-a-custom-text-template-host.md)
