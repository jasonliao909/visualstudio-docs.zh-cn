---
title: 使用 MEF 扩展 DSL
description: 了解如何使用 MANAGED EXTENSIBILITY FRAMEWORK (MEF (DSL) 扩展特定于域) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 450a55427b9b41b8f05278c9b830acddde15608c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671855"
---
# <a name="extend-your-dsl-by-using-mef"></a>使用 MEF 扩展 DSL

可以使用 MEF (扩展特定于域) DSL Managed Extensibility Framework (语言) 。 你或其他开发人员将能够为 DSL 编写扩展，而无需更改 DSL 定义和程序代码。 此类扩展包括菜单命令、拖放处理程序和验证。 用户将能够安装 DSL，然后可以选择安装其扩展。

此外，在 DSL 中启用 MEF 时，可以更轻松地编写 DSL 的一些功能，即使这些功能都是与 DSL 一起构建的。

有关 MEF 详细信息，请参阅 meF Managed Extensibility Framework ([) 。 ](/dotnet/framework/mef/index)

### <a name="to-enable-your-dsl-to-be-extended-by-mef"></a>使 DSL 能够由 MEF 扩展

1. 在 **DslPackage** 项目中创建名为 **MefExtension** 的新文件夹。 将以下文件添加到它：

     文件名： `CommandExtensionVSCT.tt`

    > [!IMPORTANT]
    > 将此文件中的 GUID 设置为与 DslPackage\GeneratedCode\Constants.tt

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#
    // CmdSet Guid must be defined before master template is included
    // This Guid must be kept synchronized with the CommandSetId Guid in Constants.tt
    Guid guidCmdSet = new Guid ("00000000-0000-0000-0000-000000000000");
    string menuidCommandsExtensionBaseId="0x4000";
    #>
    <#@ include file="DslPackage\CommandExtensionVSCT.tt" #>
    ```

    文件名： `CommandExtensionRegistrar.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\CommandExtensionRegistrar.tt" #>
    ```

    文件名： `ValidationExtensionEnablement.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\ValidationExtensionEnablement.tt" #>
    ```

    文件名： `ValidationExtensionRegistrar.tt`

    如果添加此文件，则必须使用 DSL 资源管理器中的 **EditorValidation** 中的至少一个开关在 DSL 中启用验证。

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\ValidationExtensionRegistrar.tt" #>
    ```

    文件名： `PackageExtensionEnablement.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\PackageExtensionEnablement.tt" #>
    ```

2. 在 **Dsl** 项目中创建名为 **MefExtension** 的新文件夹。 将以下文件添加到它：

     文件名： `DesignerExtensionMetaDataAttribute.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="Dsl\DesignerExtensionMetadataAttribute.tt" #>
    ```

    文件名： `GestureExtensionEnablement.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="Dsl\GestureExtensionEnablement.tt" #>
    ```

    文件名： `GestureExtensionController.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="Dsl\GestureExtensionController.tt" #>
    ```

3. 将以下行添加到名为 **DslPackage\Commands.vsct 的现有文件**：

    ```xml
    <Include href="MefExtension\CommandExtensionVSCT.vsct"/>
    ```

    将行插入到现有 指令 `<Include>` 之后。

4. 打开 *DslDefinition.dsl*。

5. 在 DSL 资源管理器中，选择"**编辑器\验证"。**

6. 在属性窗口中，请确保至少一个名为 **Uses** 的属性为 `true` 。

7. 在 **"解决方案资源管理器"** 工具栏中，单击 **"转换所有模板"。**

     附属文件显示在添加的每个文件下方。

8. 生成并运行解决方案，验证其是否仍在工作。

DSL 现已启用 MEF。 可以将菜单命令、笔势处理程序和验证约束编写为 MEF 扩展。 可以将这些扩展与其他自定义代码一起写入 DSL 解决方案中。 此外，你或其他开发人员可以编写单独的Visual Studio扩展 DSL 的扩展。

## <a name="create-an-extension-for-a-mef-enabled-dsl"></a>为启用了 MEF 的 DSL 创建扩展

如果你有权访问自己或其他人创建的启用了 MEF 的 DSL，你可以为它编写扩展。 扩展可用于添加菜单命令、笔势处理程序或验证约束。 若要创作这些扩展，请使用 VSIX Visual Studio解决方案 (扩展) 扩展。 该解决方案包含两个部分：一个生成代码程序集的类库项目，一个打包程序集的 VSIX 项目。

### <a name="to-create-a-dsl-extension-vsix"></a>创建 DSL 扩展 VSIX

1. 创建新的“类库”项目。

