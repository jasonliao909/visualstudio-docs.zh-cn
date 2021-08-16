---
title: 何时实现源代码管理 VSPackage
description: 了解可用于扩展 Visual Studio 源代码管理解决方案的源代码管理插件和源代码管理 vspackage 的选项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, about source control packages
ms.assetid: 60b3326e-e7e2-4729-95fc-b682e7ad5c99
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 3a833abb38b42ff136532159996b438bf7466a4d6fb3eec10dcdab14eda3e8c9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359524"
---
# <a name="determine-whether-to-implement-a-source-control-vspackage"></a>确定是否实现源代码管理 VSPackage

本部分然后详细阐述源代码管理插件和源代码管理 Vspackage 的选择，用于扩展源代码管理解决方案，并提供有关选择合适的集成路径的广义指导。

## <a name="small-source-control-solution-with-limited-resources"></a>资源有限的小型源代码管理解决方案

 如果资源有限，而且不能承受写入源代码管理包的开销，则可以创建基于源代码管理插件的插件。这样做使您可以与源代码管理包并行工作，并且您可以根据需要在源代码管理插件和包之间进行切换。 有关详细信息，请参阅 [注册和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)。

## <a name="large-source-control-solution-with-a-rich-feature-set"></a>具有丰富功能集的大型源代码管理解决方案

 如果要实现一个源代码管理解决方案，该解决方案提供一个使用源代码管理插件 API 未充分捕获的丰富源代码管理模型，则可以将源代码管理包视为集成路径。 这尤其适用于替换源代码管理适配器包 (它与源代码管理插件通信，并提供自己的基本源代码管理 UI) ，以便能够以自定义方式处理源代码管理事件。 如果你已经有一个令人满意的源代码管理 UI，并且想要在中保留该体验 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，则源代码管理包选项仅允许你这样做。 源代码管理包不是泛型包，而是专门为与 IDE 一起使用而设计的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

 如果要实现一个源代码管理解决方案，该解决方案可为源代码管理逻辑和 UI 提供灵活性和更丰富的控制，您可能更倾向于源代码管理包集成路由。 方法：

1. 注册自己的源代码管理 VSPackage (参阅 [注册和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)) 。

2. 将默认源代码管理 UI 替换为自定义 UI (参阅 [自定义用户界面](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)) 。

3. 指定要使用的标志符号并处理解决方案资源管理器标志符号事件 (请参阅 [标志符号控件](../../extensibility/internals/glyph-control-source-control-vspackage.md)) 。

4. 处理查询编辑和查询保存事件 (参阅 [查询编辑查询保存](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)) 。

## <a name="see-also"></a>另请参阅

- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
