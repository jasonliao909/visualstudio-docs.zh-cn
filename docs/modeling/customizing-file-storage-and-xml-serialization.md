---
title: 自定义文件存储和 XML 序列化
description: 了解在将域特定语言的实例或模型保存到 Visual Studio (DSL) 时创建或更新的 XML 文件。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122061306"
---
# <a name="customize-file-storage-and-xml-serialization"></a>自定义文件存储和 XML 序列化

当用户将域特定语言的实例或 *模型* 保存 (DSL) 在 Visual Studio 中时，将创建或更新 XML 文件。 可以重新加载该文件以在应用商店中重新创建该模型。

可以通过在 DSL 资源管理器中调整 **Xml 序列化行为** 下的设置，自定义序列化方案。 对于每个域类、属性和关系， **Xml 序列化行为** 下有一个节点。 关系位于其源类下。 还有对应于形状、连接符和关系图类的节点。

你还可以编写程序代码以进行更高级的自定义。

> [!NOTE]
> 如果要以特定格式保存模型，但不需要从该窗体中重新加载它，请考虑使用文本模板从模型生成输出，而不是使用自定义序列化方案。 有关详细信息，请参阅 [从 Domain-Specific 语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)。

## <a name="model-and-diagram-files"></a>模型和关系图文件

每个模型通常保存在两个文件中：

- 模型文件具有一个名称，例如 **Model1. mydsl**。 它存储模型元素和关系及其属性。 文件扩展名（如 **mydsl** ）由 DSL 定义中 **编辑器** 节点的 **FileExtension** 属性确定。

- 关系图文件具有一个名称，例如 **Model1. mydsl**。 它存储形状、连接符及其位置、颜色、线条粗细和关系图外观的其他详细信息。 如果用户删除某个 **关系图** 文件，则模型中的基本信息不会丢失。 仅会丢失关系图的布局。 打开模型文件时，将创建一组默认的形状和连接线。

### <a name="to-change-the-file-extension-of-a-dsl"></a>更改 DSL 的文件扩展名

1. 打开 DSL 定义。 在 DSL 资源管理器中，单击 "编辑器" 节点。

2. 在属性窗口中，编辑 **FileExtension** 属性。 不要包含文件扩展名的初始 "."。

3. 在解决方案资源管理器中，更改 **DslPackage\ProjectItemTemplates** 中两个项模板文件的名称。 这些文件的名称遵循以下格式：

     `myDsl.diagram`

     `myDsl.myDsl`

## <a name="the-default-serialization-scheme"></a>默认序列化方案

若要创建本主题的示例，请使用以下 DSL 定义。

