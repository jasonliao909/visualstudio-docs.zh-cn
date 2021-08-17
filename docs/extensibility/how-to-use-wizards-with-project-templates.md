---
title: 如何：使用向导来处理项目模板
description: 了解如何使用 Visual Studio SDK 中的 IWizard 接口，该接口使用户能够在用户从模板创建项目时运行自定义代码。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122095057"
---
# <a name="how-to-use-wizards-with-project-templates"></a>如何：将向导与项目模板一同使用

Visual Studio 提供了 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口，可实现该接口来在用户从模板创建项目时运行自定义代码。

Project模板自定义可用于显示自定义 UI，该 UI 收集用户输入以自定义模板、将其他文件添加到模板或项目上允许的其他任何操作。

创建项目时，会从用户单击"新建项目"对话框中的"确定"开始， <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> **在** Project调用接口方法。 接口的每个方法都命名为 ，用于描述调用它的点。 例如，Visual Studio项目时立即调用 ，因此它是编写自定义代码以 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> 收集用户输入的良好位置。

## <a name="create-a-project-template-project-with-a-vsix-project"></a>使用 VSIX 项目创建项目模板项目

开始使用项目模板项目创建自定义模板，该项目是 Visual Studio SDK 的一部分。 在此过程中，我们将使用 C# 项目模板项目，但还有一个Visual Basic模板项目。 然后将 VSIX 项目添加到包含项目模板项目的解决方案。

