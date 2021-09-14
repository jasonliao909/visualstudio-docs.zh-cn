---
title: 如何：使用向导来处理项目模板
description: 了解如何使用 Visual Studio SDK 中的 IWizard 接口，通过该接口，您可以在用户从模板创建项目时运行自定义代码。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- project templates [Visual Studio], wizards
- Visual Studio templates, wizards
- wizards [Visual Studio], project templates
- templates [Visual Studio], wizards
- IWizard interface
ms.assetid: 47ee26cf-67b7-4ff1-8a9d-ab11a725405c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: cc023655c42ea63db5015d00a33ce140275f6ee0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600766"
---
# <a name="how-to-use-wizards-with-project-templates"></a>如何：将向导与项目模板结合使用

Visual Studio 提供了 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口，可实现该接口来在用户从模板创建项目时运行自定义代码。

Project 模板自定义项可用于显示自定义 UI，该 UI 可收集用户输入来自定义模板、向模板添加其他文件或在项目中允许的任何其他操作。

<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>当创建项目时，会在用户单击 "**新建 Project** " 对话框中的 **"确定"** 后立即调用接口方法。 接口的每个方法都命名为，以描述它的调用点。 例如，Visual Studio <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> 在开始创建项目时立即调用，使其成为编写自定义代码以收集用户输入的良好位置。

## <a name="create-a-project-template-project-with-a-vsix-project"></a>使用 VSIX 项目创建项目模板项目

开始使用项目模板项目创建自定义模板，该模板是 Visual Studio SDK 的一部分。 在此过程中，我们将使用 c # 项目模板项目，但还有一个 Visual Basic 项目模板项目。 然后向包含项目模板项目的解决方案中添加一个 VSIX 项目。

1. 创建 c # 项目模板项目 (在 Visual Studio 中，选择 "**文件**  >  " "**新建**"  >  **Project** 并搜索 "项目模板" ) 。 将其命名为 **MyProjectTemplate**。

   > [!NOTE]
   > 系统可能会要求你安装 Visual Studio SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

2. 在 **解决方案资源管理器** 的项目模板项目 (中添加新的 VSIX 项目，选择 "解决方案" 节点，右键单击，然后选择 "**添加**  >  **新 Project** " 并搜索 "VSIX" ) 。 将其命名为 **MyProjectWizard。**

3. 将 VSIX 项目设置为启动项目。 在 **解决方案资源管理器** 中，选择 "VSIX 项目" 节点，右键单击，然后选择 "**设为启动 Project**"。

4. 将模板项目添加为 VSIX 项目的资产。 在 **解决方案资源管理器** 的 "VSIX 项目" 节点下，找到 *source.extension.vsixmanifest* 文件。 双击以在清单编辑器中打开它。

5. 在清单编辑器中，选择窗口左侧的 " **资产** " 选项卡。

6. 在 " **资产** " 选项卡中，选择 " **新建**"。 在 " **添加新资产** " 窗口中，为 "类型" 字段选择 " **VisualStudio**"。 在 " **源** " 字段中，选择 " **当前解决方案中的项目**"。 在 " **Project** " 字段中，选择 " **MyProjectTemplate**"。 。

7. 生成解决方案并启动调试。 将出现 Visual Studio 的第二个实例。 （这可能需要几分钟的时间。）

8. 在 Visual Studio 的第二个实例中，尝试使用新模板 (**File** new Project 创建新的项目  >    >  ，搜索 "myproject" ) 。 新项目应显示一个名为 **Class1** 的类。 你现在已创建自定义项目模板！ 立即停止调试。

## <a name="create-a-custom-template-wizard"></a>创建自定义模板向导

此过程说明如何创建自定义向导，以便在创建项目之前打开 Windows 窗体。 使用窗体，用户可以添加在项目创建期间添加到源代码的自定义参数值。

1. 设置 VSIX 项目以允许它创建程序集。

2. 在 **解决方案资源管理器** 中，选择 "VSIX 项目" 节点。 在 **解决方案资源管理器** 下，应会看到 " **属性** " 窗口。 如果不这样做，请选择 "**查看**  >  **属性" 窗口**，或者按 **F4**。 在 " **属性** " 窗口中，选择以下字段以 `true` 执行以下操作：

   - **在 VSIX 容器中包含程序集**

   - **在 VSIX 容器中包含调试符号**

   - **在本地 VSIX 部署中包含调试符号**

3. 将程序集作为资产添加到 VSIX 项目。 打开 *source.extension.vsixmanifest* 文件，然后选择 "**资产**" 选项卡。在 "**添加新资产**" 窗口中，为 "**类型**" 选择 " **VisualStudio**"，对于 "源"，选择 "**当前解决方案中的项目**"， **Project** 并选择 " **MyProjectWizard**" 作为 "**源**"。

