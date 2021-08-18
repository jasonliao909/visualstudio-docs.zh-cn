---
title: Visual Studio命令表 (。Vsct) Files |Microsoft Docs
description: 了解命令表配置文件，这些文件是描述 VSPackage 包含的命令集的文本文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, overview
- Visual Studio command table configuration files (VSCT), overview
ms.assetid: 1313adb4-add4-4e74-90e2-f4be522f5259
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 8eb8c98586300644b3aef8be8a68c9ae1fd8196e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122132253"
---
# <a name="visual-studio-command-table-vsct-files"></a>Visual Studio 命令表格 (.Vsct) 文件
命令表配置文件是描述 VSPackage 包含的命令集的文本文件。 VSCT (编译器) 将基于 XML 的配置文件 (.vsct) 编译为二进制命令表输出 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (.cto) 文件。 结果 .cto 文件与使用命令表创建的文件相同，这些命令表 (使用) 编译 .compiler 配置文件。 但是，基于 XML 的 .vsct 文件具有一些优点，例如 XML 编辑器和 XML IntelliSense。

 若要详细了解 .vsct 文件的语法和语义，请参阅设计 XML 命令表 [ (。Vsct) 文件](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)

## <a name="in-this-section"></a>本节内容
 [设计 XML 命令表格 (.Vsct) 文件](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)

 介绍如何设计 .vsct 文件。

 [如何：创建 .Vsct 文件](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)

 比较用于创建 .vsct 文件的方法。 描述手动创建新的 .vsct 文件的过程。

## <a name="related-sections"></a>相关章节
 [VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)

 提供有关命令表 XML 配置文件的每个部分的详细信息。

 [命令表配置 (。") ](/previous-versions/bb165153(v=vs.100)) 提供已弃用 .保存文件格式的概述。

 [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 描述命令表格式规范。

 [VSPackage 中的资源](../../extensibility/internals/resources-in-vspackages.md)

 介绍如何在托管 VSPackages 中使用托管资源以及非托管资源。

 [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)

 说明如何创建包含菜单、工具栏和命令组合框的 UI。