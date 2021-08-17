---
title: 可视化代码
description: 了解如何使用应用程序中的可视化和建模工具Visual Studio了解现有代码并描述应用程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- code, understanding
- code, visualizing
- code, exploring
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 50ccc16c6367d6e177d523e0480479d447cfc940937593a2b04829d03d94f758
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121443966"
---
# <a name="visualize-code"></a>可视化代码

你可以在 Visual Studio 中使用可视化和建模工具，以帮助你了解现有代码并描述你的应用程序。 这可以让你直观地了解更改可能对代码产生的影响，并帮助你评估更改导致的工作和风险。 例如：

- 了解代码的关系，可以用可视的方式映射这些关系。

- 若要描述系统的体系结构并保持代码与设计一致，请根据这些关系图创建依赖项关系图并验证代码。

- 若要描述类结构，请创建类关系图。

这些工具还可以帮助你更轻松地与参与项目的人员进行沟通。

要查看支持每个功能的 Visual Studio 版本，请参阅[体系结构和建模工具的版本支持](../modeling/analyze-and-model-your-architecture.md#VersionSupport)

## <a name="what-do-you-want-to-do"></a>你希望做什么？

|方案|项目|
|-|-|
|**了解代码及其关系：**<br /><br /> 特定代码段之间的代码图关系<br /><br /> 请参阅整个解决方案中的代码关系概述。|- [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)<br />- [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)<br />- [使用代码图分析器查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)<br />- [调试时映射调用堆栈上的方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)|
|**了解类结构：**<br /><br /> 通过从代码创建类关系图，在项目中查看类的结构。|[如何：向项目添加类图（类设计器）](../ide/class-designer/how-to-add-class-diagrams-to-projects.md)|
|**描述高级系统设计，并对此设计进行代码验证：**<br /><br /> 通过创建依赖项关系图描述高级系统设计及其预期依赖项。 对此设计进行代码验证，以确保代码中的依赖项与设计保持一致。|- [从代码创建依赖项关系图](../modeling/create-layer-diagrams-from-your-code.md)<br />- [依赖项关系图：参考](../modeling/layer-diagrams-reference.md)<br />- [依赖项关系图：指南](../modeling/layer-diagrams-guidelines.md)<br />- [使用依赖项关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)|

## <a name="see-also"></a>请参阅

- [安装体系结构代码工具](install-architecture-tools.md)
- [方案：使用可视化和建模更改设计](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)
- [分析和模型体系结构](../modeling/analyze-and-model-your-architecture.md)
- [应用体系结构建模](../modeling/model-your-app-s-architecture.md)
- [在你的开发过程中使用模型](../modeling/use-models-in-your-development-process.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
