---
title: 将跟踪属性添加到 DSL 定义
description: 了解跟踪域属性，以及如何将跟踪属性添加到域模型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tracking properties [Domain-Specific Language Tools], walkthrough
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools]
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 798b88b23aa68ec6e12e81ef5061160a8a7636df
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666188"
---
# <a name="add-a-tracking-property-to-a-domain-specific-language-definition"></a>向域特定语言定义中添加跟踪属性

本演练演示如何将跟踪属性添加到域模型。

跟踪域属性是一种可由用户更新的属性，但它有一个通过使用其他域属性或元素的值来计算的默认值。

比如，在特定于域的语言工具（DSL 工具）中，域类的“显示名称”属性具有一个通过使用域类名称计算的默认值，但用户可以在设计时更改该值或将其重置为计算值。

在本演练中，创建一个域特定语言 (DSL)，该语言具有一个命名空间跟踪属性，该属性具有一个基于模型的默认命名空间属性的默认值。 有关跟踪属性的详细信息，请参阅[定义跟踪属性](/previous-versions/cc825929(v=vs.100))。

- DSL 工具支持跟踪属性描述符。 但是，DSL 设计器不能用于向语言添加跟踪属性。 因此，必须添加自定义代码来定义和实现跟踪属性。

  跟踪属性有两种状态：“正在跟踪”和“用户已更新”。 跟踪属性具有以下功能：

- 处于“正在跟踪”状态时，将计算跟踪属性的值，并且该值会随着模型中其他属性的更改而更新。

- 处于“用户已更新”状态时，跟踪属性的值将保留用户上次设置属性的值。

- 在“属性”窗口中，只有在属性处于“用户已更新”状态时，才启用跟踪属性的 Reset 命令 。 Reset 命令将跟踪属性状态设置为“正在跟踪”。

- 在“属性”窗口中，当跟踪属性处于“正在跟踪”状态时，其值以常规字体显示。

- 在“属性”窗口中，当跟踪属性处于“用户已更新”状态时，其值以加粗字体显示。

## <a name="prerequisites"></a>先决条件

在开始本演练之前，必须先安装以下组件：

