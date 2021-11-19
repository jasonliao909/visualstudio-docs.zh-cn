---
title: 在你的开发过程中使用模型
description: 了解在 Visual Studio 中，你可以使用模型帮助你理解和更改系统、应用程序或组件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- UML, using models
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 910aa4d25325ac6498e941bbba3a1a6d7ee2f957
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663854"
---
# <a name="use-models-in-your-development-process"></a>在你的开发过程中使用模型

在 Visual Studio 中，你可以使用模型帮助你理解和更改系统、应用程序或组件。 模型能帮助你可视化系统工作的环境、阐明用户需求、定义你系统的体系结构、分析代码并确保你的代码符合要求。 请参阅[第 9 频道视频：通过建模改善体系结构](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Improving-architecture-through-modeling)。

若要查看支持每种类型的模型的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/analyze-and-model-your-architecture.md#VersionSupport)。

模型可以通过几种方式帮助你：

- 绘制建模图可帮助明确需求、体系结构和高级设计中所涉及的概念。 有关详细信息，请参阅[用户需求建模](../modeling/model-user-requirements.md)。

- 使用模型可帮助你揭示需求中的不一致性。

- 使用模型通信可帮助你沟通重要概念时比使用自然语言更明确。 有关详细信息，请参阅[应用的体系结构建模](../modeling/model-your-app-s-architecture.md)。

- 有时可使用模型生成代码或其他项目（如数据库架构或文档）。 例如，Visual Studio 建模组件是从模型生成的。 有关详细信息，请参阅[从模型中生成并配置你的应用](../modeling/generate-and-configure-your-app-from-models.md)。

你可以在从极端敏捷到崇礼的各种流程中使用模型。

## <a name="use-models-to-reduce-ambiguity"></a>使用模型减少多义性

建模语言比自然语言更明确，它用来表达软件开发期间通常需要的想法。

如果你的项目有一个小的团队遵循敏捷做法，则可以使用模型来帮助你阐明用户情景。 在与客户讨论其需求时，与编写图文场或原型代码相比，创建一个模型可以在更广泛的产品领域更快地生成有用的问题。

如果你的项目很大，并且团队遍布全球各个位置，与使用纯文本相比，你可以使用模型来帮助更有效地沟通需求和体系结构。

在这两种情况下，创建模型几乎总是会导致不一致和多义性的显著降低。 不同的利益干系人经常会对系统工作的业务领域有不同的理解，并且不同的开发人员经常会对系统的工作方式有不同的理解。 通常使用模型作为讨论的焦点来揭示这些不同之处。 有关如何使用模型来减少不一致的详细信息，请参阅[用户需求建模](../modeling/model-user-requirements.md)。

## <a name="use-models-with-other-artifacts"></a>对其他项目使用模型

一个模型本身并不是需求规范或体系结构。 它是一个工具，用于更清楚地表达的事物某些方面，但不是所有软件设计过程中所需的全部概念都可以表达出来。 因此，模型应当与其他通信方法一起使用，如 OneNote 页面或段落、Microsoft Office 文档、Team Foundation 中的工作项，或项目文件室墙上的粘滞便笺。 除了最后一项，所有这些对象类型都可以链接到模型的元素部分。

通常与模型一起使用的其他方面的规范包括以下内容。 具体取决于项目的大小和样式，你可以使用这些方面中的几个，也可以根本不适用它们：

- 用户情景。 用户情景是与用户和其他利益干系人一起讨论的系统行为方面的简短描述，该行为将在项目的迭代之一中出现。 典型的用户情景以“客户将能够...”开始。用户情景可能会引入一组用例，也可以定义先前已开发的用例的扩展。 定义或扩展用例有助于使用户情景更清晰。

- 更改请求。 更正式项目中的更改请求非常类似于敏捷项目中的用户情景。 敏捷方法会将所有需求视为对之前迭代中所开发内容进行的更改。

- 用例描述。 用例表示用户与系统交互以达到特定目标的一种方法。 完整的描述包括目标、事件的主要和备选序列以及异常结果。 用例图可帮助汇总并提供用例的概述。

