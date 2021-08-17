---
title: Visual Studio 2017 中用于设计的新增功能
description: 了解 2017 年 1 月提供的代码设计的新功能，例如实时依赖项Visual Studio功能。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122055271"
---
# <a name="whats-new-for-design-in-visual-studio-2017"></a>Visual Studio 2017 中用于设计的新增功能

## <a name="live-dependency-validation"></a>实时依赖项验证

删除不需要的依赖项是管理技术债务的重要组成部分。 Visual Studio提供依赖项实时验证，包括有关问题（例如问题所在的位置）的精确信息。 实时依赖项验证充分利用了错误列表和编辑器中的新功能。

![实时依赖项验证操作](media/dep-validation-whatsnew-01.png)

创作体验已更改，使依赖项验证更易于发现和访问。 术语从"层关系图"更改为"依赖项关系图"。

" **体系结构** "菜单现在包含一个命令，用于直接创建依赖项关系图：

!["体系结构"菜单上的实时依赖项项](media/dep-validation-whatsnew-02.png)

更改了层属性名称和说明，使其更有意义：

![实时依赖项更新的属性名称](media/dep-validation-whatsnew-03.png)

每次保存关系图时，你会立即在解决方案中当前代码的分析结果中看到更改的影响。 不必等待 Validate **Dependencies** 命令完成。

有关更多详细信息，请参阅[这篇博客文章](https://devblogs.microsoft.com/devops/live-architecture-dependency-validation-in-visual-studio-15-preview-5/)。

## <a name="uml-designers-have-been-removed"></a>已删除 UML 设计器

UML 设计器已从 Visual Studio。

* UML 关系图现在呈现为 XML 文件
* UML 模型资源管理器不再存在
* 建模项目引用不再用于依赖项验证
* 不再显示解决方案资源管理器"层引用"节点
* 不再使用"依赖关系"层 (") "验证"生成操作 - 生成任务已删除
* 维护项目结构，以在版本之间往返
* 仍可以打开、创建、编辑依赖项并将其另存为 XML (层) 关系图
* 在设计图面上无法访问链接到 (层) 的 TFS 工作项
* 不再支持从 到 DSL 或层的后退链接
* 不再支持建模 SDK 中的 UML 扩展性

可以通过代码图 来支持可视化 .NET 和 C++ 代码 [的体系结构](map-dependencies-across-your-solutions.md)。

如果你是 UML 设计器的重要用户，可以继续使用 Visual Studio 2015 或更早版本，同时确定满足 UML 需求的备用工具。

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
