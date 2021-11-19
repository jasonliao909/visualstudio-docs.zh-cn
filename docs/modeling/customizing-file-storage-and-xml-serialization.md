---
title: 自定义文件存储和 XML 序列化
description: 了解在 Visual Studio 中保存域特定语言 (DSL) 的实例或模型时创建或更新的 XML 文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.dsldesigner.xmlbehavior
helpviewer_keywords:
- Domain-Specific Language, serialization
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: cf3f80c51866f278f4cf9a72876963d60ab17e4f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602319"
---
# <a name="customize-file-storage-and-xml-serialization"></a>自定义文件存储和 XML 序列化

当用户在 Visual Studio 中保存域特定语言 (DSL) 的实例或模型时，将创建一个 XML 文件或对其进行更新。 可以重新加载文件以在 Store 中重新创建模型。

可以通过在 DSL 资源管理器中调整“Xml 序列化行为”下的设置来自定义序列化方案。 对于每个域类、属性和关系，“Xml 序列化行为”下都有对应节点。 关系位于其源类下。 还有对应于形状、连接器和关系图类的节点。

还可以编写程序代码以实现更高级的自定义。

> [!NOTE]
> 如果要以特定格式保存模型，但不需要从该窗体重新加载它，请考虑使用文本模板从模型生成输出，而不是使用自定义序列化方案。 有关详细信息，请参阅[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)。

## <a name="model-and-diagram-files"></a>模型和关系图文件

每个模型通常保存在两个文件中：

- 模型文件具有一个名称，例如 Model1.mydsl。 它存储模型元素和关系及其属性。 文件扩展名（如 .mydsl）由 DSL 定义中“编辑器”节点的“FileExtension”属性确定。

- 关系图文件具有一个名称，例如 Model1.mydsl.diagram。 它存储形状、连接器及其位置、颜色、线条粗细以及关系图外观的其他详细信息。 如果用户删除某个 .diagram 文件，模型中的基本信息并不会丢失。 只有关系图的布局会丢失。 打开模型文件时，将创建一组默认的形状和连接器。

### <a name="to-change-the-file-extension-of-a-dsl"></a>更改 DSL 的文件扩展名

1. 打开 DSL 定义。 在 DSL 资源管理器中，单击“编辑器”节点。

2. 在“属性”窗口中，编辑“FileExtension”属性。 不要包含文件扩展名开头的“.”。

3. 在“解决方案资源管理器”中，更改 DslPackage\ProjectItemTemplates 中两个项模板文件的名称。 这些文件的名称遵循以下格式：

     `myDsl.diagram`

     `myDsl.myDsl`

## <a name="the-default-serialization-scheme"></a>默认序列化方案

为了创建本主题示例，使用了以下 DSL 定义。