2. 在新项目中，添加对 DSL 程序集的引用。

   - 此程序集的名称通常以".Dsl.dll"结尾。

   - 如果有权访问 DSL 项目，可以在目录 Dsl bin 下找到 **程序集 \\ 文件 \\ \***

   - 如果有权访问 DSL VSIX 文件，可以通过将 VSIX 文件的文件扩展名更改为".zip"来查找程序集。 解压缩.zip文件。

3. 添加对以下 .NET 程序集的引用：

   - Microsoft.VisualStudio.Modeling.Sdk.11.0.dll

   - Microsoft.VisualStudio.Modeling.Sdk.Diagrams.11.0.dll

   - Microsoft.VisualStudio.Modeling.Sdk.Shell.11.0.dll

   - System.ComponentModel.Composition.dll

   - System.Windows.Forms.dll

4. 创建新的 **VSIX 项目** 项目。

5. 在 **解决方案资源管理器** 中，右键单击 VSIX 项目，然后选择"设置为启动 **Project"。**

6. 在新项目中，打开 **source.extension.vsixmanifest**。

7. 单击"**添加内容"。** 在对话框中，将"**内容** 类型"设置为 **"MEF** 组件"，将"**源** Project"设置为类库项目。

8. 向 DSL 添加 VSIX 引用。

   1. 在 **source.extension.vsixmanifest 中，单击**" **添加引用"**

   2. 在对话框中，单击" **添加有效负载** "，然后找到 DSL 的 VSIX 文件。 VSIX 文件在 DSL 解决方案中的 **DslPackage bin \\ 中生成 \\ \***。

       这允许用户同时安装 DSL 和扩展。 如果用户已安装 DSL，则只会安装扩展。

9. 查看和更新 **source.extension.vsixmanifest 的其他字段**。 单击 **"选择版本**"，并验证Visual Studio版本是否正确。

10. 将代码添加到类库项目。 使用下一部分中的示例作为指南。

     可以添加任意数目的命令、笔势和验证类。

11. 若要测试扩展，请按 **F5**。 在 VISUAL STUDIO实例中，创建或打开 DSL 的示例文件。

## <a name="writing-mef-extensions-for-dsls"></a>为 DSL 编写 MEF 扩展

可以在单独的 DSL 扩展解决方案的程序集代码项目中编写扩展。 还可以在 DslPackage 项目中使用 MEF，作为 DSL 的一部分编写命令、手势和验证代码的简便方法。

### <a name="menu-commands"></a>菜单命令

若要编写菜单命令，请定义一个类，该类使用 DSL 中定义的属性（名为 <xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ICommandExtension> *YourDsl）实现 类并添加其前缀* `CommandExtension` 。 可以编写多个菜单命令类。

`QueryStatus()` 每当用户右单击关系图时，都会调用 。 它应检查当前选择，并设置为 `command.Enabled` 指示命令何时适用。

```csharp
using System.ComponentModel.Composition;
using System.Linq;
using Company.MyDsl; // My DSL
using Company.MyDsl.ExtensionEnablement; // My DSL
using Microsoft.VisualStudio.Modeling; // Transactions
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement; // IVsSelectionContext
using Microsoft.VisualStudio.Modeling.ExtensionEnablement; // ICommandExtension

namespace MyMefExtension
{
  // Defined in Dsl\MefExtension\DesignerExtensionMetaDataAttribute.cs:
  [MyDslCommandExtension]
  public class MyCommandClass : ICommandExtension
  {
    /// <summary>
    /// Provides access to current document and selection.
    /// </summary>
    [Import]
    IVsSelectionContext SelectionContext { get; set; }

    /// <summary>
    /// Called when the user selects this command.
    /// </summary>
    /// <param name="command"></param>
    public void Execute(IMenuCommand command)
    {
      // Transaction is required if you want to update elements.
      using (Transaction t = SelectionContext.CurrentStore
              .TransactionManager.BeginTransaction("fix names"))
      {
        foreach (ExampleShape shape in SelectionContext.CurrentSelection)
        {
          ExampleElement element = shape.ModelElement as ExampleElement;
          element.Name = element.Name + " !";
        }
        t.Commit();
      }
    }

    /// <summary>
    /// Called when the user right-clicks the diagram.
    /// Determines whether the command should appear.
    /// This method should set command.Enabled and command.Visible.
    /// </summary>
    /// <param name="command"></param>
    public void QueryStatus(IMenuCommand command)
    {
      command.Enabled =
        command.Visible = (SelectionContext.CurrentSelection.OfType<ExampleShape>().Count() > 0);
    }

    /// <summary>
    /// Called when the user right-clicks the diagram.
    /// Determines the text of the command in the menu.
    /// </summary>
    public string Text
    {
      get { return "My menu command"; }
    }
  }
}
```

### <a name="gesture-handlers"></a>笔势处理程序

