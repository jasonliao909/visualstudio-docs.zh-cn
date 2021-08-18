---
title: 何时创建Project类型|Microsoft Docs
description: 了解如何确定为用户自定义项目类型Visual Studio项目类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, conditions for creating
ms.assetid: 26adc860-ee4a-4f5c-95e1-e41b207dd7e6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c4974d4838955baecd0d0ebcaddecf13329adc14
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110314"
---
# <a name="when-to-create-project-types"></a>何时创建项目类型
创建新项目类型为用户自定义 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 提供了基础。 但是，并非所有自定义项都需要创建新 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目类型。 以下指南应有助于确定方案是否需要新的项目类型。

## <a name="create-a-new-project-type"></a>创建新的Project类型
 如果要自定义 以下列一种或多种方式操作，则必须创建 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目类型：

- 参与生成、部署、配置和源代码管理。

- 提供调试支持。

- 在 中显示 **解决方案资源管理器。**

- 使用"**打开Project"****或"Project"** 对话框。

- 支持项目嵌套。

## <a name="extend-an-existing-project-type"></a>扩展现有Project类型
 你可能想要创建一个可以按以下方式使用的新项目类型来修改或扩展现有项目类型的行为，例如，修改项目的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 生成 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 过程：

- 将多个文件作为单个单元使用。

- 将单个文件显示为子项的层次结构。

- 在编辑器周围显示命令上下文。

- 显示编辑器的服务上下文。

## <a name="use-an-existing-project-type"></a>使用现有Project类型
 有时不需要创建新项目。 下表显示了不需要创建项目类型的任务。

|任务|说明|
|----------|-----------------|
|处理命令|任何 VSPackage 都可以处理命令。|
|生成编辑器|可以注册自定义编辑器。 有关详细信息，请参阅文档Windows[编辑器](/previous-versions/bb165691(v=vs.100))。|
|拥有窗口|可以创建工具和文档窗口，而无需添加新项目类型。|
|公开属性属性窗口|所有对象都可以公开属性。|

## <a name="create-a-project-subtype"></a>创建Project子类型
 可以使用项目子类型来扩展托管项目类型，而无需创建新的项目类型。 Project子类型使用 COM 聚合来扩展用 Microsoft 或 编写的托管 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 。 借助 COM 聚合，可以重复使用大部分托管项目系统实现，并且仍可通过聚合和使用支持接口来自定义特定方案。 有关项目子类型详细信息，请参阅 Project[子类型](../../extensibility/internals/project-subtypes.md)。

## <a name="see-also"></a>请参阅
- [文档Windows编辑器](/previous-versions/bb165691(v=vs.100))
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)