![DSL 定义关系图 &#45; 家谱模型](../modeling/media/familyt_person.png)

此 DSL 用于创建在屏幕上具有以下外观的模型。

![家谱关系图、工具箱和资源管理器](../modeling/media/familyt_instance.png)

此模型已保存，然后在 XML 文本编辑器中重新打开：

```xml
<?xml version="1.0" encoding="utf-8"?>
<familyTreeModel xmlns:dm0="http://schemas.microsoft.com/VisualStudio/2008/DslTools/Core" dslVersion="1.0.0.0" Id="f817b728-e920-458e-bb99-98edc469d78f" xmlns="http://schemas.microsoft.com/dsltools/FamilyTree">
  <people>
    <person name="Henry VIII" birthYear="1491" deathYear="1547" age="519">
      <children>
        <personMoniker name="/f817b728-e920-458e-bb99-98edc469d78f/Elizabeth I" />
        <personMoniker name="/f817b728-e920-458e-bb99-98edc469d78f/Mary" />
      </children>
    </person>
    <person name="Elizabeth I" birthYear="1533" deathYear="1603" age="477" />
    <person name="Mary" birthYear="1515" deathYear="1558" age="495" />
  </people>
</familyTreeModel>
```

注意关于序列化模型的以下几点：

- 每个 XML 节点的名称都与域类名相同，但初始字母为小写。 例如，`familyTreeModel` 和 `person`。

- Name 和 BirthYear 等域属性在 XML 节点中序列化为特性。 同样，属性名称的初始字符将转换为小写。

- 每个关系都序列化为嵌套在关系的源端内的 XML 节点。 节点与源角色属性同名，但初始字符为小写。

     例如，在 DSL 定义中，名为“People”的角色来源于 FamilyTree 类。  在 XML 中，这由嵌套在 `familyTreeModel` 节点内名为 `people` 的节点表示。

- 每个嵌入关系的目标端序列化为嵌套在关系下的节点。 例如，`people` 节点包含多个 `person` 节点。

- 每个引用关系的目标端序列化为名字对象，用于编码对目标元素的引用。

     例如，在 `person` 节点下，可以有 `children` 关系。 此节点包含名字对象，例如：

    ```xml
    <personMoniker name="/f817b728-e920-458e-bb99-98edc469d78f/Elizabeth I" />
    ```

## <a name="understand-monikers"></a>了解名字对象

名字对象用于表示模型和关系图文件的不同部分之间的交叉引用。 它们还在 `.diagram` 文件中用于引用模型文件的节点。 有两种形式的名字对象：

- Id 名字对象引用目标元素的 GUID。 例如：

    ```xml
    <personShapeMoniker Id="f79734c0-3da1-4d72-9514-848fa9e75157" />
    ```

- 限定键名字对象通过名为“名字对象键”的指定域属性的值来标识目标元素。 目标元素的名字对象在嵌入关系树中以其父元素的名字对象作为前缀。

     以下示例取自 DSL，其中存在一个名为“Album”的域类，该类与名为“Song”的域类具有嵌入关系：

    ```xml
    <albumMoniker title="/My Favorites/Jazz after Teatime" />
    <songMoniker title="/My Favorites/Jazz after Teatime/Hot tea" />
    ```

     如果目标类具有域属性，且在“Xml 序列化行为”中该属性的“Is Moniker Key”选项设置为 `true`，则将使用限定键名字对象。 在示例中，这个选项是为域类“Album”和“Song”中名为“Title”的域属性设置的。

限定键名字对象比 ID 名字对象更易于读取。 如果希望用户读取模型文件的 XML，请考虑使用限定键名字对象。 但是，用户可以将多个元素设置为具有相同的名字对象键。 重复的键可能会导致文件无法正确地重新加载。 因此，如果定义使用限定键名字对象引用的域类，应考虑阻止用户保存具有重复名字对象的文件的方法。

### <a name="to-set-a-domain-class-to-be-referenced-by-id-monikers"></a>设置要由 ID 名字对象引用的域类

1. 请确保类及其基类中每个域属性的“Is Moniker Key”设置为 `false`。

    1. 在 DSL 资源管理器中，展开“Xml 序列化行为\类数据\\\<the domain class>\元素数据”。

    2. 验证每个域属性的“Is Moniker Key”是否设置为 `false`。

    3. 如果域类具有基类，则在该类中重复这一过程。

2. 设置域类的序列化 Id = `true`。

     可以在“Xml 序列化行为”下找到此属性。

### <a name="to-set-a-domain-class-to-be-referenced-by-qualified-key-monikers"></a>设置要由限定键名字对象引用的域类

- 为现有域类的域属性设置“Is Moniker Key”。 属性的类型必须为 `string`。

    1. 在 DSL 资源管理器中，展开“Xml 序列化行为\类数据\\\<the domain class>\元素数据”，然后选择域属性。

    2. 在“属性”窗口中，将“Is Moniker Key”设置为 `true`。

- \- 或 -

     使用“命名域类”工具创建新域类。

     此工具创建一个新类，该类具有名为“Name”的域属性。 此域属性的“Is Element Name”和“Is Moniker Key”属性将初始化为 `true`。

- \- 或 -

     创建从域类到具有名字对象键属性的另一个类的继承关系。

### <a name="avoid-duplicate-monikers"></a>避免重复的名字对象

如果使用限定键名字对象，则用户模型中的两个元素在键属性中可能具有相同的值。 例如，如果 DSL 具有包含属性 Name 的 Person 类，则用户可以将两个元素的 Name 设置为相同。 尽管模型可以保存到文件中，但它无法正确重新加载。

有几种方法可帮助避免这种情况：

- 为键域属性设置 Is Element Name = `true`。 在 DSL 定义关系图中选择域属性，然后在“属性”窗口中设置值。

     当用户创建类的新实例时，此值会导致自动为域属性分配其他值。 默认行为是在类名末尾添加一个数字。 这不会阻止用户将名称更改为重复的名称，但如果用户在保存模型之前没有设置值，这样做会有所帮助。

- 为 DSL 启用验证。 在 DSL 资源管理器中，选择“编辑器\验证”，并将“Uses...”属性设置为 `true`。

     有一个自动生成的验证方法，用于检查多义性。 该方法位于 `Load` 验证类别中。 这确保将警告用户可能无法重新打开文件。

     有关详细信息，请参阅[域特定语言中的验证](../modeling/validation-in-a-domain-specific-language.md)。

### <a name="moniker-paths-and-qualifiers"></a>名字对象路径和限定符

限定键名字对象以名字对象键结尾，在嵌入树中以其父级的名字对象作为前缀。 例如，如果一张专辑的名字对象为：

```xml
<albumMoniker title="/My Favorites/Jazz after Teatime" />
```

那么，该专辑中的一首歌曲可以是：

```xml
<songMoniker title="/My Favorites/Jazz after Teatime/Hot tea" />
```

但是，如果按 ID 引用专辑，则名字对象将如下所示：

```xml
<albumMoniker Id="77472c3a-9bf9-4085-976a-d97a4745237c" />
<songMoniker title="/77472c3a-9bf9-4085-976a-d97a4745237c/Hot tea" />
```

请注意，由于 GUID 是唯一的，因此它永远不会以其父级的名字对象作为前缀。

如果你知道某个特定域属性将始终在模型内具有唯一值，则可以将该属性的“Is Moniker Qualifier”设置为 `true`。 这会使它用作限定符，而不使用父级的名字对象。 例如，如果你为 Album 类的 Title 域属性同时设置了“Is Moniker Qualifier”和“Is Moniker Key”，则不会在 Album 及其嵌入子级的名字对象中使用该模型的名称或标识符：

```xml
<albumMoniker name="Jazz after Teatime" />
<songMoniker title="/Jazz after Teatime/Hot tea" />
```

## <a name="customize-the-structure-of-the-xml"></a>自定义 XML 的结构

若要进行以下自定义，请在 DSL 资源管理器中展开“Xml 序列化行为”节点。 在域类下，展开“元素数据”节点以查看源自此类的属性和关系的列表。 选择关系，并在“属性”窗口中调整其选项。

- 将“Omit Element”设置为 true 可省略源角色节点，只留下目标元素列表。 如果源类和目标类之间存在多个关系，则不应设置此选项。

    ```xml
    <familyTreeModel ...>
      <!-- The following node is omitted by using Omit Element: -->
      <!-- <people> -->
        <person name="Henry VIII" .../>
        <person name="Elizabeth I" .../>
      <!-- </people> -->
    </familyTreeModel>
    ```

- 设置“Use Full Form”，将目标节点嵌入表示关系实例的节点中。 将域属性添加到域关系时，会自动设置此选项。

    ```xml
    <familyTreeModel ...>
      <people>
        <!-- The following node is inserted by using Use Full Form: -->
        <familyTreeModelHasPeople myRelationshipProperty="x1">
          <person name="Henry VIII" .../>
        </familyTreeModelHasPeople>
        <familyTreeModelHasPeople myRelationshipProperty="x2">
          <person name="Elizabeth I" .../>
        </familyTreeModelHasPeople>
      </people>
    </familyTreeModel>
    ```

- 设置 Representation = Element，以将域属性另存为元素而不是特性值。

    ```xml
    <person name="Elizabeth I" birthYear="1533">
      <deathYear>1603</deathYear>
    </person>
    ```

- 若要更改特性和关系的序列化顺序，请右键单击“元素数据”下的某个项，然后使用“上移”或“下移”菜单命令。

## <a name="major-customization-using-program-code"></a>使用程序代码的主要自定义项

可以替换部分或所有序列化算法。

建议你研究一下 Dsl\Generated Code\Serializer.cs 和 SerializationHelper.cs 中的代码。

### <a name="to-customize-the-serialization-of-a-particular-class"></a>自定义特定类的序列化

1. 在“Xml 序列化行为”下该类的节点中设置“Is Custom”。

2. 转换所有模板，生成解决方案，并调查生成的编译错误。 每个错误附近的注释说明了必须提供的代码。

### <a name="to-provide-your-own-serialization-for-the-whole-model"></a>为整个模型提供你自己的序列化

1. 替代 Dsl\GeneratedCode\SerializationHelper.cs 中的方法

## <a name="options-in-xml-serialization-behavior"></a>Xml 序列化行为中的选项

在 DSL 资源管理器中，“Xml 序列化行为”节点包含每个域类、关系、形状、连接器和关系图类的子节点。 每个节点下是源自该元素的属性和关系的列表。 关系在其自己的右侧和源类下显示。

下表总结了可以在 DSL 定义的这一部分中设置的选项。 在每种情况下，在 DSL 资源管理器中选择一个元素，并在“属性”窗口中设置选项。

### <a name="xml-class-data"></a>Xml 类数据

这些元素位于 DSL 资源管理器中的“Xml 序列化行为\类数据”下。

|属性|说明|
|-|-|
|Has Custom Element Schema|如果为 True，则指示域类具有自定义元素架构|
|Is Custom|如果要为此域类编写自己的序列化和反序列化代码，请将此值设置为 True。<br /><br /> 生成解决方案并调查错误以发现详细说明。|
|域类|此类数据节点应用到的域类。 只读。|
|元素名称|此类的元素的 Xml 节点名称。 默认值是域类名称的小写版本。|
|Moniker Attribute Name|名字对象元素中用于包含引用的特性的名称。 如果为空，则使用键属性的名称或 ID。<br /><br /> 在此示例中为 "name":  `<personMoniker name="/Mike Nash"/>`|
|Moniker Element Name|XML 元素的名称，用于引用该类的元素的名字对象。<br /><br /> 默认值是带有“Moniker”后缀的类名的小写版本。 例如，`personMoniker`。|
|Moniker Type Name|为此类的元素的名字对象所生成 xsd 类型的名称。 XSD 位于 Dsl\Generated Code\\\*Schema.xsd 中|
|Serialize Id|如果为 True，则元素 GUID 包含在文件中。 如果没有标记为“Is Moniker Key”的属性，并且 DSL 定义对此类的引用关系，则此属性必须为 true。|
|类型名称|由指定域类在 xsd 中生成的 XML 类型的名称。|
|备注|与此元素相关联的非正式注释|

### <a name="xml-property-data"></a>Xml Property Data

Xml 属性节点位于类节点下。

|属性|说明|
|-|-|
|Domain Property|XML 序列化配置数据应用到的属性。 只读。|
|Is Moniker Key|如果为 True，则属性用作创建引用此域类的实例的名字对象的键。|
|Is Moniker Qualifier|如果为 True，则属性用于在名字对象中创建限定符。 如果为 false，并且此域类的 SerializeId 不为 true，则名字对象由嵌入树中父元素的名字对象限定。|
|表示形式|如果是“特性”，则属性序列化为 XML 特性；如果是“元素”，则序列化为元素；如果是“忽略”，则不序列化。|
|Xml Name|用于代表属性的 XML 特性或元素的名称。 默认情况下，这是域属性名称的小写版本。|
|备注|与此元素相关联的非正式注释|

### <a name="xml-role-data"></a>Xml Role data

角色数据节点位于源类节点下。

|属性|说明|
|-|-|
|Has Custom Moniker|如果要提供自己的代码来生成和解析遍历此关系的名字对象，请设置为 true。<br /><br /> 有关详细说明，请生成解决方案，然后双击错误消息。|
|域关系|指定这些选项应用于的关系。 只读。|
|Omit Element|如果为 True，则从架构中省略对应于源角色的 XML 节点。<br /><br /> 如果源类和目标类之间存在多个关系，此角色节点将区分属于这两种关系的链接。 因此，在这种情况下不建议设置此选项。|
|Role Element Name|指定从源角色派生的 XML 元素的名称。 默认值为角色属性名称。|
|Use Full Form|如果为 true，则每个目标元素或名字对象都包含在表示关系的 XML 节点中。 如果关系具有其自己的域属性，则应将此属性设置为 true。|

## <a name="see-also"></a>另请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)
