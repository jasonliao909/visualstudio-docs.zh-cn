---
title: 依赖项关系图：指南
description: 了解如何在 Visual Studio 中创建依赖关系图，以较高的层次描述应用程序的体系结构。
ms.custom: SEO-VS-2020
ms.date: 09/28/2018
ms.topic: conceptual
helpviewer_keywords:
- architecture, dependency diagrams
- dependency diagrams
- diagrams - modeling, layer
- constraints, architectural
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: c1bb37c00e2437d214a7607a1a5dd8bf062197d3da7be26b04f28225bb321984
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121428986"
---
# <a name="dependency-diagrams-guidelines"></a>依赖项关系图：准则

通过在 Visual Studio 中创建 *依赖关系图*，以较高的级别描述你的应用程序的体系结构。 通过使用依赖关系图验证代码，确保你的代码与此设计保持一致。 还可以在生成过程中包括层验证。 请参阅第 [9 频道视频：使用依赖关系图设计和验证体系结构](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Using-layer-diagrams-to-design-and-validate-your-architecture)。

若要查看支持此功能的 Visual Studio 的版本，请参阅 [体系结构和建模工具的版本支持](../modeling/analyze-and-model-your-architecture.md#VersionSupport)。

> [!NOTE]
> 从 Visual Studio 2019 16.2 版开始，支持 .net Core 项目的依赖项关系图。

## <a name="what-is-a-dependency-diagram"></a>什么是依赖项关系图？

与传统的体系结构关系图一样，依赖关系图确定了设计及其依赖项的主要组件或功能单元。 关系图上的每个节点（称为 *层*）表示命名空间、项目或其他项目的逻辑组。 您可以绘制出您的设计中存在的依赖关系。 与传统的体系结构关系图不同的是，您可以验证源代码中的实际依赖关系符合您指定的预期依赖关系。 通过在[!INCLUDE[esprtfs](../code-quality/includes/esprtfs_md.md)]上验证常规生成的一部分，您可以确保程序代码继续符合系统的体系结构将来的更改。 请参阅 [依赖关系图：参考](../modeling/layer-diagrams-reference.md)。

## <a name="how-to-design-or-update-your-app-with-dependency-diagrams"></a>如何在依赖项关系图中设计或更新应用程序

以下步骤概述了如何在开发过程中使用依赖关系图。 本主题中的后面几节描述了有关每个步骤的更多详细信息。 如果你正在开发新的设计，请忽略引用现有代码的步骤。

> [!NOTE]
> 这些步骤按大致顺序显示。 您可能需要重叠任务、重新排序它们以符合您自己的具体情况，并在项目中的每个迭代开始时重新访问它们。

1. 为整个应用程序或其中的某个层[创建依赖关系图](#Create)。

2. [定义用于表示应用程序的主要功能区域或组件的层](#CreateLayers) 。 按其功能命名这些层，例如“演示文稿”或“服务”。 如果有 Visual Studio 解决方案，则可以将每个层 *与项目集合*（如项目、命名空间、文件等）相关联。

3. 发现各层之间[的现有依赖关系](#Generate)。

4. [编辑层和依赖项](#EditArchitecture) 以显示希望代码反映的更新的设计。

5. 通过创建层来表示主要体系结构块或组件，并定义依赖项以显示每个层如何使用其他层来[设计应用程序的新区域](#NewAreas)。

6. [编辑关系图的布局和外观](#EditLayout) ，以帮助您与同事讨论。

7. [对照依赖关系图验证代码](#Validate) ，以突出显示所需的代码和体系结构之间的冲突。

8. [更新代码以符合新的体系结构](#UpdateCode)。 以迭代方式开发和重构代码，直到此验证不再显示有冲突。

9. [在生成过程中包括层验证](#BuildValidation) 以确保代码继续遵循您的设计。

## <a name="create-a-dependency-diagram"></a><a name="Create"></a> 创建依赖关系图

依赖关系关系图必须在建模项目内创建。 您可以将新的依赖关系图添加到现有建模项目，为依赖关系图创建新的建模项目，或复制同一建模项目中的现有依赖关系图。

> [!IMPORTANT]
> 不要向另一个建模项目或解决方案中的另一个位置添加、拖动或复制现有依赖关系图。 即使修改了关系图，以这种方式复制的依赖项关系图也会具有与原始关系图相同的引用。 这将阻止层验证正常操作，并可能导致出现其他问题，例如，尝试打开该关系图时元素缺失或出现其他错误。

请参阅 [通过代码创建依赖关系图](../modeling/create-layer-diagrams-from-your-code.md)。

## <a name="define-layers-to-represent-functional-areas-or-components"></a><a name="CreateLayers"></a> 定义用于表示功能区域或组件的层

层表示项目的逻辑组，如 *项目、代码* 文件、命名空间、类和方法。 你可以从 Visual c # 和 Visual Basic 项目中的项目创建层，也可以通过链接文档（如 Word 文件或 PowerPoint 演示文稿）将规范或计划附加到层。 每一层显示为关系图上的一个矩形，并显示链接到它的项目数。 一个层可以包含描述更具体任务的嵌套的层。

一般原则是按其功能命名层，例如“演示文稿”或“服务”。 如果这些项目依赖关系紧密，则将它们放在同一层。 如果可以分别更新或在单独的应用程序中使用这些项目，请将它们放在不同的层中。 若要了解分层模式，请参阅中的模式 & 实践 [http://go.microsoft.com/fwlink/?LinkId=145794](https://archive.codeplex.com/?p=apparch) 。

> [!TIP]
> 某些类型的项目可以链接到层，但不支持对依赖关系图进行验证。 若要查看项目是否支持验证，请打开 " **层资源管理器** " 以查看项目链接的 " **支持验证** " 属性。 请参阅 [发现层之间的现有依赖关系](#Generate)。

更新不熟悉的应用程序时，你也可以创建代码图。 这些关系图可以帮助你在浏览代码时发现模式和依赖项。 使用解决方案资源管理器来浏览命名空间和类，它们通常与现有层具有很好的对应关系。 通过将这些代码项目从解决方案资源管理器拖动到依赖关系图中，将它们分配到层。 然后，你可以使用依赖关系图来帮助你更新代码，并使其与你的设计保持一致。

请参阅：

- [从代码创建依赖项关系图](../modeling/create-layer-diagrams-from-your-code.md)

- [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)

- [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)

## <a name="discover-existing-dependencies-between-layers"></a><a name="Generate"></a> 发现层之间的现有依赖关系

只要与一个层关联的项目引用与另一个层关联的项目，就存在依赖关系。 例如，一个层中的某个类声明了一个拥有其他层中的某个类的变量。 您可以对它们实施反向工程来发现现有依赖关系。

> [!NOTE]
> 无法为某些种类的项目对依赖关系进行反向工程处理。 例如，对于链接到文本文件的层，将不会对源自或指向该层的依赖关系进行反向工程处理。 若要查看哪些项目具有可进行反向工程处理的依赖项，请右键单击一个或多个层，然后单击 " **查看链接**"。 在 " **层资源管理器**" 中，检查 " **支持验证** " 列。 对于此列显示为 **False** 的项目，不会对依赖关系进行反向工程处理。

### <a name="to-reverse-engineer-existing-dependencies-between-layers"></a>为对层之间的现有依赖关系进行反向工程

选择一个或多个层，右键单击所选的层，然后单击 " **生成依赖项**"。

通常，您会看到一些不应存在的依赖关系。 可以编辑这些依赖关系，使它们与预期的设计对齐。

## <a name="edit-layers-and-dependencies-to-show-the-intended-design"></a><a name="EditArchitecture"></a> 编辑层和依赖项以显示预期的设计

若要描述你计划对系统或预期的体系结构进行的更改，请使用以下步骤编辑依赖关系图。 你还可以考虑进行一些重构的更改，以提高代码的结构，然后再扩展。 请参阅 [改进代码的结构](#Improving)。

|**To**|**执行这些步骤**|
|-|-|
|删除不应存在的依赖项|单击 "依赖关系"，然后按 " **删除**"。|
|更改或限制依赖项的方向|设置其 **方向** 属性。|
|创建新的依赖项|使用 **依赖** 关系和 **双向依赖关系** 工具。<br /><br /> 若要绘制多个依赖关系，请双击该工具。 完成后，请单击 **指针** 工具或按 **ESC** 键。|
|指定与层关联的项目不能依赖于指定的命名空间|在层的 " **禁止的命名空间依赖项** " 属性中键入命名空间。 使用分号 (**;**) 分隔命名空间。|
|指定与层关联的项目必须不属于指定的命名空间|在层的 " **禁止的命名空间** " 属性中键入命名空间。 使用分号 (**;**) 分隔命名空间。|
|指定与层关联的项目必须属于某个指定的命名空间|在层的 " **必需的命名空间** " 属性中键入命名空间。 使用分号 (**;**) 分隔命名空间。|

### <a name="improving-the-structure-of-the-code"></a><a name="Improving"></a> 改进代码的结构

重构更改的改进不会影响应用程序的行为，但有助于使代码在将来更易于更改和扩展。 结构良好的代码具有易于抽象到依赖项关系图的设计。

例如，如果你为代码中的每个命名空间创建图层，然后进行反向工程处理依赖关系，各层之间应该有单向依赖项的最小集。 如果您使用类或方法创建更详细的关系图作为您的层，则结果也将具有相同的特征。

如果不是这种情况，代码在其整个生命周期中将更难更改，并且不太适合使用依赖项关系图进行验证。

## <a name="design-new-areas-of-your-application"></a><a name="NewAreas"></a> 设计应用程序的新区域

当你启动开发新项目或新项目中的新区域时，你可以绘制层和依赖项，以帮助你在开始开发代码之前标识主要组件。

- **在依赖项关系图中** 显示可识别的体系结构模式（如果可能）。 例如，描述桌面应用程序的依赖项关系图可能包括表示、域逻辑和数据存储等层。 涵盖应用程序中单个特征的依赖项关系图可能包含"模型"、"视图"和"控制器"等层。 有关此类模式的信息，请参阅 [模式&做法：应用程序体系结构](https://archive.codeplex.com/?p=apparch)。

- **为每个层（如命名空间** 、类或组件）创建代码项目。 这样，就更容易跟踪代码，并把代码项目链接到层。 当你创建每个项目时，将其链接到相应的层。

- **不需要将大多数** 类和其他项目链接到层，因为它们位于较大的项目（例如已链接到层的命名空间）中。

- **为新功能创建新关系图**。 通常，有一个或多个描述整个应用程序的依赖项关系图。 如果您正在设计应用程序的新功能，请勿添加或更改现有的关系图。 相反，创建你自己的关系图来反映代码的新部分。 新关系图中的图层可能包括演示文稿、域逻辑和新功能的数据库层。

     在生成应用程序时，将同时对整体的关系图和更详细的功能关系图验证你的代码。

## <a name="edit-the-layout-for-presentation-and-discussion"></a><a name="EditLayout"></a> 编辑布局进行演示和讨论

为了帮助你识别层和依赖项或与团队成员对其进行讨论，你可以按以下方式编辑关系图的外观和布局：

- 更改图层的大小、 形状和位置。

- 更改层的颜色和依赖项。

  - 选择一个或多个层或依赖项，右键单击，然后单击"属性 **"。** 在" **属性"** 窗口中，编辑 **Color** 属性。

## <a name="validate-the-code-against-the-diagram"></a><a name="Validate"></a> 根据关系图验证代码

编辑关系图后，你可随时手动或每次生成时根据代码对其进行验证。

请参阅：

- [使用依赖项关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)

- [在生成过程中包括层验证](#BuildValidation)

## <a name="update-the-code-to-conform-to-the-new-architecture"></a><a name="UpdateCode"></a> 更新代码以符合新体系结构

通常，第一次根据更新的依赖项关系图验证代码时，会显示错误。 这些错误可能有几个原因：

- 将项目指派给了错误的层。 在这种情况下，请移动项目。

- 项目（例如类）以与你的体系结构相冲突的方式使用了其他类。 在这种情况下，请重构代码以移除依赖关系。

若要解决这些错误，请更新代码，直至验证过程中不出现其他错误为止。 这通常是一个迭代过程。 有关这些错误的详细信息，请参阅 [使用依赖项关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)。

> [!NOTE]
> 开发或重构代码时，可能有要链接到依赖项关系图的新项目。 但是，这可能不是必要的，例如，当你的层表示现有命名空间时，而且新代码只是向这些命名空间中添加更多的材料。

在开发过程中，你可能需要在验证期间禁止显示报告的某些冲突。 例如，你可能希望禁止显示你已解决或与特定情形不相关的错误。 禁止显示错误时，最佳做法是在 Team Foundation 中记录工作项。 若要执行此任务，请参阅 [使用依赖项关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)。

## <a name="include-layer-validation-in-the-build-process"></a><a name="BuildValidation"></a> 在生成过程中包括层验证

若要确保代码中的未来更改符合依赖项关系图，请对解决方案的标准生成过程包括层验证。 每当其他团队成员生成解决方案时，代码中的依赖项和依赖项关系图之间的任何差异都将报告为生成错误。 有关在生成过程中包括层验证的信息，请参阅 [使用依赖项关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)。

## <a name="see-also"></a>另请参阅

- [依赖项关系图：参考](../modeling/layer-diagrams-reference.md)
- [从代码创建依赖项关系图](../modeling/create-layer-diagrams-from-your-code.md)
