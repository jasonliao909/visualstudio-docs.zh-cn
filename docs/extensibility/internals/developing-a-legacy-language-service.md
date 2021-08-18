---
title: 开发旧版语言服务|Microsoft Docs
description: 了解如何将旧版语言服务作为 VSPackage 的一部分实现，或通过使用 MANAGED EXTENSIBILITY FRAMEWORK (MEF) 扩展。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.vsip.LangServWiz.langtoks
- vs.vsip.LangServWiz.welcome
- vs.vsip.LangServWiz.langSpec
- vs.vsip.LangServWiz.langInfo
- vs.vsip.LangServWiz.langServOpts
helpviewer_keywords:
- language services, developing
ms.assetid: 6151ba88-c1c3-41de-a1cc-668f494d48d1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 4b300756334a84dd2e3d6ade83cc48caa10349bf
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122124615"
---
# <a name="develop-a-legacy-language-service"></a>开发旧版语言服务
本部分链接到可帮助你创建旧版语言服务的主题。

 旧版语言服务作为 VSPackage 的一部分实现，但实现语言服务功能的较新方式是使用 MEF 扩展。 若要详细了解实现语言服务的新方法，请参阅编辑器 [和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 建议尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并让你能够利用新的编辑器功能。

## <a name="in-this-section"></a>本节内容
- [旧版语言服务模型](../../extensibility/internals/model-of-a-legacy-language-service.md)

 为核心编辑器提供最小语言 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 服务的模型。 可以使用此模型作为创建自己的语言服务的指南。

- [旧版语言服务接口](../../extensibility/internals/legacy-language-service-interfaces.md)

 讨论实现语言服务所需的对象，并提供可用于提供语法突出显示、方法数据和其他功能的其他对象列表。

- [截获旧版语言服务命令](../../extensibility/internals/intercepting-legacy-language-service-commands.md)

 描述如何将命令筛选器插入到语言服务中，以截获文本视图将处理的命令。

- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service2.md)

 提供有关如何使用 注册语言服务的信息 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [调试的语言服务支持](../../extensibility/internals/language-service-support-for-debugging.md)

 描述语言服务如何提供功能来支持调试器。

- [清单：创建旧版语言服务](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)

 提供有关为核心编辑器创建和集成语言服务的分步说明。

## <a name="related-sections"></a>相关章节
- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 讨论如何在语言服务中实现语法突出显示。

- [旧版语言服务中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)

 讨论语句完成，语言服务可帮助用户完成他们已开始键入的语言关键字或元素的过程。

- [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)

 介绍如何为重载函数和方法提供方法提示。

- [如何：在旧版语言服务中提供隐藏文本支持](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)

 说明隐藏文本区域的用途，并提供有关如何实现隐藏文本区域的说明。

- [如何：在旧版语言服务中提供扩展的大纲显示支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)

 介绍除了支持"折叠到定义"命令之外，扩展语言大纲支持的两 *个选项* 。