![DSL 定义关系图 &#45; 系列树模型](../modeling/media/familyt_person.png)

此 DSL 用于创建在屏幕上具有以下外观的模型。

![家谱关系图、工具箱和资源管理器](../modeling/media/familyt_instance.png)

已保存此模型，然后在 XML 文本编辑器中将其重新打开：

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

请注意有关序列化模型的以下几点：

- 每个 XML 节点都具有与域类名称相同的名称，只不过初始字母为小写。 例如，`familyTreeModel` 和 `person`。

- 诸如 Name 和 BirthYear 之类的域属性将作为 XML 节点中的属性进行序列化。 同样，将属性名称的初始字符转换为小写。

- 每个关系都序列化为嵌套在关系的源端内的 XML 节点。 该节点与源角色属性同名，但使用的是小写的初始字符。

     例如，在 DSL 定义中，名为 " **人员** " 的角色来源于 **FamilyTree** 类。  在 XML 中，这由节点内名为 "嵌套" 的节点表示 `people` `familyTreeModel` 。

- 每个嵌入关系的目标端均序列化为在关系下嵌套的节点。 例如， `people` 节点包含多个 `person` 节点。

- 每个引用关系的目标端均序列化为 *标记*，这将对目标元素的引用进行编码。

     例如，在节点下 `person` ，可以有 `children` 关系。 此节点包含如下所示的名字对象：

    ```xml
    <personMoniker name="/f817b728-e920-458e-bb99-98edc469d78f/Elizabeth I" />
    ```

## <a name="understand-monikers"></a>了解名字对象

名字对象用于表示在模型和关系图文件的不同部分之间进行交叉引用。 它们还在文件中用于 `.diagram` 引用模型文件中的节点。 名字对象有两种形式：

- *Id 名字对象* 引用目标元素的 GUID。 例如：

    ```xml
    <personShapeMoniker Id="f79734c0-3da1-4d72-9514-848fa9e75157" />
    ```

- *限定键名字对象* 通过称为 "名字对象" 键的指定域属性的值识别目标元素。 目标元素的名字对象在嵌入关系树中以其父元素的名字对象为前缀。

     下面的示例来自一个 DSL，其中有一个名为 "唱片集" 的域类，它与名为 Song 的域类具有嵌入关系：

    ```xml
    <albumMoniker title="/My Favorites/Jazz after Teatime" />
    <songMoniker title="/My Favorites/Jazz after Teatime/Hot tea" />
    ```

     如果目标类具有域属性（  `true` 在 **Xml 序列化行为** 中，此选项为其设置为名字对象键），则将使用限定键名字对象。 在此示例中，为域类 "唱片集" 和 "歌曲" 中名为 "Title" 的域属性设置了此选项。

限定密钥名字对象比 ID 名字对象更易于读取。 如果你想要将模型文件的 XML 作为人员读取，请考虑使用限定的密钥名字。 但是，用户可以将多个元素设置为具有相同的名字对象密钥。 重复键可能导致文件无法正确地重新加载。 因此，如果您定义使用限定密钥名字对象引用的域类，则应考虑阻止用户保存具有重复名字对象的文件的方法。

### <a name="to-set-a-domain-class-to-be-referenced-by-id-monikers"></a>设置由 ID 名字对象引用的域类

1. 请确保为类及其基类中的每个域属性都 **是名字对象密钥** `false` 。

    1. 在 DSL 资源管理器中，展开 " **Xml 序列化 Behavior\Class data \\ \<the domain class> \Element data**"。

    2. 验证是否为每个域属性都 **是名字对象密钥** `false` 。

    3. 如果域类有一个基类，请重复此类中的过程。

2. 设置域类的 **序列化 Id**  =  `true` 。

     此属性可在 " **Xml 序列化行为**" 下找到。

### <a name="to-set-a-domain-class-to-be-referenced-by-qualified-key-monikers"></a>设置由限定的键名字对象引用的域类

- Set 是现有域类的域属性的 **名字对象密钥** 。 属性的类型必须为 `string` 。

    1. 在 DSL 资源管理器中，展开 " **Xml 序列化 Behavior\Class data \\ \<the domain class> \Element data**"，然后选择 "域" 属性。

    2. 在属性窗口中，set **是的名字对象键** 为 `true` 。

- \- 或 -

     使用 **命名域类** 工具创建新的域类。

     此工具创建一个新类，该类具有名为 Name 的域属性。 **是元素名称**，并且是此域属性的 **名字对象键** 属性将初始化为 `true` 。

- \- 或 -

     创建从域类到具有名字对象键属性的另一个类的继承关系。

### <a name="avoid-duplicate-monikers"></a>避免重复的名字对象

如果使用限定的键名字对象，则用户模型中的两个元素可能在键属性中具有相同的值。 例如，如果 DSL 具有具有属性名称的类人员，则用户可以将两个元素的名称设置为相同的名称。 虽然可以将模型保存到文件，但它不会正确地重新加载。

有多种方法可帮助避免这种情况：

- 设置 **为**  =  `true` key domain 属性的元素名称。 选择 DSL 定义关系图上的 "域" 属性，然后在 "属性窗口中设置值。

     当用户创建类的新实例时，此值将导致自动为域属性分配不同的值。 默认行为向类名的末尾添加一个数字。 这不会阻止用户将该名称更改为重复的名称，但在保存模型之前，用户不设置该值时，这会有所帮助。

- 启用 DSL 验证。 在 DSL 资源管理器中，选择 "编辑器 \ 验证"，并将 " **使用 ...** " 属性设置为 `true` 。

     自动生成的验证方法会检查歧义。 方法位于 `Load` 验证类别中。 这可以确保用户将收到警告，指出可能无法重新打开文件。

     有关详细信息，请参阅 [Domain-Specific 语言的验证](../modeling/validation-in-a-domain-specific-language.md)。

### <a name="moniker-paths-and-qualifiers"></a>名字对象路径和限定符

限定的键名字对象以名字对象键结尾，在嵌入树中以其父级的名字对象作为前缀。 例如，如果一个相集的名字是：

```xml
<albumMoniker title="/My Favorites/Jazz after Teatime" />
```

然后，该相集中的一个歌曲可以是：

```xml
<songMoniker title="/My Favorites/Jazz after Teatime/Hot tea" />
```

但是，如果按 ID 引用了本集，则名字对象将如下所示：

```xml
<albumMoniker Id="77472c3a-9bf9-4085-976a-d97a4745237c" />
<songMoniker title="/77472c3a-9bf9-4085-976a-d97a4745237c/Hot tea" />
```

请注意，由于 GUID 是唯一的，因此它永远不会以其父级的名字作为前缀。

如果知道特定域属性在模型中始终具有唯一值，可以将该属性的"名字 **对象限定** 符" `true` 设置为 。 这会使它用作限定符，而不使用父级的名字对象。 例如，如果同时为 Album 类的 Title 域属性设置 Is **Moniker Qualifier** 和 **Is Moniker Key，** 则不将模型的名称或标识符用于 Album 及其嵌入子级的名字对象：

```xml
<albumMoniker name="Jazz after Teatime" />
<songMoniker title="/Jazz after Teatime/Hot tea" />
```

## <a name="customize-the-structure-of-the-xml"></a>自定义 XML 的结构

若要进行以下自定义，请展开 DSL 资源管理器 **中的"Xml 序列化行为** "节点。 在域类下，展开"元素数据"节点以查看来自此类的属性和关系的列表。 选择关系，并调整其选项属性窗口。

- 将 **Omit 元素** 设置为 true 可省略源角色节点，仅保留目标元素的列表。 如果源类和目标类之间存在多个关系，则不应设置此选项。

    ```xml
    <familyTreeModel ...>
      <!-- The following node is omitted by using Omit Element: -->
      <!-- <people> -->
        <person name="Henry VIII" .../>
        <person name="Elizabeth I" .../>
      <!-- </people> -->
    </familyTreeModel>
    ```

- 设置 **"使用完整窗体** "，将目标节点嵌入表示关系实例的节点中。 将域属性添加到域关系时，会自动设置此选项。

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

- 将 **Representation**  =  **元素** 设置为将域属性另存为元素而不是属性值。

    ```xml
    <person name="Elizabeth I" birthYear="1533">
      <deathYear>1603</deathYear>
    </person>
    ```

- 若要更改属性和关系的序列化顺序，请右键单击"元素数据"下的项，并使用"上移"或"下移 **"** 菜单命令。

## <a name="major-customization-using-program-code"></a>使用程序代码的主要自定义项

可以替换部分或所有序列化算法。

建议研究 **Dsl\Generated Code\Serializer.cs** 和 **SerializationHelper.cs 中的代码**。

### <a name="to-customize-the-serialization-of-a-particular-class"></a>自定义特定类的序列化

1. 在 **Xml 序列** 化行为 下的该类的节点中，将 设置为 **Custom。**

2. 转换所有模板，生成解决方案，并调查生成的编译错误。 每个错误附近的注释说明了必须提供的代码。

### <a name="to-provide-your-own-serialization-for-the-whole-model"></a>为整个模型提供你自己的序列化

1. 替代 Dsl\GeneratedCode\SerializationHelper.cs 中的方法

## <a name="options-in-xml-serialization-behavior"></a>Xml 序列化行为中的选项

在 DSL 资源管理器中，Xml 序列化行为节点包含每个域类、关系、形状、连接器和关系图类的子节点。 每个节点下都是一个属性和关系列表，这些属性和关系都来自该元素。 关系在其自己的右侧和源类下都表示。

下表总结了可以在 DSL 定义的此部分中设置的选项。 在每种情况下，在 DSL 资源管理器中选择一个元素，并设置"属性窗口"。

### <a name="xml-class-data"></a>Xml 类数据

这些元素位于 DSL 资源管理器中的 **Xml 序列化行为\类数据 下**。

|属性|说明|
|-|-|
|具有自定义元素架构|如果为 True，则指示域类具有自定义元素架构|
|是自定义的|如果要为此 **域** 类编写自己的序列化和反序列化代码，请设置为 True。<br /><br /> 生成解决方案并调查错误以发现详细说明。|
|域类|此类数据节点应用到的域类。 只读。|
|元素名称|此类的元素的 Xml 节点名称。 默认值是域类名称的小写版本。|
|名字对象属性名称|名字对象元素中用于包含引用的属性的名称。 如果为空，则使用键属性或 ID 的名称。<br /><br /> 此示例中，它是"name"：  `<personMoniker name="/Mike Nash"/>`|
|名字对象元素名称|用于引用此类元素的名字对象的 xml 元素的名称。<br /><br /> 默认值是带有"名字对象"后缀的类名的一个小写版本。 例如 `personMoniker`。|
|名字对象类型名称|为此类元素的名字对象生成的 xsd 类型的名称。 XSD 位于 **Dsl\Generated \\ \* Code Schema.xsd 中**|
|序列化 ID|如果为 True，则元素 GUID 包含在文件中。 如果没有标记为"是名字对象键"的属性，并且DSL 定义对此类的引用关系，则此属性必须为 true。|
|类型名称|从指定的域类在 xsd 中生成的 xml 类型的名称。|
|说明|与此元素关联的非正式说明|

### <a name="xml-property-data"></a>Xml 属性数据

Xml 属性节点位于类节点下。

|属性|说明|
|-|-|
|域属性|xml 序列化配置数据应用于的属性。 只读。|
|名字对象键|如果为 True，则属性用作创建引用此域类的实例的名字对象的键。|
|是名字对象限定符|如果为 True，则属性用于在名字对象中创建限定符。 如果为 false，并且此域类的 SerializeId 不为 true，则名字对象由嵌入树中父元素的名字对象限定。|
|表示形式|如果为 Attribute，则属性序列化为 xml 属性;如果为 Element，则序列化为元素;如果忽略，则不序列化。|
|Xml 名称|用于表示属性的 xml 属性或元素的名称。 默认情况下，这是域属性名称的一个小写版本。|
|说明|与此元素关联的非正式说明|

### <a name="xml-role-data"></a>Xml 角色数据

角色数据节点位于源类节点下。

|属性|说明|
|-|-|
|具有自定义名字对象|如果要提供自己的代码来生成和解析遍历此关系的名字对象，请设置为 true。<br /><br /> 有关详细说明，请生成解决方案，然后双击错误消息。|
|域关系|指定这些选项应用于的关系。 只读。|
|Omit 元素|如果为 true，则架构中将省略与源角色对应的 XML 节点。<br /><br /> 如果源类和目标类之间存在多个关系，此角色节点将区分属于这两种关系的链接。 因此，建议在这种情况下不要设置此选项。|
|Role 元素名称|指定派生自源角色的 XML 元素的名称。 默认值为角色属性名称。|
|使用完整窗体|如果为 true，则每个目标元素或名字对象都包含在表示关系的 XML 节点中。 如果关系具有其自己的域属性，应设置为 true。|

## <a name="see-also"></a>请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)
