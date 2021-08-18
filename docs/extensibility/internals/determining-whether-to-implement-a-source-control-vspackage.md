---
title: 何时实现源代码管理 VSPackage
description: 了解可用于扩展源代码管理解决方案的源代码管理插件和源代码管理 VSPackage Visual Studio选项。
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
ms.openlocfilehash: 5e16803a570c845e9283debcfb9e8d388b1cdd20
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122124654"
---
# <a name="determine-whether-to-implement-a-source-control-vspackage"></a>确定是否实现源代码管理 VSPackage

本部分详细介绍了用于扩展源代码管理解决方案的源代码管理插件和源代码管理 VSPackage 选项，并提供了有关选择合适的集成路径的广泛准则。

## <a name="small-source-control-solution-with-limited-resources"></a>资源有限的小型源代码管理解决方案

 如果资源有限，并且无法承担编写源代码管理包的开销，可以创建基于源代码管理插件 API 的插件。这样，就可以与源代码管理包并行工作，并可以按需在源代码管理插件和包之间切换。 有关详细信息，请参阅注册 [和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)。

## <a name="large-source-control-solution-with-a-rich-feature-set"></a>具有丰富功能集的大型源代码管理解决方案

 如果要实现提供使用源代码管理插件 API 无法充分捕获的丰富源代码管理模型的源代码管理解决方案，可以考虑将源代码管理包作为集成路径。 这尤其适用于希望替换源代码管理适配器包 (该包与源代码管理插件通信，并提供具有你自己的基本源代码管理 UI) 以便可以自定义方式处理源代码管理事件的情况。 如果已有一个满意源代码管理 UI，并且想要在 中保留该体验，则源代码管理包选项允许你 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 这样做。 源代码管理包不是泛型包，仅用于 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE。

 如果要实现对源代码管理逻辑和 UI 提供灵活性和更丰富的控制的源代码管理解决方案，可能首选源代码管理包集成路由。 方法：

1. 注册自己的源代码管理 VSPackage (注册 [和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)) 。

2. 将默认源代码管理 UI 替换为自定义 UI (请参阅 [自定义用户界面](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)) 。

3. 指定使用字形并处理解决方案资源管理器事件， (字[形控件) 。](../../extensibility/internals/glyph-control-source-control-vspackage.md)

4. 处理查询编辑和查询保存事件 (查询[编辑查询保存) 。](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)

## <a name="see-also"></a>请参阅

- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