- 方案。 方案是事件序列的非常详细的说明，这些事件显示系统、用户及其他系统如何协同工作以向利益干系人提供价值。 它可能会采用以下形式：用户界面的幻灯片放映或用户界面的原型。 它可以描述一个用例或一个用例序列。

- 词汇表。 项目的需求词汇表描述了客户用于讨论其领域的单词。 用户界面和需求模型也应使用这些术语。 类图可以帮助阐明其中大多数术语之间的关系。 创建关系图和词汇表不仅可减少用户和开发人员之间的误解，而且几乎总是会揭露不同的业务利益干系人之间的误解。

- 业务规则。 许多业务规则都能表示为需求类模型中关联和特性上的固定约束，也可表示为序列图上的约束。

- 高级设计。 描述主要部件以及它们如何组合在一起。 组件、序列和界面图都是高级设计的主要部件。

- 设计模式。 描述系统的不同部件之间共享的设计规则。

- 测试规范。 测试脚本和测试代码的设计可以更好地利用活动和序列图来描述测试步骤的序列。 系统测试应按照需求模型来表达，这样在需求更改时它们也能轻松更改。

- 项目计划。 项目计划或积压工作定义何时发送每个功能。 你可以通过声明它实现或扩展了什么用例和业务规则来定义每个功能。 你可以直接在计划中引用用例和业务规则，也可以在一个单独的文档中定义一组功能并在计划中使用该功能标题。

## <a name="use-models-in-iteration-planning"></a>在迭代计划中使用模型

虽然所有项目的大小和组织不同，典型的项目计划为二到六周之间的一系列迭代。 重要的是计划足够的迭代以允许来自早期迭代的反馈能用于调整后续迭代的范围和计划。

你可能会发现以下建议可以帮助实现在迭代项目中建模的好处。

### <a name="sharpen-focus-as-each-iteration-approaches"></a>随着每次迭代临近逐渐聚焦

随着每次迭代的临近，使用模型来帮助定义要在迭代末尾传递的内容。

- 不要在早期迭代中对所有内容详细建模。 第一次迭代中，在用户术语表中为主要项目创建一个类图，绘制主要用例的关系图，并绘制主要组件的关系图。 不要详细地描述这些关系图，因为项目中的详细信息在以后将会更改。 使用此模型中定义的术语来创建功能或主要用户情景的列表。 将功能分配到迭代，以便大约平衡整个项目的估计工作负荷。 这些分配之后将在项目中作出更改。

- 尝试在早期迭代中实现所有最重要用例的简化版本。 在后续迭代中扩展这些用例。 此方法有助于降低太晚发现项目中需求或体系结构的缺陷而无法补救的风险。

- 每次迭代接近结束时，举办一次需求研讨会，以详细定义将在下个迭代中开发的需求或用户情景。 邀请能够确定优先级的用户和业务利益干系人，以及开发人员和系统测试员。 允许用三个小时为一个 2 周的迭代定义需求。

- 该研讨会的目标是使每个人就下个迭代结束时将完成的内容达成一致。 将模型用作一种工具来帮助阐明需求。 该研讨会的输出是一个迭代积压工作：即 Team Foundation 中的开发任务列表和 [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] 中的测试套件。

- 在需求研讨会中，仅在你需要为开发任务确定估计值的范围内讨论设计。 否则，请保持讨论用户可以直接体验的系统行为。 保持需求模型与体系结构模型分开。

- 从你这里获取一些指导后，非技术性的利益干系人对理解 UML 关系图通常不会有问题。

### <a name="link-model-to-work-items"></a>将模型链接到工作项

需求研讨会结束后，请详细说明需求模型的的详细信息，并将模型链接到开发任务。 你可以通过将 Team Foundation 中的工作项链接到模型中的元素来实现此操作。

你可以将任意元素链接到工作项，但最有用的元素如下所示：

- 描述业务规则或服务质量要求的注释。 有关详细信息，请参阅[用户需求建模](../modeling/model-user-requirements.md)。

