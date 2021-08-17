---
title: 自定义 T4 文本转换
description: 了解如何通过自定义文本模板指令处理器或文本模板宿主来扩展默认模板转换过程。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, API
- text templates, custom hosts
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 4549fbcd8f342816cec490ac6b461d3448f8827e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122027755"
---
# <a name="customize-t4-text-transformation"></a>自定义 T4 文本转换

文本模板是一项Visual Studio，用于通过转换过程生成程序代码或其他文本文件。 使用 [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] ，可以通过自定义文本模板指令处理器或文本模板宿主来扩展默认模板转换过程。

## <a name="in-this-section"></a>本节内容

 [文本模板转换过程](../modeling/the-text-template-transformation-process.md) 描述文本转换的工作原理，并说明模板主机和指令处理器的角色。

 [创建自定义 T4 文本模板指令处理器](../modeling/creating-custom-t4-text-template-directive-processors.md) 指令处理器处理模板中的指令，例如，它在模板编译期间运行， `<#@template#>.` 并可以加载程序集和其他资源。 它还可以插入将运行时加载资源的代码。 通过定义自己的指令处理器，可以降低模板的复杂性。

 [在 VS 扩展中调用文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)如果要编写一个Visual Studio（如菜单命令或事件处理程序）的扩展，则扩展可以使用文本模板化服务来转换任何文本模板。 可以使用 Session 对象将参数数据传递到模板中，然后使用 指令从模板内获取 `<#@parameter#>` 值。

 [使用自定义主机处理文本模板](../modeling/processing-text-templates-by-using-a-custom-host.md) 执行文本模板的代码时，主机提供对外部文件和应用程序状态的访问权限。 例如，在 Visual Studio 中运行文本转换的主机可以提供对 **解决方案资源管理器** 的访问权限。 它还在错误消息窗口中显示错误。 如果要在不同的上下文中运行文本转换，可以定义自己的主机，以访问该上下文中可用的服务。

 如果要编写一个Visual Studio，请考虑使用现有的文本转换服务，而不是编写自己的主机。 有关详细信息，请参阅调用 [VS 扩展中的文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)。

## <a name="reference"></a>参考

- [编写 T4 文本模板](../modeling/writing-a-t4-text-template.md) 提供文本模板指令和控制块的语法。
