---
title: 在 Windows 窗体中嵌入图表
description: 了解如何在 Windows 控件中嵌入 DSL 关系图，该控件显示在Visual Studio窗口中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4db60267b835882a69a08c990af644b902697bad
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388979"
---
# <a name="embed-a-diagram-in-a-windows-form"></a>在 Windows 窗体中嵌入图表

可以在 Windows 控件中嵌入 DSL 关系图，该关系图显示在Visual Studio窗口中。

## <a name="embed-a-dsl-diagram-in-a-windows-control"></a>在 Windows 控件中嵌入 DSL 关系图

1. 将新的 **用户控件文件** 添加到 DslPackage 项目。

2. 将 Panel 控件添加到用户控件。 此面板将包含 DSL 关系图。

     添加需要的其他控件。

     设置控件的定位点属性。

3. 在解决方案资源管理器中，右键单击用户控件文件，然后单击"**查看代码"。** 将此构造函数和变量添加到代码中：

    ```csharp
    internal UserControl1(MyDSLDocView docView, Control content)
      : this()
    {
      panel1.Controls.Add(content);
      this.docView = docView;
    }
    private MyDSLDocView docView;
    ```

4. 将包含以下内容的新文件添加到 DslPackage 项目：

    ```csharp
    using System.Windows.Forms;
    namespace Company.MyDSL
    {
      partial class MyDSLDocView
      {
        private UserControl1 container;
        public override IWin32Window Window
        {
          get
          {
            if (container == null)
            {
              // Put our own form inside the DSL window:
              container = new UserControl1(this,
                (Control)base.Window);
            }
            return container;
    } } } }
    ```

5. 若要测试 DSL，请按 **F5** 并打开示例模型文件。 关系图显示在 控件内。 工具箱和其他功能正常运行。

## <a name="update-the-form-using-store-events"></a>使用存储事件更新窗体

1. 在窗体设计器中，添加 **名为 的 ListBox。** `listBox1` 这将显示模型中元素的列表。 它使用存储事件 与 *模型同步*。 有关详细信息，请参阅事件 [处理程序在模型 外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

2. 在自定义代码文件中，重写 DocView 类的更多方法：

    ```csharp
    partial class MyDSLDocView
    {
     /// <summary>
     /// Register store event listeners.
     /// This method is called when the model and diagram
     /// have completed loading.
     /// </summary>
     protected override bool LoadView()
      {
        bool result = base.LoadView();
        Store store = this.DocData.Store;
        EventManagerDirectory emd = store.EventManagerDirectory;
        DomainClassInfo componentClass = store.DomainDataDirectory.FindDomainClass(typeof(ExampleElement));
        emd.ElementAdded.Add(componentClass, new EventHandler<ElementAddedEventArgs>(AddElement));
        emd.ElementDeleted.Add(componentClass, new EventHandler<ElementDeletedEventArgs>(RemoveElement));

        // Do the initial parts list:
        container.SetUpFormFromModel();
        return result;
      }
     /// <summary>
     /// Listener method called on creation of each instance of
     /// the ExampleElement class or its subclasses.
     /// </summary>
     private void AddElement(object sender, ElementAddedEventArgs e)
     {
       container.Add(e.ModelElement as ExampleElement);
     }
     /// <summary>
     /// Listener method called after deletion of each instance of
     /// the ExampleElement class or its subclasses.
     /// </summary>
     private void RemoveElement(object sender, ElementDeletedEventArgs e)
     {
       container.Remove(e.ModelElement as ExampleElement);
     }
    ```

3. 在用户控件后面的代码中，插入用于侦听添加和删除的元素的方法：

    ```csharp
    public partial class UserControl1 : UserControl { ...

    private ExampleModel modelRoot;

    internal void Add(ExampleElement e) { UpdatePartsList(); }
    internal void Remove(ExampleElement e) { UpdatePartsList(); }

    internal void SetUpFormFromModel()
    {
      modelRoot = this.docView.CurrentDiagram.ModelElement as ExampleModel;
      UpdatePartsList();
    }

    private void UpdatePartsList()
    {
      StringBuilder builder = new StringBuilder();
      listBox1.Items.Clear();
      foreach (ExampleElement c in modelRoot.Elements)
      {
        listBox1.Items.Add(c.Name);
      }
    }
    ```

4. 若要测试 DSL，请按 **F5，** 在 Visual Studio实例中打开示例模型文件。

     请注意，列表框显示模型中元素的列表，在添加或删除后以及撤消和重做后，该列表框是正确的。

## <a name="see-also"></a>另请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)
