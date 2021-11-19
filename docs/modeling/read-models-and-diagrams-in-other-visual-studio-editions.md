---
title: 在其他 Visual Studio 版本中读取模型和关系图
description: 了解在 Visual Studio 中读取模型和关系图，以及使用不支持创建模型的 Visual Studio 版本时的只读行为。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- models, versions of Visual Studio
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 4adcdb442e31a0de834a05a06ea96981b761ea73
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663908"
---
# <a name="read-models-and-diagrams-in-other-visual-studio-editions"></a>在其他 Visual Studio 版本中读取模型和关系图

如果你在一个不支持创建模型的 Visual Studio 中打开模型，该模型将以只读模式打开。 在此模式下，你可以更改的关系图的布局，但不能更改该模型。

若要查看哪些版本的 Visual Studio 支持创建模型，请参阅[体系结构和建模工具的版本支持](../modeling/analyze-and-model-your-architecture.md#VersionSupport)。

## <a name="obtaining-access-to-a-model-and-diagrams"></a>获取对某一模型和关系图的访问权限

若要读取依赖项关系图，必须首先使用 Visual Studio 打开建模项目，然后在该项目中打开关系图。

出于此原因，如果你想要读取依赖项关系图，则必须有权限访问创建它的建模项目。 可以通过从源代码管理来访问项目，也可以通过获取项目文件的副本来获得访问权限。

> [!NOTE]
> 这不适用于从代码生成的代码图和 .NET 类图。 这些关系图可以独立建模项目中查看。

若要读取依赖项关系图，你所需的最小文件集如下：

- 要读取的关系图的两个关系图文件，例如 MyDiagram.classdiagram 和 MyDiagram.classdiagram.layout。

    > [!NOTE]
    > 对于依赖项关系图，还应具有名为 MyDiagram.layerdiagram.suppressions 的文件。

- 建模项目文件 (MyModel.modelproj)

- 根模型文件 (ModelDefinition\MyModel.uml)

- 关系图中引用的任何包的包文件 (ModelDefinition\MyPackage.uml)

## <a name="changes-that-you-can-make-in-read-only-mode"></a>在只读模式下可执行的更改

如果你在一个不支持创建模型的 Visual Studio 中打开模型及其关系图，则你无法更改模型。 也就是说，你无法更改显示在关系图或模型资源管理器上的元素和关系。 但是，你可以对关系图的布局进行某些更改：

- 重新排列关系图上的形状和连接符。

- 展开和折叠形状

你可以保存这些更改。 如果要使所做的更改对其他用户可见，至少必须发送已更新的 .layout 文件。

## <a name="see-also"></a>另请参阅

- [依赖项关系图：参考](../modeling/layer-diagrams-reference.md)
- [为你的应用程序创建模型](../modeling/create-models-for-your-app.md)
