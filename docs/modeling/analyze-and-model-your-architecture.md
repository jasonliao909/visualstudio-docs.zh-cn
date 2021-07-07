---
title: 体系结构分析和建模工具
description: 设计应用并建模，确保应用符合体系结构要求。
ms.custom: SEO-VS-2020
ms.date: 06/04/2021
ms.topic: overview
helpviewer_keywords:
- diagrams - modeling
- architecture
- code visualization
- application design
- code exploration
- modeling
- application architecture
- architecture [Visual Studio ALM], modeling
- application modeling
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 542b74e7d3bb73847303fa4215651eea7e110e91
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384871"
---
# <a name="analyze-and-model-your-architecture"></a>对体系结构进行分析和建模

通过使用 Visual Studio 体系结构和建模工具对应用进行设计和建模，确保应用满足体系结构要求。

1. 通过使用代码图和依赖关系图来[可视化代码](visualize-code.md)结构，从而更好地了解现有程序。
    - 通过创建代码图查看代码的组织和关系。 
    - 可视化程序集、命名空间、类、方法等之间的依赖关系。
    - 通过创建依赖项关系图以验证代码来查找代码及其设计之间的冲突。
    - 通过[从代码创建类图](../ide/class-designer/designing-and-viewing-classes-and-types.md)来查看特定项目的类结构和成员。
    - [使用 T4 模板生成文本](../modeling/code-generation-and-t4-text-templates.md)，并在模板中使用文本块和控制逻辑生成基于文本的文件。 
    
1. 让团队了解尊重体系结构依赖项的必要性。

1. 作为开发过程的一部分，可以跨整个应用程序生命周期创建不同详细信息级别的模型。

请参阅[场景：通过可视化和建模来更改设计](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)。

## <a name="code-maps"></a>代码图

代码图是一种模型，可帮助你查看代码中的组织和关系。

使用代码图检查程序代码，以便可以更好地了解其结构及其依赖关系以及如何对其进行更新，并估计建议更改的成本。

了解详细信息：
- [安装体系结构代码工具](install-architecture-tools.md)
- [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)
- [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)
- [使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)

## <a name="dependency-diagrams"></a>依赖项关系图

依赖项关系图可将应用程序的结构定义为一组带有显式依赖项的层或块。 实时验证可显示代码中依赖项与依赖项关系图中所述依赖项之间的冲突。

使用依赖关系图以： 
- 通过在应用程序生命周期中进行大量更改来稳定其结构。
- 在签入对代码的更改之前发现无意的依赖项冲突。

了解详细信息：
- [安装体系结构代码工具](install-architecture-tools.md)
- [从代码创建依赖项关系图](../modeling/create-layer-diagrams-from-your-code.md)
- [依赖项关系图：参考](../modeling/layer-diagrams-reference.md)
- [使用依赖项关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)

## <a name="domain-specific-language-dsl-models"></a>域特定语言 (DSL) 模型

DSL 是为特定目的而设计的一种表示法。 在 Visual Studio 中，通常为图形。

使用域特定语言以： 
- 生成或配置应用程序的各部分。 若要开发表示法和工具，则需要进行工作。 其产生的结果，与 UML 自定义相比，会更好地适应你的域。
- 适用于大型项目或在某些产品系列中（其中 DSL 及其工具的开发投资会通过该产品在多个项目中的使用而回收）。

了解详细信息：
- [Visual Studio 的建模 SDK - 特定于域的语言](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)


## <a name="edition-support-for-architecture-and-modeling-tools"></a><a name="VersionSupport" />对体系结构和建模工具的版本支持

Visual Studio 有多个版本。 并非所有版本支持体系结构和建模工具。 下表显示每个工具的可用性。

|**功能**|**Enterprise Edition**|**Professional Edition**|**Community Edition**|
|-|-|-|-|
|**代码图**|是|仅支持读取代码图、筛选代码图、添加新的泛型节点以及从所选内容创建新的定向关系图。|-|
|**依赖项关系图**|是|仅支持读取依赖关系图。|仅支持读取依赖关系图。|
|定向图（DGML 图）|是|是|是|
|**代码克隆**|是|-|-|