### <a name="link-model-to-tests"></a>将模型链接到测试

使用需求模型来指导验收测试的设计。 在开发工作进行的同时创建这些测试。

若要了解有关此技术的详细信息，请参阅[从模型开发测试](../modeling/develop-tests-from-a-model.md)。

### <a name="estimate-remaining-work"></a>估计剩余工作

需求模型可以帮助根据每个迭代的大小估计项目的总大小。 评估用例和类的数量和复杂性可以帮助你估计将需要的开发工作。 完成前几个迭代后，对已涵盖需求以及仍将涵盖的需求进行比较可以估算出项目剩余部分的成本和范围。

每个迭代接近结束时，请查看对未来迭代的需求分配。 它可以用于将每个迭代结束时软件的状态表示为用例图中的子系统。 在讨论中，可以将用例和用例扩展从这些子系统中的其中一个移到另一个子系统。

## <a name="levels-of-abstraction"></a>抽象级别

模型具有与软件相关的一系列抽象。 最具体的模型直接表示程序代码，而最抽象的模型表示可能会或可能不会在代码中表示的业务概念。

可以通过多种类型的关系图中查看模型。 有关模型和关系图的信息，请参阅[为你的应用创建模型](../modeling/create-models-for-your-app.md)。

不同类型的关系图可用于描述不同抽象级别的设计。 许多关系图类型可用于多个级别。 此表显示可以如何使用每种类型的关系图。

|设计级别|关系图类型|
|-|-|
|业务流程<br /><br /> 了解将在其中使用你的系统的上下文有助于你了解用户对系统的需求。|- 概念类图描述了业务流程中使用的业务概念。|
|用户需求<br /><br /> 用户对系统的需求的定义。|- 可以在单独的文档中描述业务规则和服务质量要求。|
|高级设计<br /><br /> 系统的整体结构：主要组件以及它们如何结合在一起。|- 依赖项关系图描述了系统如何组织成相互依赖的部件。 你可以验证程序代码对依赖项关系图的有效性，以确保它符合体系结构。|
|代码分析<br /><br /> 可以从代码生成关系图。|- 依赖项关系图显示了各个类之间的依赖项。 可以验证更新后的代码对依赖项关系图的有效性。<br />- 类图显示了代码中的类。|

## <a name="external-resources"></a>外部资源

|**类别**|**链接**|
|-|-|
|**视频**|![链接到视频](../data-tools/media/playvideo.gif) [MSDN 如何操作视频：如何创建和使用 UML 模型和关系图 (Visual Studio 2010 Ultimate)](/previous-versions/visualstudio/visual-studio-2010/dd831853(v=vs.100))<br /><br /> ![链接到视频](../data-tools/media/playvideo.gif) [第 9 频道：使用 Visual Studio 2010 的 UML](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-1-brainstorming-a-project)<br /><br /> ![链接到视频](../data-tools/media/playvideo.gif) [MSDN 如何操作系列：UML 工具和扩展性 (Visual Studio 2010 Ultimate)](/previous-versions/visualstudio/visual-studio-2010/dd831853(v=vs.100))|
|**论坛**|- [Visual Studio 可视化和建模工具](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />- [Visual Studio 可视化和建模 SDK（DSL 工具）](https://social.msdn.microsoft.com/Forums/home?forum=dslvsarchx)|
|**Blogs**|[Microsoft DevOps](https://devblogs.microsoft.com/devops/)|
|**技术文章和日志**|[MSDN 体系结构中心](/previous-versions/dn630665(v=msdn.10))|

## <a name="see-also"></a>另请参阅

- [在敏捷开发中使用模型](/previous-versions/ff398061(v=vs.140))
- [为你的应用程序创建模型](../modeling/create-models-for-your-app.md)
- [建立用户需求模型](../modeling/model-user-requirements.md)
- [应用体系结构建模](../modeling/model-your-app-s-architecture.md)
- [基于模型开发测试](../modeling/develop-tests-from-a-model.md)
- [安排你的建模解决方案](../modeling/structure-your-modeling-solution.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]