笔势处理程序可以处理从任何位置、内部或外部拖动到关系图上的对象Visual Studio。 以下示例允许用户将文件从资源管理器Windows拖动到关系图上。 它创建包含文件名的元素。

可以编写处理程序来处理来自其他 DSL 模型和 UML 模型的拖动。 有关详细信息，请参阅 [如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)。

```csharp
using System.ComponentModel.Composition;
using System.Linq;
using Company.MyDsl;
using Company.MyDsl.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling; // Transactions
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;

namespace MefExtension
{
  [MyDslGestureExtension]
  class MyGestureExtension : IGestureExtension
  {
    public void OnDoubleClick(ShapeElement targetElement, DiagramPointEventArgs diagramPointEventArgs)
    {
      System.Windows.Forms.MessageBox.Show("double click!");
    }

    /// <summary>
    /// Called when the user drags anything over the diagram.
    /// Return true if the dragged object can be dropped on the current target.
    /// </summary>
    /// <param name="targetMergeElement">The shape or diagram that the mouse is currently over</param>
    /// <param name="diagramDragEventArgs">Data about the dragged element.</param>
    /// <returns></returns>
    public bool CanDragDrop(ShapeElement targetMergeElement, DiagramDragEventArgs diagramDragEventArgs)
    {
      // This handler only allows items to be dropped onto the diagram:
      return targetMergeElement is MefDsl2Diagram &&
      // And only accepts files dragged from Windows Explorer:
        diagramDragEventArgs.Data.GetFormats().Contains("FileNameW");
    }

    /// <summary>
    /// Called when the user drops an item onto the diagram.
    /// </summary>
    /// <param name="targetDropElement"></param>
    /// <param name="diagramDragEventArgs"></param>
    public void OnDragDrop(ShapeElement targetDropElement, DiagramDragEventArgs diagramDragEventArgs)
    {
      MefDsl2Diagram diagram = targetDropElement as MefDsl2Diagram;
      if (diagram == null) return;

      // This handler only accepts files dragged from Windows Explorer:
      string[] draggedFileNames = diagramDragEventArgs.Data.GetData("FileNameW") as string[];
      if (draggedFileNames == null || draggedFileNames.Length == 0) return;

      using (Transaction t = diagram.Store.TransactionManager.BeginTransaction("file names"))
      {
        // Create an element to represent each file:
        foreach (string fileName in draggedFileNames)
        {
          ExampleElement element = new ExampleElement(diagram.ModelElement.Partition);
          element.Name = fileName;

          // This method of adding the new element allows the position
          // of the shape to be specified:
          ElementGroup group = new ElementGroup(element);
          diagram.ElementOperations.MergeElementGroupPrototype(
            diagram, group.CreatePrototype(), PointD.ToPointF(diagramDragEventArgs.MousePosition));
        }
        t.Commit();
      }
    }
  }
}
```

### <a name="validation-constraints"></a>验证约束

验证方法由 DSL 生成的 属性以及 由 `ValidationExtension` 标记 <xref:Microsoft.VisualStudio.Modeling.Validation.ValidationMethodAttribute> 。 方法可以出现在任何未由属性标记的类中。

有关详细信息，请参阅在语言 [中Domain-Specific验证](../modeling/validation-in-a-domain-specific-language.md)。

```csharp
using Company.MyDsl;
using Company.MyDsl.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.Validation;

namespace MefExtension
{
  class MyValidationExtension // Can be any class.
  {
    // SAMPLE VALIDATION METHOD.
    // All validation methods have the following attributes.

    // Specific to the extended DSL:
    [MyDslValidationExtension]

    // Determines when validation is applied:
    [ValidationMethod(
       ValidationCategories.Save
     | ValidationCategories.Open
     | ValidationCategories.Menu)]

    /// <summary>
    /// When validation is executed, this method is invoked
    /// for every element in the model that is an instance
    /// of the second parameter type.
    /// </summary>
    /// <param name="context">For reporting errors</param>
    /// <param name="elementToValidate"></param>
    private void ValidateClassNames
      (ValidationContext context,
       // Type determines to what elements this will be applied:
       ExampleElement elementToValidate)
    {
      // Write code here to test values and links.
      if (elementToValidate.Name.IndexOf(' ') >= 0)
      {
        // Log any unacceptable values:
        context.LogError(
          // Description:
          "Name must not contain spaces"
          // Error code unique to this type of error:
          , "MyDsl001"
          // Element to highlight when user double-clicks error:
          , elementToValidate);
} } } }
```

## <a name="see-also"></a>另请参阅

- [传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)
- [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)
- [如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [域特定语言中的验证](../modeling/validation-in-a-domain-specific-language.md)
