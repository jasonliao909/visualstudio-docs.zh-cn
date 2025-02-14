---
title: 了解模型、类和关系
description: 了解域特定语言 (DSL) 是如何由其 DSL 定义文件定义的，以及 DSL 解决方案中的大多数程序代码是如何在此文件中生成的。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, models
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: e1fed82d9a8baaf44300e002a5436a532781ed01
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663859"
---
# <a name="understanding-models-classes-and-relationships"></a>了解模型、类和关系
域特定语言 (DSL) 是由其 DSL 定义文件以及你可能编写的任何自定义程序代码定义的。 DSL 解决方案中的大多数程序代码都是通过此文件生成的。

 本主题介绍 DSL 定义的核心功能。

## <a name="the-dsl-definition"></a>DSL 定义
 打开 `Dsl\DslDefinition.dsl` 时，Visual Studio 窗口如下图所示。

 ![dsl 设计器](../modeling/media/dsl_designer.png)

 DSL 定义关系图中显示了 DSL 定义中最重要的信息。 还会在 DSL 资源管理器中显示其他信息，该信息也是 Dsldefinition.dsl 的一部分，通常出现在关系图一侧。 可以使用关系图处理最常见的任务，使用 DSL 资源管理器进行更高级的自定义。

 DSL 定义关系图显示定义模型元素的域类，以及定义模型元素间的链接的关系。 它还显示用于向用户显示模型元素的形状和连接器。

 ![具有泳道的 dsl 设计器](../modeling/media/dsl_desinger.png)

 在关系图或 DSL 资源管理器中选择 DSL 定义中的项时，属性窗口中会显示相关信息。 其他信息可能显示在“DSL 详细信息”窗口中。

### <a name="models-are-instances-of-dsls"></a>模型是 DSL 实例
 模型是用户创建的 DSL 实例。 模型包含模型元素，它们是你定义的域类的实例，以及元素之间的链接，它们是你定义的域关系的实例。 模型还可以具有形状和连接器，它们在关系图上显示模型元素和链接。 DSL 定义包括形状类、连接器类和关系图类。

 DSL 定义也称为域模型。 DSL 定义或域模型是域特定语言的设计时表示形式，而模型是域特定语言的运行时实例化。

## <a name="domain-classes-define-model-elements"></a>域类定义模型元素
 域类用于创建域中的各种元素，而域关系是元素之间的链接。 它们是元素和链接的设计时表示形式，它们在域特定语言用户创建模型时由用户进行实例化。

 此图显示了由音乐库 DSL 的用户创建的模型。 音乐专辑由包含歌曲列表的框表示。 艺术家由圆角框表示，并连接到他们所提供的专辑。

 ![生成的 DSL 实例模型](../modeling/media/music_instance.png)

 DSL 定义将两个方面隔开。 模型关系图上模型元素的外观是通过使用形状类和连接器类定义的。 使用域类和域关系定义模型中提供的信息。

 下图显示了音乐库 DSL 定义中的域类和关系。

 ![嵌入关系和引用关系](../modeling/media/music_classes.png)

 下图显示了四个域类：Music、Album、Artist 和 Song。 域类定义域属性，如 Name、Title 等。 在实例模型中，其中某些属性的值显示在关系图上。

 类之间的关系为域关系：MusicHasAlbums、MusicHasArtists、AlbumbHasSongs 和 ArtistAppearedOnAlbums。 关系具有多重性，如 1..1、0..*。 例如，每个 Song 都必须通过 AlbumHasSongs 关系仅与一个 Album 相关。 每个 Album 可以有任意数量的 Song。

### <a name="rearranging-the-dsl-definition-diagram"></a>重新排列 DSL 定义关系图
 请注意，域类可以在 DSL 定义关系图上出现多次，如图中的 Album 所示。 始终有一个主视图，并且可以有一些引用视图。

 若要重新排列 DSL 定义关系图，可以执行以下操作：

- 使用“在此处显示树”和“拆分树”命令交换主视图和引用视图。 右键单击单个域类可查看这些命令。

- 通过按 Ctrl+向上键和 Ctrl+向下键对域类和形状类重新排序。

- 使用每个形状右上角的图标折叠或展开类。

- 单击域类底部的减号 (-)，折叠树的各个部分。

## <a name="inheritance"></a>继承
 域类可以通过继承来定义。 若要创建继承派生，请单击“继承”工具，单击派生类，然后单击基类。 模型元素包含在其自己的域类上定义的所有属性，以及从基类继承的所有属性。 它还会继承关系中的角色。

 还可以在关系、形状和连接器之间使用继承。 继承必须保留在同一个组中。 不能从域类继承形状。

## <a name="domain-relationships"></a>域关系
 可以按关系链接模型元素。 链接始终为二进制；它们精确地链接两个元素。 但是，任何元素都可以有多个指向其他对象的链接，甚至在同一对元素之间也可以有多个链接。

 正如你可以定义不同的元素类一样，你也可以定义不同的链接类。 链接的类称为域关系。 域关系指定其实例可以连接的元素类。 关系的每个端都称为角色，域关系定义两个角色的名称以及关系本身的名称。

 有两种域关系：嵌入关系和引用关系。 在 DSL 定义关系图中，嵌入关系在每个角色上都有实线，引用关系则使用虚线。

