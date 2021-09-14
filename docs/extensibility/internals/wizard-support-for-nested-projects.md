---
title: 嵌套项目的向导|Microsoft Docs
description: 了解父项目可以在 SDK 中为 VSPackage 中的嵌套项目实现Visual Studio向导。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add Item wizard
- nested projects, wizard support
- New Project wizard
ms.assetid: 1b496acc-b326-4cdb-bb48-e3b5c6f12e05
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c0fdc97b8ef15b4fdfd8fee13affb52b1935b80f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665318"
---
# <a name="wizard-support-for-nested-projects"></a>嵌套项目的向导支持
IDE 运行嵌套项目的父项目可以实现的两 **个** 向导：新建Project向导和 **添加项** 向导。

 如果用户通过选择"文件"菜单上的 **"** 添加"Project 并单击"新建 **Project"** 或选择"添加"并右键单击 解决方案资源管理器中的"新建 Project"来启动"新建 Project"向导，则 IDE 将运行 AddProject 命令和父项目的 **AddProject** 命令实现，返回模板项目文件或向导 (.vsz) 文件，该文件具有一组上下文参数。 

 同样，父项目的 **AddItem** 向导实现将返回一个 .vsz 文件，该文件具有不同的上下文参数集。

 有关向导详细信息，请参阅向导[ (。Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)、[上下文参数](../../extensibility/internals/context-parameters.md)和[注册Project和项模板](../../extensibility/internals/registering-project-and-item-templates.md)。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [嵌套项目](../../extensibility/internals/nesting-projects.md)