| 组件 | 链接 |
|-|-|
| Visual Studio | [http://go.microsoft.com/fwlink/?LinkID=185579](https://visualstudio.microsoft.com/) |
| [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] | [http://go.microsoft.com/fwlink/?LinkID=185580](/azure/devops/integrate/index?view=azure-devops&viewFallbackFrom=vsts&preserve-view=true) |
| [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] | [http://go.microsoft.com/fwlink/?LinkID=185581](https://code.msdn.microsoft.com/site/search?query=%22Modeling%20SDK%22&f%5B0%5D.Value=%22Modeling%20SDK%22&f%5B0%5D.Type=SearchText&ac=5) |

## <a name="create-the-project"></a>创建项目

1. 创建特定于域的语言设计器项目。 将其命名为 `TrackingPropertyDSL`。

2. 在“特定于域的语言设计器向导”中，设置以下选项：

    1. 选择“MinimalLanguage”模板。

    2. 使用域特定语言的默认名称 `TrackingPropertyDSL`。

    3. 将模型文件的扩展名设置为 `trackingPropertyDsl`。

    4. 使用模型文件的默认模板图标。

    5. 将产品名称设置为 `Product Name`。

    6. 将公司名称设置为 `Company Name`。

    7. 使用解决方案中项目的根命名空间的默认值 `CompanyName.ProductName.TrackingPropertyDSL`。

    8. 允许向导为程序集创建强名称密钥文件。

    9. 查看解决方案的详细信息，然后单击“完成”来创建 DSL 定义项目。

## <a name="customize-the-default-dsl-definition"></a>自定义默认 DSL 定义
 在本部分，自定义 DSL 定义以包含以下项：

- 每个模型元素的命名空间跟踪属性。

- 每个模型元素的布尔 IsNamespaceTracking 属性。 此属性将指示跟踪属性是处于“正在跟踪”状态还是“用户已更新”状态。

- 模型的默认命名空间属性。 此属性将用于计算命名空间跟踪属性的默认值。

- 模型的 CustomElements 计算属性。 此属性将指示具有自定义命名空间的元素的比例。

### <a name="to-add-the-domain-properties"></a>添加域属性

1. 在 DSL 设计器中，右键单击“ExampleModel”域类，指向“添加”，然后单击“DomainProperty”  。

    1. 将新属性命名为 `DefaultNamespace`。

    2. 在新属性的“属性”窗口中，将“默认值”设置为 `DefaultNamespace`，然后将“类型”设置为“字符串”   。

2. 将名为 `CustomElements` 的域属性添加到“ExampleModel”域类。

     在新属性的“属性”窗口中，将“种类”设置为“已计算”  。

3. 将名为 `Namespace` 的域属性添加到“ExampleElement”域类。

     在新属性的“属性”窗口中，将“可浏览”设置为“False”，然后将“种类”设置为“CustomStorage”    。

4. 将名为 `IsNamespaceTracking` 的域属性添加到“ExampleElement”域类。

     在新属性的“属性”窗口中，将“可浏览”设置为“False”，将“默认值”设置为 `true`，然后将“类型”设置为“布尔”     。

### <a name="to-update-the-diagram-elements-and-dsl-details"></a>更新关系图元素和 DSL 详细信息

1. 在 DSL 设计器中，右键单击“ExampleShape”几何形状，指向“添加”，然后单击“文本修饰器”  。

    1. 将新的文本修饰器命名为 `NamespaceDecorator`。

    2. 在文本修饰器的“属性”窗口中，将“位置”设置为“InnerBottomLeft”  。

2. 在 DSL 设计器中，选择将“ExampleElement”类连接到“ExampleShape”形状的线 。

    1. 在“DSL 详细信息”窗口中，选择“修饰器映射”选项卡 。

    2. 在“修饰器”列表中，选择“NamespaceDecorator”，选中其复选框，然后在“显示属性”列表中，选择“命名空间”   。

3. 在 DSL 资源管理器中，展开“域类”文件夹，右键单击“ExampleElement”节点，然后单击“新增域类型描述符”   。

    1. 展开“ExampleElement”节点，然后选择“自定义类型描述符(域类型描述符)”节点 。

    2. 在域类型描述符的“属性”窗口中，将“自定义编码”设置为“True”  。

4. 在 DSL 资源管理器中，选择“Xml 序列化行为”节点 。

    1. 在“属性”窗口中，将“自定义发布加载”设置为“True”  。

## <a name="transform-templates"></a>转换模板

为 DSL 定义域类和属性后，可以验证是否可正确转换 DSL 定义以重新生成项目的代码。

1. 在“解决方案资源管理器”工具栏上，单击“转换所有模板” 。

2. 系统重新生成解决方案的代码，并保存 DslDefinition.dsl。 有关定义文件的 XML 格式的信息，请参阅 [DslDefinition.dsl 文件](../modeling/the-dsldefinition-dsl-file.md)。

## <a name="create-files-for-custom-code"></a>为自定义代码创建文件

转换所有模板时，系统会生成源代码，用于定义 Dsl 和 DslPackage 项目中的域特定语言。 为了避免干扰生成的文本，可以在与生成的代码文件不同的文件中编写自定义代码。

必须提供用于维护跟踪属性的值和状态的代码。 为了帮助你区分自定义代码与生成的代码，并避免文件命名冲突，请将自定义代码文件放在单独的子文件夹。

1. 在“解决方案资源管理器”中，右键单击“DSL”项目，指向“添加”，然后单击“新建文件夹”   。 将新文件夹命名为 `CustomCode`。

2. 右键单击新的“CustomCode”文件夹，指向“添加”，然后单击“新建项”  。

3. 选择“代码文件”模板，将“名称”设置为 `NamespaceTrackingProperty.cs`，然后单击“确认”  。

     NamespaceTrackingProperty.cs 文件已创建并打开以便进行编辑。

4. 在文件夹中，创建以下代码文件：`ExampleModel.cs,``HelperClasses.cs`、`Serialization.cs` 和 `TypeDescriptor.cs`。

5. 在 DslPackage 项目中，还要创建一个 `CustomCode` 文件夹，并向其中添加一个 `Package.cs` 代码文件。

## <a name="add-helper-classes-to-support-tracking-properties"></a>添加帮助程序类以支持跟踪属性

将 `TrackingHelper` 和 `CriticalException` 类添加到 HelperClasses.cs 文件中，如下所示。 你稍后将在本演练中引用这些类。

1. 将以下代码添加到 HelperClasses.cs 文件。

    ```csharp
    using System;
    using System.Collections;
    using System.Diagnostics;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        internal static class TrackingHelper
        {
            /// <summary>Notify each model element in a collection that a tracked
            /// property has changed.</summary>
            /// <param name="store">The store for the model.</param>
            /// <param name="collection">The collection of model elements that
            /// contain the tracking property.</param>
            /// <param name="propertyId">The ID of the tracking property.</param>
            /// <param name="trackingPropertyId">The ID of the property that
            /// indicates whether the tracking property is tracking.</param>
            internal static void UpdateTrackingCollectionProperty(
                Store store,
                IEnumerable collection,
                Guid propertyId,
                Guid trackingPropertyId)
            {
                DomainPropertyInfo propInfo =
                    store.DomainDataDirectory.GetDomainProperty(propertyId);

                DomainPropertyInfo trackingPropInfo =
                    store.DomainDataDirectory.GetDomainProperty(trackingPropertyId);

                Debug.Assert(propInfo != null);
                Debug.Assert(trackingPropInfo != null);
                Debug.Assert(trackingPropInfo.PropertyType.Equals(typeof(bool)),
                    "Tracking property not specified as a boolean");

                foreach (ModelElement element in collection)
                {
                    // If the tracking property is currently tracking, then notify
                    // it that the tracked property has changed.
                    bool isTracking = (bool)trackingPropInfo.GetValue(element);
                    if (isTracking)
                    {
                        propInfo.NotifyValueChange(element);
                    }
                }
            }
        }

        /// <summary>Helper class to flag critical exceptions from ones that are
        /// safe to ignore.</summary>
        internal static class CriticalException
        {
            /// <summary>Gets whether an exception is critical and can not be
            /// ignored.</summary>
            /// <param name="ex">The exception to check.</param>
            /// <returns>True if the exception is critical.</returns>
            internal static bool IsCriticalException(Exception ex)
            {
                if (ex is NullReferenceException
                    || ex is StackOverflowException
                    || ex is OutOfMemoryException
                    || ex is System.Threading.ThreadAbortException)
                    return true;

                if (ex.InnerException != null)
                    return IsCriticalException(ex.InnerException);

                return false;
            }
        }
    }
    ```

## <a name="add-custom-code-for-the-custom-type-descriptor"></a>为自定义类型描述符添加自定义代码

为 `ExampleModel` 域类的类型描述符实现 `GetCustomProperties` 方法。

> [!NOTE]
> DSL 工具为 `ExampleModel` 的自定义类型描述符生成的代码调用 `GetCustomProperties`；但是，DSL 工具不会生成实现方法的代码。

定义此方法会为命名空间跟踪属性创建跟踪属性描述符。 此外，为跟踪属性提供特性可使“属性”窗口正确显示该属性。

### <a name="to-modify-the-type-descriptor-for-the-examplemodel-domain-class"></a>修改 ExampleModel 域类的类型描述符

1. 将以下代码添加到 TypeDescriptor.cs 文件。

    ```csharp
    using System;
    using System.ComponentModel;
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Design;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // To the custom type descriptor for the ExampleElement domain class, add
        // the GetCustomProperties method.
        public partial class ExampleElementTypeDescriptor
        {
            /// <summary>Returns the property descriptors for the described
            /// ExampleElement domain class.</summary>
            /// <remarks>This method adds the tracking property descriptor.
            /// </remarks>
            private PropertyDescriptorCollection GetCustomProperties(
                Attribute[] attributes)
            {
                // Get the default property descriptors from the base class
                PropertyDescriptorCollection propertyDescriptors =
                    base.GetProperties(attributes);

                // Get a reference to the model element that is being described.
                ExampleElement source = this.ModelElement as ExampleElement;

                //Add the descriptor for the tracking property.
                if (source != null)
                {
                    DomainPropertyInfo domainProperty =
                        source.Store.DomainDataDirectory.GetDomainProperty(
                            ExampleElement.NamespaceDomainPropertyId);

                    DomainPropertyInfo trackingProperty =
                        source.Store.DomainDataDirectory.GetDomainProperty(
                            ExampleElement.IsNamespaceTrackingDomainPropertyId);

                    // Define attributes for the tracking property so that the
                    // Properties window displays the property correctly.
                    Attribute[] attr = new Attribute[] {
                        new DisplayNameAttribute("Element Namespace"),
                        new DescriptionAttribute("The namespace of the element."),
                        new CategoryAttribute("Tracking Properties"),
                    };

                    propertyDescriptors.Add(new TrackingPropertyDescriptor(
                        source, domainProperty, trackingProperty, attr));
                }

                // Return the property descriptors for this element
                return propertyDescriptors;
            }
        }
    }
    ```

## <a name="adding-custom-code-for-the-package"></a>为包添加自定义代码

生成的代码为 ExampleElement 域类定义一个类型说明提供程序；但是，必须添加代码以指示 DSL 使用此类型说明提供程序。

1. 将以下代码添加到 Package.cs 文件。

    ```csharp
    using System.ComponentModel;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // Override the default Initialize method.
        internal sealed partial class TrackingPropertyDSLPackage
        {
            protected override void Initialize()
            {
                // Add the custom type descriptor for the ExampleElement type.
                TypeDescriptor.AddProvider(
                    new ExampleElementTypeDescriptionProvider(),
                    typeof(ExampleElement));

                base.Initialize();
            }
        }
    }
    ```

## <a name="add-custom-code-for-the-model"></a>为模型添加自定义代码

为 `ExampleModel` 域类实现 `GetCustomElementsValue` 方法。

> [!NOTE]
> DSL 工具为 `ExampleModel` 生成的代码调用 `GetCustomElementsValue`；但是，DSL 工具不会生成实现方法的代码。

定义 `GetCustomElementsValue` 方法可为 `ExampleModel` 的 CustomElements 计算属性提供逻辑。 此方法对 `ExampleElement` 域类进行计数，此域类具有一个命名空间跟踪属性，该属性具有用户更新的值，并返回一个字符串，该字符串将此计数表示为模型中元素总数的比例。

此外，将 `OnDefaultNamespaceChanged` 方法添加到 `ExampleModel`，并替代 `ExampleModel` 的 `DefaultNamespacePropertyHandler` 嵌套类的 `OnValueChanged` 方法，以此来调用 `OnDefaultNamespaceChanged`。

由于 DefaultNamespace 属性用于计算命名空间跟踪属性，因此 `ExampleModel` 必须通知所有 `ExampleElement` 域类 DefaultNamespace 的值已更改。

### <a name="to-modify-the-property-handler-for-the-tracked-property"></a>修改跟踪的属性的属性处理程序

1. 将以下代码添加到 ExampleModel.cs 文件。

    ```csharp
    using System.Linq;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        public partial class ExampleModel
        {
            public string GetCustomElementsValue()
            {
                if (this.Elements.Count == 0) return "0/0";

                int number = this.Elements.Count(e => !e.IsNamespaceTracking);
                return string.Format("{0}/{1}", number, this.Elements.Count);
            }

            #region Value changed handler for the tracked property

            // When a tracked property changes, it needs to notify all of the properties
            // that track it.

            /// <summary>Called by the DefaultNamespace property value handler when the
            /// DefaultNamespace property changes.</summary>
            /// <param name="oldValue">The previous value of the property.</param>
            /// <param name="newValue">The new value of the property.</param>
            protected virtual void OnDefaultNamespaceChanged(
                string oldValue, string newValue)
            {
                // Use the helper class to notify all of the elements in the model
                // that the default namespace has changed.
                TrackingHelper.UpdateTrackingCollectionProperty(
                    this.Store,
                    this.Elements,
                    ExampleElement.NamespaceDomainPropertyId,
                    ExampleElement.IsNamespaceTrackingDomainPropertyId);
            }

            // Update the change handler for the DefaultNamespace property.
            internal sealed partial class DefaultNamespacePropertyHandler
            {
                /// <summary>Called when the DefaultNamespace property changes.</summary>
                /// <param name="element">The model element that has the property that
                /// changed.</param>
                /// <param name="oldValue">The previous value of the property.</param>
                /// <param name="newValue">The new value of the property.</param>
                protected override void OnValueChanged(
                    ExampleModel element, string oldValue, string newValue)
                {
                    base.OnValueChanged(element, oldValue, newValue);

                    if (!element.Store.InUndoRedoOrRollback)
                    {
                        element.OnDefaultNamespaceChanged(oldValue, newValue);
                    }
                }
            }

            #endregion
        }
    }
    ```

## <a name="add-custom-code-for-the-tracking-property"></a>为跟踪属性添加自定义代码

将 `CalculateNamespace` 方法添加到 `ExampleElement` 域类。

定义此方法可为 `ExampleModel` 的 CustomElements 计算属性提供逻辑。 此方法对 `ExampleElement` 域类进行计数，此域类具有一个命名空间跟踪属性，该属性处于“用户已更新”状态，并返回一个字符串，该字符串将此计数表示为模型中元素总数的比例。

此外，为 `ExampleElement` 域类的命名空间自定义存储属性添加存储，并添加获取和设置该属性的方法。

> [!NOTE]
> DSL 工具为 `ExampleModel` 生成的代码调用 Get 和 Set 方法；但是，DSL 工具不会生成实现方法的代码。

### <a name="to-add-the-method-for-the-custom-type-descriptor"></a>为自定义类型描述符添加方法

1. 将以下代码添加到 NamespaceTrackingProperty.cs 文件。

    ```csharp
    using System;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // To the domain class that has the tracking property, add the caluclation
        // for when the property is tracking.
        public partial class ExampleElement
        {
            /// <summary>Calculates the actual value of the property when it is
            /// tracking.</summary>
            /// <returns>The value of the tracking property when it is
            /// tracking.</returns>
            /// <remarks>Making this method virtual allows child classes to modify
            /// the calculation. This method does not need to perform validation, as
            /// its caller handles validation prior to calling this method.
            /// <para>In this case, the tracking value depends on the default namespace
            /// property of the parent model.</para></remarks>
            protected virtual string CalculateNamespace()
            {
                return this.ExampleModel.DefaultNamespace;
            }

            #region Tracking property implementation

            // Implement the Namespace domain property of the ExampleElement domain class,
            // and update the IsNamespaceTracking domain property value handler.

            /// <summary>Storage for the Namespace property.</summary>
            private string namespaceStorage;

            /// <summary>Gets the value of the Namespace property.</summary>
            /// <returns>The value of the Namespace property.</returns>
            private string GetNamespaceValue()
            {
                // Only retrieve the tracked value if the store is not in the
                // middle of a serialization transaction.
                bool loading = this.Store.TransactionManager.InTransaction
                    && this.Store.TransactionManager.CurrentTransaction.IsSerializing;

                if (!loading && this.IsNamespaceTracking)
                {
                    try
                    {
                        return this.CalculateNamespace();
                    }
                    catch (NullReferenceException)
                    {
                        return default(string);
                    }
                    catch (Exception e)
                    {
                        if (CriticalException.IsCriticalException(e))
                        {
                            throw;
                        }
                        else
                        {
                            return default(string);
                        }
                    }
                }

                return namespaceStorage;
            }

            /// <summary>Sets the value of the Namespace property.</summary>
            /// <param name="value">The new value for the property.</param>
            private void SetNamespaceValue(string value)
            {
                namespaceStorage = value;

                // Only update the state of the tracking property if the store is
                // not in the middle of a serialization transaction.
                bool loading = this.Store.TransactionManager.InTransaction
                    && this.Store.TransactionManager.CurrentTransaction.IsSerializing;

                if (!this.Store.InUndoRedoOrRollback && !loading)
                {
                    this.IsNamespaceTracking = false;
                }
            }

            // Update the default behavior of the ExampleElement.IsNamespaceTracking
            // domain property value handler.
            internal sealed partial class IsNamespaceTrackingPropertyHandler
            {
                /// <summary>Called after the IsNamespaceTracking property changes.
                /// </summary>
                /// <param name="element">The model element that has the property
                /// that changed.</param>
                /// <param name="oldValue">The previous value of the property.
                /// </param>
                /// <param name="newValue">The new value of the property.</param>
                protected override void OnValueChanged(
                    ExampleElement element, Boolean oldValue, Boolean newValue)
                {
                    base.OnValueChanged(element, oldValue, newValue);
                    if (!element.Store.InUndoRedoOrRollback && newValue)
                    {
                        DomainPropertyInfo propInfo =
                            element.Store.DomainDataDirectory.GetDomainProperty(
                                ExampleElement.NamespaceDomainPropertyId);
                        propInfo.NotifyValueChange(element);
                    }
                }

                /// <summary>Performs the reset operation for the IsNamespaceTracking
                /// property for a model element.</summary>
                /// <param name="element">The model element that has the property
                /// to reset.</param>
                internal void ResetValue(ExampleElement element)
                {
                    object calculatedValue = null;

                    try
                    {
                        calculatedValue = element.CalculateNamespace();
                    }
                    catch (NullReferenceException)
                    {
                    }
                    catch (System.Exception e)
                    {
                        if (CriticalException.IsCriticalException(e))
                        {
                            throw;
                        }
                    }

                    if ((calculatedValue != null
                        && object.Equals(element.Namespace, calculatedValue)))
                    {
                        element.isNamespaceTrackingPropertyStorage = true;
                    }
                }

                /// <summary>Method to set IsNamespaceTracking to false so that this
                /// instance of this tracking property is not storage-based.
                /// </summary>
                /// <param name="element">The element on which to reset the property
                /// value.</param>
                internal void PreResetValue(ExampleElement element)
                {
                    // Force the IsNamespaceTracking property to false so that the value
                    // of the Namespace property is retrieved from storage.
                    element.isNamespaceTrackingPropertyStorage = false;
                }
            }

            #endregion
        }
    }
    ```

## <a name="add-custom-code-to-support-serialization"></a>添加自定义代码以支持序列化

添加代码以支持 XML 序列化的自定义加载后行为。

> [!NOTE]
> DSL 工具生成的代码调用 `OnPostLoadModel` 和 `OnPostLoadModelAndDiagram` 方法；但是，DSL 工具不会生成实现这些方法的代码。

### <a name="to-add-code-to-support-the-custom-post-load-behavior"></a>添加代码以支持自定义加载后行为

1. 将以下代码添加到 Serialization.cs 文件。

    ```csharp
    using System;
    using System.Diagnostics;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        #region Helper classes for maintaining state while the store is serializing.

        public abstract partial class TrackingPropertyDSLSerializationHelperBase
        {
            /// <summary>Reset the tracking state properties to their natural values
            /// based on comparing storage with calculation.</summary>
            /// <param name="store">The store that contains this model.</param>
            internal static void ResetTrackingProperties(Store store)
            {
                // Two passes required - one to set all elements to storage-based
                // then another to set some back to being tracking.
                foreach (ModelElement element in store.ElementDirectory.AllElements)
                {
                    ExampleElement myElementInstance = element as ExampleElement;
                    if (myElementInstance != null)
                    {
                        myElementInstance.PreResetIsTrackingProperties();
                        continue;
                    }
                }
                foreach (ModelElement element in store.ElementDirectory.AllElements)
                {
                    ExampleElement myElementInstance = element as ExampleElement;
                    if (myElementInstance != null)
                    {
                        myElementInstance.ResetIsTrackingProperties();
                        continue;
                    }
                }
            }
        }

        // Add the pre-reset and reset methods for the model element.
        public partial class ExampleElement
        {
            /// <summary>Calls the pre-reset method on the associated property value
            /// handler for each tracking property of this model element.</summary>
            internal virtual void PreResetIsTrackingProperties()
            {
                ExampleElement.IsNamespaceTrackingPropertyHandler.Instance.PreResetValue(this);
            }

            /// <summary>Calls the reset method on the associated property value
            /// handler for each tracking property of this model element.</summary>
            internal virtual void ResetIsTrackingProperties()
            {
                ExampleElement.IsNamespaceTrackingPropertyHandler.Instance.ResetValue(this);
            }
        }

        #endregion

        #region Custom serialization code

        // To the serialization helper for the TrackingPropertyDSL class, add post
        // load handlers to bind the tracking property to the serialization process.
        // These handlers manage the tracking states and property values when the
        // model is serialized and deserialized.
        public partial class TrackingPropertyDSLSerializationHelperBase
        {
            /// <summary>Customize model loading.</summary>
            /// <param name="serializationResult">The serialization result from the
            /// load operation.</param>
            /// <param name="partition">The partition in which the new
            /// instance was created.</param>
            /// <param name="fileName">The name of the file from which the
            /// instance was deserialized.</param>
            /// <param name="modelRoot">The root of the file that was loaded.
            /// </param>
            private void OnPostLoadModel(
                SerializationResult serializationResult,
                Partition partition,
                string fileName,
                ExampleModel modelRoot)
            {
            }

            /// <summary>Customize model and diagram loading.</summary>
            /// <param name="serializationResult">Stores serialization result from
            /// the load operation.</param>
            /// <param name="modelPartition">Partition in which the new
            /// instance will be created.</param>
            /// <param name="modelFileName">Name of the file from which the
            /// instance will be deserialized.</param>
            /// <param name="diagramPartition">Partition in which the new
            /// diagram instance will be created.</param>
            /// <param name="diagramFileName">Name of the file from which the
            /// diagram instance will be deserialized.</param>
            /// <param name="modelRoot">The root of the file that was loaded.</param>
            /// <param name="diagram">The diagram matching the modelRoot.</param>
            private void OnPostLoadModelAndDiagram(
                SerializationResult serializationResult,
                Partition modelPartition,
                string modelFileName,
                Partition diagramPartition,
                string diagramFileName,
                ExampleModel modelRoot,
                TrackingPropertyDSLDiagram diagram)
            {
                Debug.Assert(modelPartition != null);
                Debug.Assert(modelPartition.Store != null);

                // Tracking properties need to be set up according to whether the
                // serialization matches the calculated values.
                TrackingPropertyDSLSerializationHelperBase.ResetTrackingProperties(
                    modelPartition.Store);
            }
        }

        #endregion
    }
    ```

## <a name="test-the-language"></a>测试语言

下一步是在 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 的新实例中生成并运行 DSL 设计器，以便可以验证跟踪属性是否正常工作。

1. 在“生成”菜单上，单击“重新生成解决方案” 。

2. 在“调试”菜单上，单击“启动调试”。

    [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 的实验性生成打开包含空测试文件的调试解决方案。

3. 在解决方案资源管理器中，双击 Test.trackingPropertyDsl 文件以在设计器中打开它，然后单击设计图面。

    请注意，在关系图的“属性”窗口中，“默认命名空间”属性为“DefaultNamespace”，“自定义元素”属性为“0/0”    。

4. 将“ExampleElement”元素从“工具箱”拖动到关系图图面 。

5. 在元素“属性”窗口中，选择“元素命名空间”属性，将值从“DefaultNamespace”更改为“OtherNamespace”   。

    请注意，“元素命名空间”的值现以粗体显示。

6. 在“属性”窗口中，右键单击“元素命名空间”，然后单击“重置”  。

    属性的值更改为“DefaultNamespace”，并且该值以常规字体显示。

    再次右键单击“元素命名空间”。 “重置”命令现已禁用，因为该属性当前处于“正在跟踪”状态。

7. 将“ExampleElement”元素从“工具箱”拖动到关系图图面，然后将其“元素命名空间”更改为“OtherNamespace”   。

8. 单击设计图面。

    在关系图的“属性”窗口中，“自定义元素”的值现为“1/2”  。

9. 将关系图的“默认命名空间”从“DefaultNamespace”更改为“NewNamespace”  。

     第一个元素的命名空间跟踪“默认命名空间”属性，而第二个元素的命名空间保留其用户更新的值“OtherNamespace”   。

10. 保存解决方案，然后关闭实验性生成。

## <a name="next-steps"></a>后续步骤

如果计划使用多个跟踪属性，或在多个 DSL 中实现跟踪属性，可以创建一个文本模板来生成支持每个跟踪属性的通用代码。 有关文本模板的详细信息，请参阅[代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)。

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.VisualStudio.Modeling.Design.TrackingPropertyDescriptor>
- <xref:Microsoft.VisualStudio.Modeling.Design.ElementTypeDescriptor>
- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)
- [如何：创建域特定语言解决方案](../modeling/how-to-create-a-domain-specific-language-solution.md)