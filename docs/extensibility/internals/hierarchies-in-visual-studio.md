---
title: 层次结构Visual Studio |Microsoft Docs
description: 了解包含项目项及其关联Visual Studio IDE Visual Studio (IDE) 中的项目层次结构。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- hierarchies, Visual Studio IDE
- IDE, hierarchies
ms.assetid: 0a029a7c-79fd-4b54-bd63-bd0f21aa8d30
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 3d8058091742f8e0f9ed3e51ebf0d046ee1524e5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664373"
---
# <a name="hierarchies-in-visual-studio"></a>Visual Studio 中的层次结构
IDE [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (集成) 将项目显示为 *层次结构*。 在 IDE 中，层次结构是节点树，其中每个节点都有一组关联的属性。 *项目层次结构是* 一个容器，用于保存项目的项、项的关系以及项的关联属性和命令。

 在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中，使用层次结构接口 管理项目层次结构 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 。 接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 会将从项目项调用的命令重定向到相应的层次结构窗口，而不是标准命令处理程序。

## <a name="project-hierarchies"></a>Project层次结构
 每个项目层次结构都包含可以查看和编辑的项。 这些项因项目类型而异。 例如，数据库项目可能包含存储过程、数据库视图和数据库表。 另一方面，编程语言项目可能包含位图和对话框的源文件和资源文件。 层次结构可以嵌套，这为你提供了一些创建项目层次结构时的灵活性。

 创建新项目类型时，项目类型控制可在其中编辑的完整项集。 但是，项目可以包含它们没有编辑支持的项。 例如，Visual C++项目可以包含 HTML 文件，即使Visual C++为 HTML 文件类型提供任何自定义编辑器。

 层次结构管理它们包含的项的持久性。 层次结构的实现必须控制影响层次结构中项持久性的任何特殊属性。 例如，如果项表示存储库中的对象而不是文件，则层次结构实现必须控制这些对象的持久性。 IDE 本身指示层次结构根据用户输入保存项，但 IDE 不控制保存这些项所需的任何操作。 相反，项目在控制中。

 当用户在编辑器中打开某个项时，将选择控制该项的层次结构，并变为活动层次结构。 所选层次结构确定可用于对项执行的命令集。 通过此方式跟踪用户焦点，层次结构可以反映用户的当前上下文。

## <a name="see-also"></a>另请参阅
- [项目类型](../../extensibility/internals/project-types.md)
- [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)