### <a name="embedding-relationships"></a>嵌入关系
 模型中的每个元素（其根除外）都是一个嵌入链接的目标。 因此，整个模型构成嵌入链接的单个树。 嵌入关系表示包含或所有权。 以这种方式相关的两个模型元素也称为父元素和子元素。 子元素被认为嵌入在父元素中。

 嵌入链接通常不在关系图上显式显示为连接器。 相反，它们通常由包含来表示。 模型的根由关系图表示，嵌入在其中的元素显示为关系图上的形状。

 在此示例中，根类 Music 具有与 Album 的嵌入关系 MusicHasAlbums，后者将 AlbumHasSongs 嵌入到 Song。 Song 显示为每个 Album 内列表中的项。 Music 还有一个嵌入到 Artist 类的 MusicHasArtists，其实例也显示为关系图上的形状。

 默认情况下，在删除嵌入元素的父元素时，会自动将其删除。

 如果将模型保存到 XML 格式的文件中，则嵌入元素将嵌套在其父元素内，除非你已自定义序列化。

> [!NOTE]
> 嵌入与继承不同。 嵌入关系中的子元素不继承父元素的属性。 嵌入是模型元素之间的链接类型。 继承是类之间的关系，不会在模型元素之间创建链接。

### <a name="embedding-rules"></a>嵌入规则
 实例模型中的每个元素只能是一个嵌入链接的目标，模型的根除外。

 因此，每个非抽象域类（根类除外）都必须至少是一个嵌入关系的目标，或必须从基类继承嵌入。 一个类可以是两个或多个嵌入的目标，但其实例模型元素一次只能有一个父元素。 从目标到源的多重性必须为 0..1 或 1..1。

### <a name="the-explorer-displays-the-embedding-tree"></a>资源管理器显示嵌入树
 DSL 定义还会创建一个资源管理器，用户可以在其模型关系图旁边看到该资源管理器。

 ![生成的 DSL 资源管理器](../modeling/media/music_explorer.png)

 资源管理器将显示模型中的所有元素，甚至是还没有为其定义任何形状的元素。 它显示元素和嵌入关系，但不显示引用关系。

 若要查看某个元素的域属性的值，用户可以在模型关系图或模型资源管理器中选择一个元素，然后打开属性窗口。 它将显示所有域属性，包括未显示在关系图中的属性。 在示例中，每个 Song 都有 Title 和 Genre，但关系图上只显示 Title 值。

## <a name="reference-relationships"></a>引用关系
 引用关系表示任何未嵌入的关系。

 引用关系通常在关系图中显示为形状之间的连接器。

 在模型的 XML 表示形式中，使用名字对象表示两个元素之间的引用链接。 也就是说，名字对象是唯一标识模型中每个元素的名称。 每个模型元素的 XML 节点都包含一个节点，该节点指定关系的名称和其他元素的名字对象。

## <a name="roles"></a>角色
 每个域关系都有两个角色：源角色和目标角色。

 在下图中，域类 Publisher 和域关系 PublisherCatalog 之间的行是源角色。 域关系与 Album 域类之间的行是目标角色。

 ![角色和属性。](../modeling/media/propertycode.png)

 编写遍历模型的程序代码时，与关系关联的名称尤为重要。 例如，生成 DSL 解决方案时，生成的类Publisher 有一个属性 Catalog，该属性表示 Album 集合。 类 Album 具有属性 Publisher，该属性表示类 Publisher 的单个实例。

 在 DSL 定义中创建关系时，将为属性和关系名称提供默认值。 但你可以更改这些值。

## <a name="multiplicities"></a>多重性
 多重性指定在域关系中可以具有相同角色的元素数。 在示例中，Catalog 角色的零对多 (0..\*) 多重性设置指定 Publisher 域类的任何实例可以具有任意数量的 PublisherCatalog 关系链接。

 通过键入关系图或在“属性”窗口中修改 `Multiplicity` 属性来配置角色的多重性。 下表描述了此属性的设置。

|多重性类型|说明|
|-|-|
|0..*（零对多）|域类的每个实例可以有多个关系实例，也可以没有关系实例。|
|0..1（零对一）|域类的每个实例可以有一个关系实例，也可以没有关系实例。|
|1..1（一）|域类的每个实例可以有一个关系实例。 不能从角色类的任何实例创建此关系的多个实例。 如果启用了验证，则当角色类的任何实例没有关系实例时，将出现验证错误。|
|1..*（一对多）|具有此多重性的角色上类的每个实例可以有多个关系实例，并且每个实例必须至少有一个关系实例。 如果启用了验证，则当角色类的任何实例没有关系实例时，将出现验证错误。|

## <a name="domain-relationships-as-classes"></a>作为类的域关系
 链接在 Store 中表示为 LinkElement 实例，该实例是 ModelElement 的派生类。 可以在域关系的域模型关系图中定义这些属性。

 还可以将关系作为其他关系的源或目标。 在域模型关系图中，右键单击域关系，然后单击“显示为类”。 将出现其他类框。 然后，可以将关系连接到它。

 可以部分通过继承定义关系，就像使用域类一样。 选择派生关系，并在属性窗口中设置“基关系”。

 派生关系专门化其基关系。 它链接的域类应派生自基关系链接的类或与之相同。 在模型中创建派生关系链接时，它是派生关系和基关系的实例。 在程序代码中，可以使用基类或派生类生成的属性导航到链接的另一端。

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))