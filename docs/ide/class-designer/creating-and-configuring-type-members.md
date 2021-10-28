---
title: 创建和配置类型成员（类设计器）
description: 了解如何将成员添加到类图上的类型中并在“类详细信息”窗口中配置这些成员。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.classdetails.method
- vs.classdetails.property
- vs.classdetails.parameter
- vs.classdetails.event
- vs.classdetails.field
helpviewer_keywords:
- Class Designer [Visual Studio], member creation
- type members, modifying in Class Designer
- parameters [ASP.NET Web Services], adding to methods
- type members, configuring
- type members
- members
- type members, creating
- members, creating
- Class Designer [Visual Studio], type members
- read-only information, displaying
- members, configuring
- methods [Visual Studio], adding parameters
- Class Details window
- Class Details window, member creation
ms.assetid: 42af8738-3738-4ca7-82ff-edf573a68f96
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 793b4262e457301f79f625156194573d63664e9a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641899"
---
# <a name="create-and-configure-type-members-in-class-designer"></a>在类设计器中创建和配置类型成员

可以将以下成员添加到类图上的类型中并在“类详细信息”窗口中配置这些成员：

|**Type**|**包含的成员**|
|--------------| - |
|类|方法、属性（对于 C# 和 Visual Basic）、字段、事件（对于 C# 和 Visual Basic）、构造函数（方法）、析构函数（方法）和常数|
|Enum|成员|
|接口|方法、属性和事件（对于 C# 和 Visual Basic）|
|抽象类|方法、属性（对于 C# 和 Visual Basic）、字段、事件（对于 C# 和 Visual Basic）、构造函数（方法）、析构函数（方法）和常数|
|结构（C# 中的结构）|方法、属性（对于 C# 和 Visual Basic）字段、事件（对于 C# 和 Visual Basic）、构造函数（方法）和常数|
|委托|parameter|
|模块（仅限 VB）|方法、属性、字段、事件、构造函数和常量|

> [!NOTE]
> 通过使用自动实现的属性（仅限 C#），属性的 get 和 set 访问器不需要其他逻辑，因而属性声明更加简洁。 若要显示完全签名，请从“类图”菜单中选择“更改成员格式” > “显示完全签名”  。 有关自动实现的属性的详细信息，请参阅[自动实现的属性](/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties)。

## <a name="common-tasks"></a>常见任务

