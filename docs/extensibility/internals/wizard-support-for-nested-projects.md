---
title: 嵌套项目的向导支持 |Microsoft Docs
description: 了解父项目可为 Visual Studio SDK 中 VSPackage 的嵌套项目实现的两个向导。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122041706"
---
# <a name="wizard-support-for-nested-projects"></a>嵌套项目的向导支持
IDE 运行可实现嵌套项目的父项目的两个向导： "**新建 Project** 向导" 和 "**添加项** 向导"。

 如果用户通过在 "文件" 菜单上选择 "**添加 Project** 并单击"**新建 "Project** ，或者选择"**添加**"并右键单击解决方案资源管理器中的" 新建 " **Project** 来启动"**新建 Project** 向导 "，则 IDE 将运行 **AddProject** 命令， **AddProject** 命令的父项目实现将返回模板项目文件或包含一组上下文参数的向导 ( 文件。

 同样，一个父项目的 **AddItem** 向导实现返回一个 .vsz 文件，该文件具有一组不同的上下文参数。

 有关向导的详细信息，请参阅[向导 (。.vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)、[上下文参数](../../extensibility/internals/context-parameters.md)和[注册 Project 和项模板](../../extensibility/internals/registering-project-and-item-templates.md)。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [嵌套项目](../../extensibility/internals/nesting-projects.md)