4. 将以下引用添加到 VSIX 项目。  (在 **解决方案资源管理器** 的 "VSIX 项目" 节点下，选择 "**引用**"，右键单击，然后选择 "**添加引用**" ) 。在 "**添加引用**" 对话框的 "**框架**" 选项卡中，找到 " **Windows 窗体**" 程序集并选择它。 同时，查找并选择 " **系统** " 和 " **系统** " 程序集。 现在选择 " **扩展** " 选项卡。找到 **EnvDTE** 程序集并将其选中。 同时，查找 **TemplateWizardInterface** 程序集并将其选中。 单击“确定”。

5. 将向导实现的类添加到 VSIX 项目。  (在 **解决方案资源管理器** 中，右键单击 VSIX 项目节点，然后依次选择 "**添加**"、"**新建项**" 和 ") **类**"，然后将 WizardImplementation 类命名为。

6. 将 *WizardImplementationClass* 文件中的代码替换为以下代码：

   ```csharp
   using System;
   using System.Collections.Generic;
   using Microsoft.VisualStudio.TemplateWizard;
   using System.Windows.Forms;
   using EnvDTE;

   namespace MyProjectWizard
   {
       public class WizardImplementation:IWizard
       {
           private UserInputForm inputForm;
           private string customMessage;

           // This method is called before opening any item that
           // has the OpenInEditor attribute.
           public void BeforeOpeningFile(ProjectItem projectItem)
           {
           }

           public void ProjectFinishedGenerating(Project project)
           {
           }

           // This method is only called for item templates,
           // not for project templates.
           public void ProjectItemFinishedGenerating(ProjectItem
               projectItem)
           {
           }

           // This method is called after the project is created.
           public void RunFinished()
           {
           }

           public void RunStarted(object automationObject,
               Dictionary<string, string> replacementsDictionary,
               WizardRunKind runKind, object[] customParams)
           {
               try
               {
                   // Display a form to the user. The form collects
                   // input for the custom message.
                   inputForm = new UserInputForm();
                   inputForm.ShowDialog();

                   customMessage = UserInputForm.CustomMessage;

                   // Add custom parameters.
                   replacementsDictionary.Add("$custommessage$",
                       customMessage);
               }
               catch (Exception ex)
               {
                   MessageBox.Show(ex.ToString());
               }
           }

           // This method is only called for item templates,
           // not for project templates.
           public bool ShouldAddProjectItem(string filePath)
           {
               return true;
           }
       }
   }
   ```

    稍后将实现在此代码中引用的 **UserInputForm** 。

    `WizardImplementation`类包含的每个成员的方法实现 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 。 在此示例中，只有 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> 方法执行任务。 所有其他方法要么不执行任何操作 `true` ，要么返回。

    此 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> 方法接受四个参数：

   - 一个 <xref:System.Object> 可以强制转换为根对象的参数 <xref:EnvDTE._DTE> ，以使您能够自定义项目。

   - 一个 <xref:System.Collections.Generic.Dictionary%602> 参数，该参数包含模板中所有预定义参数的集合。 有关模板参数的详细信息，请参阅 [模板参数](../ide/template-parameters.md)。

   - 一个 <xref:Microsoft.VisualStudio.TemplateWizard.WizardRunKind> 参数，该参数包含有关所使用的模板类型的信息。

   - 一个 <xref:System.Object> 数组，该数组包含通过 Visual Studio 传递到向导的一组参数。

     此示例将用户输入窗体中的参数值添加到 <xref:System.Collections.Generic.Dictionary%602> 参数中。 项目中参数的每个实例 `$custommessage$` 都将替换为用户输入的文本。

7. 现在，创建 **UserInputForm**。 在 *WizardImplementation* 文件中，在类的末尾添加以下代码 `WizardImplementation` 。

   ```csharp
   public partial class UserInputForm : Form
       {
           private static string customMessage;
           private TextBox textBox1;
           private Button button1;

           public UserInputForm()
           {
               this.Size = new System.Drawing.Size(155, 265);

               button1 = new Button();
               button1.Location = new System.Drawing.Point(90, 25);
               button1.Size = new System.Drawing.Size(50, 25);
               button1.Click += button1_Click;
               this.Controls.Add(button1);

               textBox1 = new TextBox();
               textBox1.Location = new System.Drawing.Point(10, 25);
               textBox1.Size = new System.Drawing.Size(70, 20);
               this.Controls.Add(textBox1);
           }
           public static string CustomMessage
           {
               get
               {
                   return customMessage;
               }
               set
               {
                   customMessage = value;
               }
           }
           private void button1_Click(object sender, EventArgs e)
           {
               customMessage = textBox1.Text;
               this.Close();
           }
       }
   ```

    用户输入窗体提供了一个用于输入自定义参数的简单窗体。 该窗体包含一个名为的文本框 `textBox1` 和一个名为的按钮 `button1` 。 单击该按钮时，文本框中的文本将存储在 `customMessage` 参数中。

## <a name="connect-the-wizard-to-the-custom-template"></a>将向导连接到自定义模板

为了使您的自定义项目模板可以使用您的自定义向导，您需要对向导程序集进行签名，并向您的自定义项目模板添加一些行，以让它知道在创建新项目时在何处查找向导实现。

1. 为程序集签名。 在 **解决方案资源管理器** 中，选择 VSIX 项目，右键单击，然后选择 " **Project 属性**"。

2. 在 " **Project 属性**" 窗口中，选择 "**签名**" 选项卡。在 "**签名**" 选项卡中，选中 "**为程序集签名"**。 在 " **选择强名称密钥文件** " 字段中，选择 **\<New>** 。 在 " **创建强名称密钥** " 窗口的 " **密钥文件名称** " 字段中，键入 " **key .snk**"。 取消选中 " **使用密码保护密钥文件** " 字段。

3. 在 **解决方案资源管理器** 中，选择 VSIX 项目并找到 " **属性** " 窗口。

4. 将 " **将生成输出复制到输出目录** " 字段设置为 " **true**"。 这允许在重新生成解决方案时将程序集复制到输出目录中。 它仍包含在文件中 `.vsix` 。 需要查看程序集才能查找其签名密钥。

5. 重新生成解决方案。

6. 你现在可以在 MyProjectWizard 项目目录中找到密钥 .snk 文件 (*\<your disk location> \MyProjectTemplate\MyProjectWizard\key.snk*) 。 复制 *密钥 .snk* 文件。

7. 中转到输出目录，查找 (*\<your disk location> \ MyProjectTemplate/MyProjectWizard\bin\Debug\MyProjectWizard.dll*) 的程序集。 将 *密钥 .snk* 文件粘贴到此处。 这并不是绝对必要的 (，但这会使以下步骤更简单。 ) 

8. 打开命令窗口，并更改为创建该程序集的目录。

9. 查找 *sn.exe* 签名工具。 例如，在 Windows 10 64 位操作系统上，典型路径如下：

     *C:\Program 文件 (x86) \microsoft sdk \ Windows \v10.0A\bin\NETFX 4.6.1 工具*

     如果找不到该工具，请在命令窗口中尝试运行 **sn.exe** 。 记下该路径。

10. 从 *key.snk 文件中提取* 公钥。 在命令窗口中，键入

     **\<location of sn.exe>\sn.exe -p key.snk outfile.key。**

     如果目录名称中具有空格 *，sn.exe* 用引号括起来！

11. 从 outfile 获取公钥令牌：

     **\<location of sn.exe>\sn.exe -t outfile.key。**

     同样，不要忘记引号。 输出中应显示如下所示的行

     **公钥令牌为 \<token>**

     记下此值。

12. 向项目模板的 *.vstemplate* 文件添加对自定义向导的引用。 在 **解决方案资源管理器中**，找到名为 *MyProjectTemplate.vstemplate* 的文件并打开它。 在 节的末尾 \<TemplateContent> ，添加以下部分：

    ```xml
    <WizardExtension>
        <Assembly>MyProjectWizard, Version=1.0.0.0, Culture=Neutral, PublicKeyToken=token</Assembly>
        <FullClassName>MyProjectWizard.WizardImplementation</FullClassName>
    </WizardExtension>
    ```

     其中 **MyProjectWizard** 是程序集的名称 **，token** 是在上一步中复制的令牌。

13. 保存项目的所有文件并重新生成。

## <a name="add-the-custom-parameter-to-the-template"></a>将自定义参数添加到模板

此示例中，用作模板的项目显示自定义向导的用户输入形式中指定的消息。

1. 在 **解决方案资源管理器** 中，转到 **MyProjectTemplate** 项目并打开 *Class1.cs*。

2. 在 `Main` 应用程序的 方法中，添加以下代码行。

   ```csharp
   Console.WriteLine("$custommessage$");
   ```

    从模板创建项目时，参数将替换为在用户输入表单 `$custommessage$` 中输入的文本。

下面是导出到模板之前的完整代码文件。

```csharp
using System;
using System.Collections.Generic;
$if$ ($targetframeworkversion$ >= 3.5)using System.Linq;
$endif$using System.Text;

namespace $safeprojectname$
{
    public class Class1
    {
          static void Main(string[] args)
          {
               Console.WriteLine("$custommessage$");
          }
    }
}
```

## <a name="use-the-custom-wizard"></a>使用自定义向导

现在，可以从模板创建项目并使用自定义向导。

1. 重新生成解决方案并开始调试。 将显示 Visual Studio 的第二个实例。

2. 创建新的 MyProjectTemplate 项目。  (  >  **文件新建**  >  **Project) 。**

3. 在 **"新建Project"** 对话框中，搜索"myproject"以查找模板，键入名称，然后单击"确定 **"。**

     向导用户输入窗体随即打开。

4. 键入自定义参数的值，然后单击按钮。

     向导用户输入窗体关闭，并且从模板创建项目。

5. 在 **解决方案资源管理器** 中，右键单击源代码文件，然后单击"**查看代码"。**

     请注意 `$custommessage$` ， 已替换为在向导用户输入表单中输入的文本。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TemplateWizard.IWizard>
- [自定义模板](../ide/customizing-project-and-item-templates.md)
- [WizardExtension 元素 (Visual Studio模板) ](../extensibility/wizardextension-element-visual-studio-templates.md)
- [Visual Studio 模板中的 NuGet 包](/nuget/visual-studio-extensibility/visual-studio-templates)