|任务|支持内容|
|----------| - |
|**开始操作：** 创建并配置类型成员之前，必须打开“类详细信息”窗口。|- [打开“类详细信息”窗口](creating-and-configuring-type-members.md#open-the-class-details-window)<br />- [“类详细信息”用法说明](creating-and-configuring-type-members.md#class-details-usage-notes)<br />- [显示只读信息](creating-and-configuring-type-members.md#display-of-read-only-information)<br />- [类图和“类详细信息”窗口中的键盘快捷方式和鼠标快捷方式](keyboard-and-mouse-shortcuts-in-the-class-diagram-and-class-details-window.md)|
|**创建和修改类型成员：** 可以使用“类详细信息”窗口创建新成员、修改成员并向方法中添加参数。|- [创建成员](creating-and-configuring-type-members.md#create-members)<br />- [修改类型成员](creating-and-configuring-type-members.md#modify-type-members)<br />- [向方法中添加参数](creating-and-configuring-type-members.md#add-parameters-to-methods)|

## <a name="open-the-class-details-window"></a>打开“类详细信息”窗口

默认情况下，在打开一个新类图时，“类详细信息”窗口会自动显示。 请参阅[如何：向项目添加类图](how-to-add-class-diagrams-to-projects.md)。 也可以通过以下方式打开“类详细信息”窗口：

- 右键单击关系图中的任何类以显示上下文菜单，然后选择“类详细信息”。

- 从该菜单栏中，选择“视图” > “其他窗口”“类详细信息” > 。

## <a name="create-members"></a>创建成员

可以使用以下任何工具创建成员：

- 类设计器

- “类详细信息”窗口工具栏

- “类详细信息”窗口

> [!NOTE]
> 还可使用本节中介绍的过程创建构造函数和析构函数。 请切记构造函数和析构函数是特殊类型的方法，因此这两种函数显示在类图形状的“方法”隔离舱以及“类详细信息”窗口网格的“方法”区域  。

> [!NOTE]
> 可以添加到委托中的唯一实体就是参数。 注意，标题为“使用‘类详细信息’窗口工具栏创建成员”的过程对此操作无效。

### <a name="create-a-member-using-class-designer"></a>使用类设计器创建成员

1. 右键单击要向其中添加成员的类型，将鼠标指向“添加”，然后选择要添加的成员类型。

     将创建一个新的成员签名并将其添加到该类型中。 系统将以默认名称为其命名，可在“类设计器”、“类详细信息”窗口或“属性”窗口中更改该名称  。

2. 或者，也可指定有关成员的其他详细信息，例如成员类型。

### <a name="create-a-member-using-the-class-details-window-toolbar"></a>使用“类详细信息”窗口工具栏创建成员

1. 在关系图面上选择希望向其添加成员的类型。

     该类型获得焦点，其内容显示在“类详细信息”窗口中。

2. 在“类详细信息”窗口工具栏上单击顶部图标，再从下拉列表中选择“新建 \<member>” 。

     光标移至要添加的那类成员所对应行中的“名称”字段。 例如，如果单击了“新建属性”，则光标将移至“类详细信息”窗口中“属性”区域的一个新行上  。

3. 键入希望创建的成员的名称，再按 Enter（或者通过按 Tab 等方式移动焦点）。

     将创建一个新的成员签名并将其添加到该类型中。 现在该成员就存在于代码中，并显示在“类设计器”、“类详细信息”窗口和“属性”窗口中 。

4. 或者，也可指定有关成员的其他详细信息，例如成员类型。

### <a name="create-a-member-using-the-class-details-window"></a>使用“类详细信息”窗口创建成员

1. 在关系图面上选择希望向其添加成员的类型。

     该类型获得焦点，其内容显示在“类详细信息”窗口中。

2. 在“类详细信息”窗口中包含要添加的那类成员的部分中，单击“\<add member>” 。 例如，若要添加一个字段，请单击“\<add field>”。

3. 键入希望创建的成员的名称，再按 Enter。

     将创建一个新的成员签名并将其添加到该类型中。 现在该成员就存在于代码中，并显示在“类设计器”、“类详细信息”窗口和“属性”窗口中 。

4. 或者，也可指定有关成员的其他详细信息，例如成员类型。

    > [!NOTE]
    > 还可使用键盘快捷方式创建成员。 有关详细信息，请参阅[类图和“类详细信息”窗口中的键盘快捷方式和鼠标快捷方式](keyboard-and-mouse-shortcuts-in-the-class-diagram-and-class-details-window.md)。

## <a name="modify-type-members"></a>修改类型成员

类设计器使你能够修改关系图上显示的类型的成员。 你可以修改类图上显示的任何非只读类型的成员。 通过在设计图面、“属性”窗口和“类详细信息”窗口上使用就地编辑来修改类型成员。

“类详细信息”窗口中显示的所有成员均表示类图中类型的成员。 有四种成员：方法、属性、字段和事件。

所有成员均显示在标题之下，这些标题按种类对成员进行分组。 例如，所有属性均显示在“属性”标题之下，它们像网格中的节点一样可以折叠或展开。

每个成员行均显示以下元素：

- **成员图标**

     每种成员均由各自的图标表示。 将鼠标指向成员图标时，可显示该成员的签名。 单击成员图标或成员图标左边的空白处可选择该行。

- **成员名称**

     成员行的“名称”列显示成员的名称。 此名称还显示在“属性”窗口的“名称”属性中。 使用此单元格可更改任何具有读写权限的成员的名称。

     如果“名称”列过窄而无法完整地显示名称，则将鼠标指向成员名称即可显示完整名称。

- **成员类型**

     “成员类型”单元格使用 IntelliSense，这使你可以选择当前项目或引用项目中列出的所有可用类型。

- **成员修饰符**

     将成员的可见性修饰符更改为 `Public` (`public`)、`Private` (`private`)、`Friend` (`internal`) `Protected` (`protected`)、`Protected Friend` (`protected internal`) 或 `Default`。

- **\<add member>**

     “类详细信息”窗口中最后一行的“名称”单元格中包含文本“\<add member>”  。 如果单击此单元格，则可创建新成员。 有关详细信息，请参阅[创建成员](creating-and-configuring-type-members.md#create-members)。

- “属性”窗口中的成员属性

     “类详细信息”窗口显示的成员属性是“属性”窗口中所显示的成员属性的子集。 在一个位置更改某个属性将使该属性的值在全局范围内得到更新， 包括该属性的值在其他位置的显示。

- **摘要**

     “摘要”单元格公开该成员相关信息的摘要。 单击“摘要”单元格中的省略号可查看或编辑该成员的“摘要”、“返回类型”和“标记”相关信息   。

- **隐藏**

     选中“隐藏”复选框后，该成员将不会显示在该类型中。

### <a name="to-modify-a-type-member"></a>修改类型成员

1. 使用类设计器选择一种类型。

2. 如果未显示“类详细信息”窗口，请在“类设计器”工具栏上单击“类详细信息’窗口”按钮 。

3. 编辑“类详细信息”窗口网格中各字段的值。 每编辑完一个字段按一下 Enter，或者以其他方式（例如按 Tab）将焦点从已编辑的字段中移开。 你的编辑将立即在代码中反映出来。

    > [!NOTE]
    > 如果只希望修改成员的名称，你可以使用就地编辑来进行操作。

## <a name="add-parameters-to-methods"></a>向方法中添加参数

使用“类详细信息”窗口向方法中添加参数。 可以将参数配置为必需或可选。 如果为参数的“可选的默认值”属性提供值，将指示设计器以可选参数的形式生成代码。

参数行包含以下项：

- **Name**

     参数行中的“名称”列显示参数的名称。 此名称还显示在“属性”窗口的“名称”属性中。 使用此单元格可更改任何具有读写权限的参数的名称。

     如果“名称”列过窄而无法显示参数的完整名称，将光标指向参数名即可显示参数的名称。

- **Type**

     “参数类型”单元格使用 IntelliSense，由此可选择当前项目或引用项目中列出的所有可用类型。

- **修饰符**

     参数行中的“修饰符”单元格接受并显示参数的新修饰符。 若要输入新的参数修饰符，请使用下拉列表框选择 C# 中的“None”、“ref”、“out”或“params”以及 VB 中的 “ByVal”、“ByRef”或“ParamArray”      。

- **摘要**

     参数行中的“摘要”单元格允许输入代码注释，在代码编辑器中输入参数时，这些注释将出现在 IntelliSense 中。

- **\<add parameter>**

     成员的最后一个参数行的“名称”单元格中包含文本“<添加参数\>” 。 单击此单元格可创建新的参数。 有关详细信息，请参阅[向方法中添加参数](creating-and-configuring-type-members.md#add-parameters-to-methods)。

“属性”窗口显示的参数属性与“类详细信息”窗口中显示的相同 ：“名称”、“类型”、“修饰符”、“摘要”以及“可选默认值”属性    。 在一个位置更改某个属性将使该属性的值在全局范围内得到更新，包括这个属性值在其他位置的显示。

> [!NOTE]
> 若要向委托中添加参数，请参阅[创建成员](creating-and-configuring-type-members.md#create-members)。

> [!NOTE]
> 尽管析构函数是一种方法，但它不能有参数。

### <a name="to-add-a-parameter-to-a-method"></a>向方法添加参数

1. 在关系图图面上，单击你要向其中添加参数的方法所属的类型。

     该类型获得焦点，其内容显示在“类详细信息”窗口中。

2. 在“类详细信息”窗口中，展开你要向其中添加参数的方法所在的行。

     此时将显示缩进的参数行，其中仅包含一对括号和文字“\<add parameter>”。

3. 单击“\<add parameter>”，键入新参数的名称，然后按 Enter 。

     新参数随即添加到方法和方法的代码中。 它显示在“类详细信息”窗口和“属性”窗口中。

4. （可选）指定参数的其他详细信息，例如参数类型。

### <a name="to-add-an-optional-parameter-to-a-method"></a>向方法添加可选参数

1. 在关系图面上，单击要向其中添加可选参数的方法所属的类型。

     该类型获得焦点，其内容显示在“类详细信息”窗口中。

2. 在“类详细信息”窗口中，展开要向其中添加可选参数的方法所在的行。

     此时将显示缩进的参数行，其中仅包含一对括号和文字“\<add parameter>”。

3. 单击“\<add parameter>”，键入新参数的名称，然后按 Enter 。

     新参数随即添加到方法和方法的代码中。 它显示在“类详细信息”窗口和“属性”窗口中。

4. 在“属性”窗口中，为“可选的默认值”属性键入值。 如果设置参数的“可选的默认值”属性，将使该参数变为可选。

    > [!NOTE]
    > 可选参数必须是参数列表中位于最后面的参数。

## <a name="class-details-usage-notes"></a>“类详细信息”用法说明

请注意以下关于使用“类详细信息”窗口的技巧。

### <a name="editable-and-non-editable-cells"></a>可编辑的和不可编辑的单元格

除了下面几个特例外，“类详细信息”窗口中的所有单元格都可以编辑：

- 整个类型是只读的，比如它位于引用的程序集中时。 当你在类设计器中选择形状时，“类详细信息”窗口将以只读方式显示形状的详细信息。

- 对于索引器，名称是只读的，其余内容（类型、修饰符、摘要）都是可编辑的。

- 所有泛型参数在“类详细信息”窗口中都是只读的。 要更改泛型参数，请编辑它的源代码。

- 泛型类型上定义的类型参数的名称是只读的。

- 如果类型的代码是中断的（不可分析），“类详细信息”窗口将以只读方式显示该类型的内容。

### <a name="the-class-details-window-and-source-code"></a>“类详细信息”窗口和源代码

- 右键单击“类详细信息”窗口（或类设计器）中的一个形状，然后单击“查看代码”，即可查看源代码。 源代码文件随即会打开并滚动到选定的元素。

- 对源代码的更改会立即在类设计器和“类详细信息”窗口中所显示的签名信息中反映出来。 如果“类详细信息”窗口当时是关闭的，那么在你下次打开它时就会看到这些新信息。

- 如果类型的代码是中断的（不可分析），“类详细信息”窗口将以只读方式显示该类型的内容。

### <a name="clipboard-functionality-in-the-class-details-window"></a>“类详细信息”窗口中的剪贴板功能

你可以复制或剪切“类详细信息”窗口中的字段或行，然后将它们粘贴到另一个类型中。 仅当行不是只读的时候才能剪切。 在粘贴行时，“类详细信息”窗口会给行分配一个新名称（派生自所复制的行的名称）以避免冲突。

## <a name="display-of-read-only-information"></a>显示只读信息

类设计器和“类详细信息”窗口可显示以下各项的类型（及类型成员）：

- 包含类关系图的项目

- 引用了其他项目的项目，所引用的项目包含类关系图

- 引用了项目的程序集，所引用的项目包含类关系图

在后两种情况下，被引用的实体（类型或成员）在表示该实体的关系图中是只读的。

整个项目或项目的一部分（例如单个文件）可以是只读的。 最常见的项目或项目的一个文件只读的情况发生在项目受源代码管理（并且尚未签出）时、项目存在于外部程序集中时，或在操作系统认为文件只读时。

**源代码管理**

因为类图是作为文件保存在项目中的，所以你需要签出该项目，以保存在类设计器或“类详细信息”窗口中所做的任何更改。

**只读项目**

项目只读的原因也有可能不是源代码管理。 关闭项目时会显示一个对话框，询问是覆盖项目文件、放弃更改（不保存）还是取消关闭操作。 如果选择进行覆盖，则项目文件会被覆盖并设置为只读。 新的类关系图文件也会添加进来。

**只读类型**

如果尝试保存文件包含其源代码文件为只读的类型，则会出现“保存只读文件”对话框，该对话框提供几种选择，可以将文件以新的名称保存、另存至新位置或者覆盖只读文件。 如果选择覆盖文件，则新的副本不再是只读的。

如果代码文件包含语法错误，则显示该文件中的代码的形状将临时处于只读状态，直至修复该语法错误。 处于此状态的形状以红色文本和红色图标的形式显示工具提示“源代码文件包含一个分析错误”。

存在于其他项目节点或被引用程序集节点下的被引用类型（例如 .NET 类型）在类设计器设计图面上指示为只读。 存在于已打开的项目中的本地类型是读写的，其在类设计器设计图面上的形状作出的指示也是如此。

索引器在代码中和“类详细信息”窗口中是读写的，但索引器名称是只读的。

无法使用类设计器或“类详细信息”窗口来编辑分部方法；必须使用代码编辑器来编辑它们。

无法使用类设计器或“类详细信息”窗口来编辑本机 C++ 代码；必须使用代码编辑器来编辑本机 C++ 代码。

## <a name="see-also"></a>请参阅

- [查看类型和关系](designing-and-viewing-classes-and-types.md)
- [重构类和类型](refactoring-classes-and-types.md)
