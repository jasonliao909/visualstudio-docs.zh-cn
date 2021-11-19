---
title: Visual Studio 2017 中用于设计的新增功能
description: 了解 Visual Studio 2017 中提供的代码设计新功能，例如实时依赖项验证。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio], architecture and modeling
- architecture [Visual Studio], modeling
- modeling software [Visual Studio], What's New
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: 5fd93098ce569247774b6af5828b7696201b8835
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665486"
---
# <a name="whats-new-for-design-in-visual-studio-2017"></a>Visual Studio 2017 中用于设计的新增功能

## <a name="live-dependency-validation"></a>实时依赖项验证

删除不需要的依赖项是管理技术债务的重要组成部分。 Visual Studio 对依赖项进行实时验证，包括有关问题的精确信息（例如问题所在的位置）。 实时依赖项验证充分利用了错误列表和编辑器中的新功能。

![实时依赖项验证的实际运用](media/dep-validation-whatsnew-01.png)

创作体验已更改，使依赖项验证更易于发现和访问。 术语已从“层关系图”更改为“依赖项关系图”。

“体系结构”菜单现在包含一个命令，用于直接创建依赖项关系图：

![“体系结构”菜单上的实时依赖项项](media/dep-validation-whatsnew-02.png)

层属性名称和说明已更改，使其更有意义：

![实时依赖项更新的属性名称](media/dep-validation-whatsnew-03.png)

每次保存关系图时，都会立即看到更改对解决方案中当前代码的分析结果产生的影响。 不必等到“验证依赖项”命令完成。

有关更多详细信息，请参阅[这篇博客文章](https://devblogs.microsoft.com/devops/live-architecture-dependency-validation-in-visual-studio-15-preview-5/)。

## <a name="uml-designers-have-been-removed"></a>删除了 UML 设计器

已从 Visual Studio 中删除 UML 设计器。

* UML 关系图现在显示为 XML 文件
* UML 模型资源管理器不再存在
* 建模项目引用不再用于依赖项验证
* 不再显示解决方案资源管理器中的“层引用”节点
* 不再使用依赖项（层）关系图上的“验证”生成操作 - 生成任务已删除
* 会维护项目结构以在版本之间往返
* 你仍然可以 XML 格式打开、创建、编辑和保存依赖项（层）关系图
* 无法在设计图面上访问链接到依赖项（层）关系图的 TFS 工作项
* 不再支持 DSL 或层的后退链接
* 不再支持建模 SDK 中的 UML 扩展性

可通过[代码图](map-dependencies-across-your-solutions.md)来支持可视化 .NET 和 C++ 代码的体系结构。

如果你是 UML 设计器的重要用户，你可继续使用 Visual Studio 2015 或更低版本，同时决定满足 UML 需求的备用工具。

有关更多详细信息，请参阅[这篇博客文章](https://devblogs.microsoft.com/devops/uml-designers-have-been-removed-layer-designer-now-supports-live-architectural-analysis/)。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="edition-support-for-architecture-and-modeling-tools"></a><a name="VersionSupport" />对体系结构和建模工具的版本支持

Visual Studio 有多个版本。 并非所有版本支持体系结构和建模工具。 下表显示每个工具的可用性。

|**功能**|**Enterprise Edition**|**Professional Edition**|**Community Edition**|
|-|-|-|-|
|**代码图**|是|仅支持读取代码图、筛选代码图、添加新的泛型节点以及从所选内容创建新的定向关系图。|-|
|**依赖项关系图**|是|仅支持读取依赖关系图。|仅支持读取依赖关系图。|
|定向图（DGML 图）|是|是|是|
|**代码克隆**|是|-|-|