1. 在 (创建 C# 项目模板Visual Studio，选择"文件""Project"，然后搜索"  >    >  项目模板") 。 将名称命名 **为 MyProjectTemplate**。

   > [!NOTE]
   > 系统可能会要求你安装 Visual Studio SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

2. 在 解决方案资源管理器 中的项目模板项目 **(** 的同一解决方案中添加一个新的 VSIX 项目，选择解决方案节点，右键单击并选择"添加新Project  >  **并** 搜索"vsix") 。 将名称命名 **为 MyProjectWizard。**

3. 将 VSIX 项目设置为启动项目。 在 **解决方案资源管理器** 中，选择 VSIX 项目节点，右键单击并选择"设置为启动 **Project"。**

4. 将模板项目添加为 VSIX 项目的资产。 在 **解决方案资源管理器** 中，在 VSIX 项目节点下，找到 *source.extension.vsixmanifest* 文件。 双击它，在清单编辑器中打开它。

5. 在清单编辑器中 **，选择窗口** 左侧的"资产"选项卡。

6. 在"**资产"选项卡** 中，选择"新建 **"。** 在"**添加新资产"** 窗口中，对于"类型"字段，选择 **"Microsoft.VisualStudio.ProjectTemplate"。** 在" **源"** 字段中， **选择当前解决方案 中的项目**。 在 **"Project"** 字段中，选择 **"MyProjectTemplate"。** 然后单击“确定”。

7. 生成解决方案并启动调试。 将出现 Visual Studio 的第二个实例。 （这可能需要几分钟的时间。）

8. 在 Visual Studio (的第二个实例中，尝试使用新模板"文件""新建Project"创建新Project，然后搜索  >    >  "myproject") 。 新项目应显示一个名为 **Class1** 的类。 现已创建自定义项目模板！ 现在停止调试。

## <a name="create-a-custom-template-wizard"></a>创建自定义模板向导

此过程演示如何创建一个自定义向导，该向导在Windows窗体之前打开窗体。 窗体允许用户添加在项目创建过程中添加到源代码中的自定义参数值。

1. 设置 VSIX 项目以允许其创建程序集。

2. 在 **解决方案资源管理器** 中，选择 VSIX 项目节点。 在 **解决方案资源管理器** 中，应会看到" **属性"** 窗口。 如果没有，请选择"查看  >  **属性窗口"，** 或按 **F4**。 在" **属性** "窗口中，选择以下字段 `true` 以 ：

   - **在 VSIX 容器中包含程序集**

   - **在 VSIX 容器中包括调试符号**

   - **在本地 VSIX 部署中包括调试符号**

3. 将程序集作为资产添加到 VSIX 项目。 打开 *source.extension.vsixmanifest 文件，然后选择*"**资产"** 选项卡。在"**添加新资产**"窗口中，对于"类型"，选择 **"Microsoft.VisualStudio.Assembly"，** 对于 **"源"，请选择"当前解决方案** 中的项目"，对于"Project选择 **"MyProjectWizard"。**  

4. 添加对 VSIX 项目的以下引用。  (在 **解决方案资源管理器** 中，在 VSIX 项目节点下，选择"引用"，右键单击并选择"添加引用 .) "。在"添加引用"对话框中，在"**框架**"选项卡中，找到 **"System.Windows Forms"程序集并选择它**。 另请查找并选择 **"System"** 和 **"System.Drawing"** 程序集。 现在，选择 **"扩展"** 选项卡。找到 **EnvDTE** 程序集并选择它。 另请找到 **Microsoft.VisualStudio.TemplateWizardInterface** 程序集并选择它。 单击“确定”。

5. 将向导实现类添加到 VSIX 项目。   **("解决方案资源管理器"** 中，右键单击 VSIX 项目节点，然后选择"添加"，然后选择"新建项 **"，然后选择"** 类 .) 将类命名 **WizardImplementation"。**

6. 将 *WizardImplementationClass.cs* 文件中的代码替换为以下代码：

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

    稍后将实现此代码中引用的 **UserInputForm。**

    类 `WizardImplementation` 包含 每个成员的方法实现 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 。 此示例中，只有 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> 方法执行任务。 所有其他方法要么不执行任何操作，要么返回 `true` 。

    方法 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> 接受四个参数：

   - <xref:System.Object>可强制转换到根对象的参数 <xref:EnvDTE._DTE> ，用于自定义项目。

   - <xref:System.Collections.Generic.Dictionary%602>一个参数，它包含模板中所有预定义参数的集合。 有关模板参数详细信息，请参阅 [模板参数](../ide/template-parameters.md)。

   - 一 <xref:Microsoft.VisualStudio.TemplateWizard.WizardRunKind> 个参数，其中包含有关所使用的模板类型的信息。

   - 一 <xref:System.Object> 个数组，其中包含由向导传递的一组Visual Studio。

     此示例将用户输入窗体中的参数值添加到 <xref:System.Collections.Generic.Dictionary%602> 参数。 项目中参数 `$custommessage$` 的每一个实例都将替换为用户输入的文本。

7. 现在创建 **UserInputForm**。 在 *WizardImplementation.cs* 文件中，在 类的末尾添加以下 `WizardImplementation` 代码。

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

    用户输入窗体提供用于输入自定义参数的简单窗体。 窗体包含一个名为 的文本框 `textBox1` 和一个名为 的按钮 `button1` 。 单击按钮时，文本框中的文本将存储在 参数 `customMessage` 中。

## <a name="connect-the-wizard-to-the-custom-template"></a>连接向导到自定义模板

为了使自定义项目模板使用自定义向导，需要对向导程序集进行签名，并添加一些行到自定义项目模板，以便它知道在新建项目时在何处可以找到向导实现。

1. 对程序集进行签名。 在 **"解决方案资源管理器"** 中，选择 VSIX 项目，右键单击并选择"Project **属性"。**

2. 在 **"Project"** 窗口中，选择"签名 **"** 选项卡。在"签名"选项卡中，选中"**对程序集进行签名"。** 在" **选择强名称密钥文件"字段中** ，选择 **\<New>** 。 在" **创建强名称密钥** "窗口的" **密钥文件名"** 字段中，键入 **key.snk**。 取消选中 **"使用密码保护我的密钥文件"** 字段。

3. 在 **"解决方案资源管理器"** 中，选择 VSIX 项目并找到" **属性"** 窗口。

4. 将"**将生成输出复制到输出目录"** 字段设置为 **true。** 这允许在重新生成解决方案时将程序集复制到输出目录中。 它仍包含在 `.vsix` 文件中。 需要查看程序集才能找到其签名密钥。

5. 重新生成解决方案。

6. 现在可以在 MyProjectWizard 项目目录 (*\<your disk location> \MyProjectTemplate\MyProjectWizard\key.snk*) 中查找 key.snk 文件。 复制 *key.snk* 文件。

7. 转到输出目录，找到 *\<your disk location> \MyProjectTemplate/ (\MyProjectTemplate/MyProjectWizard\bin\Debug\MyProjectWizard.dll) 。* 在此处 *粘贴 key.snk* 文件。  (这不是绝对必要的，但会简化以下步骤。) 

8. 打开命令窗口，并更改为已创建程序集的目录。

9. 找到 *sn.exe* 签名工具。 例如，在 Windows 10 64 位操作系统上，典型的路径如下：

     *C：\Program Files (x86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.6.1 Tools*

     如果找不到该工具，请尝试在命令窗口中运行 **/R sn.exe** 。 记下路径。

10. 从 *密钥 .snk* 文件中提取公钥。 在命令窗口中，键入

     **\<location of sn.exe>\sn.exe-p 密钥 .snk。密钥。**

     如果目录名称中有空格，请不要忘记用引号将 *sn.exe* 的路径括起来！

11. 从 outfile 获取公钥标记：

     **\<location of sn.exe>\sn.exe。**

     同样，不要忘记引号。 输出中应会显示一行，如下所示

     **公钥标记为 \<token>**

     记下此值。

12. 将对自定义向导的引用添加到项目模板的 *.vstemplate* 文件中。 在 **解决方案资源管理器** 中，找到名为 *MyProjectTemplate* 的文件，然后将其打开。 在此部分结束后 \<TemplateContent> ，添加以下部分：

    ```xml
    <WizardExtension>
        <Assembly>MyProjectWizard, Version=1.0.0.0, Culture=Neutral, PublicKeyToken=token</Assembly>
        <FullClassName>MyProjectWizard.WizardImplementation</FullClassName>
    </WizardExtension>
    ```

     其中， **MyProjectWizard** 是程序集的名称，而 **标记** 是在上一步中复制的标记。

13. 保存项目中的所有文件，然后重新生成。

## <a name="add-the-custom-parameter-to-the-template"></a>将自定义参数添加到模板

在此示例中，用作模板的项目显示在 "自定义向导" 的 "用户输入" 窗体中指定的消息。

1. 在 **解决方案资源管理器** 中，请切换到 **MyProjectTemplate** 项目并打开 *Class1*。

2. 在 `Main` 应用程序的方法中，添加以下代码行。

   ```csharp
   Console.WriteLine("$custommessage$");
   ```

    `$custommessage$`当从模板创建项目时，将参数替换为在用户输入窗体中输入的文本。

下面是完整的代码文件，然后将其导出到模板。

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

现在，可以从模板创建一个项目，并使用自定义向导。

1. 重新生成解决方案并启动调试。 将显示 Visual Studio 的第二个实例。

2. 创建新的 MyProjectTemplate 项目。 )  (**文件**  >    >  **Project** 。

3. 在 "**新建 Project** " 对话框中，搜索 "myproject" 以查找模板，键入名称，然后单击 **"确定**"。

     此时将打开向导用户输入窗体。

4. 键入自定义参数的值，然后单击 "" 按钮。

     向导用户输入窗体将关闭，并且将从该模板创建一个项目。

5. 在 **解决方案资源管理器** 中，右键单击源代码文件，然后单击 " **查看代码**"。

     请注意，已 `$custommessage$` 替换为在向导用户输入窗体中输入的文本。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TemplateWizard.IWizard>
- [自定义模板](../ide/customizing-project-and-item-templates.md)
- [WizardExtension 元素 (Visual Studio 模板) ](../extensibility/wizardextension-element-visual-studio-templates.md)
- [Visual Studio 模板中的 NuGet 包](/nuget/visual-studio-extensibility/visual-studio-templates)
