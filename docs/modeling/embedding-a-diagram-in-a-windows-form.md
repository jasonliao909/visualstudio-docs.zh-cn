---
title: 在 Windows 窗体中嵌入图表
description: 了解如何将 DSL 关系图嵌入到显示在 Visual Studio 窗口的 Windows 控件中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: f7c8abdb8b3eff82c7dc36ec9be8bb7e9c1be7d6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671861"
---
# <a name="embed-a-diagram-in-a-windows-form"></a>在 Windows 窗体中嵌入图表

可以将 DSL 关系图嵌入到显示在 Visual Studio 窗口的 Windows 控件中。

## <a name="embed-a-dsl-diagram-in-a-windows-control"></a>在 Windows 控件中嵌入 DSL 关系图

1. 将新的用户控件文件添加到 DslPackage 项目。

2. 向用户控件添加面板控件。 此面板将包含 DSL 关系图。

     添加所需的其他控件。

     设置控件的 Anchor 属性。

3. 在“解决方案资源管理器”中右击用户控件文件，然后单击“查看代码”。 将此构造函数和变量添加到代码中：

    ```csharp
    internal UserControl1(MyDSLDocView docView, Control content)
      : this()
    {
      panel1.Controls.Add(content);
      this.docView = docView;
    }
    private MyDSLDocView docView;
    ```

4. 向 DslPackage 项目添加一个新文件，其中包含以下内容：

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

5. 若要测试 DSL，请按 F5 并打开示例模型文件。 关系图显示在控件内。 工具箱和其他功能正常工作。

## <a name="update-the-form-using-store-events"></a>使用存储事件更新窗体

1. 在窗体设计器中，添加名为 `listBox1` 的 ListBox。 这将显示模型中元素的列表。 它使用存储事件与模型同步。 有关详细信息，请参阅[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

2. 在自定义代码文件中，重写 DocView 类的其他方法：

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

4. 若要测试 DSL，请按 F5，并在 Visual Studio 的实验实例中，打开示例模型文件。

     请注意，列表框显示模型中的元素列表，并且在添加或删除后以及撤消和重做后，该列表都是正确的。

## <a name="see-also"></a>另请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)
