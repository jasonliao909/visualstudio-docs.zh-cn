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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602318"
---
# <a name="customize-t4-text-transformation"></a>自定义 T4 文本转换

文本模板是 Visual Studio 的一项功能，它允许您通过转换过程生成程序代码或其他文本文件。 使用 [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] ，你可以通过自定义文本模板指令处理器或文本模板宿主来扩展默认模板转换过程。

## <a name="in-this-section"></a>本节内容

 [文本模板转换过程](../modeling/the-text-template-transformation-process.md) 描述文本转换的工作方式，并解释模板主机和指令处理器的角色。

 [创建自定义 T4 文本模板指令处理器](../modeling/creating-custom-t4-text-template-directive-processors.md) 指令处理器处理模板中的指令，例如模板在 `<#@template#>.` 编译过程中运行，并且可以加载程序集和其他资源。 它还可插入将在运行时加载资源的代码。 通过定义自己的指令处理器，可以降低模板的复杂性。

 [在 VS 扩展中调用文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)如果要编写 Visual Studio 扩展（如菜单命令或事件处理程序），则扩展可以使用文本模板化服务来转换任何文本模板。 可以使用 Session 对象将参数数据传递到模板，并使用指令从模板内获取值 `<#@parameter#>` 。

 [使用自定义宿主处理文本模板](../modeling/processing-text-templates-by-using-a-custom-host.md) 当执行文本模板的代码时，主机提供对外部文件和应用程序状态的访问。 例如，在 Visual Studio 中运行文本转换的宿主可以提供对 **解决方案资源管理器** 的访问。 它还在错误消息窗口中显示错误。 如果要在不同的上下文中运行文本转换，可以定义自己的主机，以便提供对该上下文中可用服务的访问权限。

 如果要编写 Visual Studio 扩展，请考虑使用现有的文本转换服务，而不是编写自己的主机。 有关详细信息，请参阅 [在 VS 扩展中调用文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)。

## <a name="reference"></a>参考

- [编写 T4 文本模板](../modeling/writing-a-t4-text-template.md) 提供文本模板指令和控制块的语法。
