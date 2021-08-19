---
title: VSIX Project 模板 |Microsoft Docs
description: 了解如何使用 vsix Project 模板来包装 vsix 项目中的 Visual Studio 扩展，然后将包发布到 Visual Studio Marketplace。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- deploy packages
- publish extension
ms.assetid: b6c82167-e2a5-4cff-8c8b-2d72e2a9092c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6d6cb7112d404b0ecc9decbc7e5b7caea251ab35
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122109768"
---
# <a name="vsix-project-template"></a>VSIX 项目模板

您可以使用 vsix Project 模板来包装 VSIX 项目中的一个或多个 Visual Studio 扩展，然后将包发布到[Visual Studio Marketplace](https://marketplace.visualstudio.com/)网站。

 VSIX 部署支持 Vspackage、程序集、MEF 组件、项目模板、项模板、工具箱控件和自定义扩展类型。

> [!NOTE]
> 若要使用 VSIX 项目，必须安装 Visual Studio SDK。 有关 Visual Studio sdk 的详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

## <a name="where-to-find-the-vsix-project-template"></a>在何处查找 VSIX 项目模板

通过搜索 "vsix"，可以在 "**新建 Project** " 对话框中使用 "vsix Project" 模板。  同时提供 c # 和 Visual Basic 版本。

> [!TIP]
> 应确保在 "**新建 Project** " 对话框顶部的下拉列表框中指定 .NET Framework 4.5 或更高版本。

## <a name="uses-of-the-vsix-project-template"></a>使用 VSIX 项目模板

VSIX 项目模板有两个主要用途：

- 部署项目模板、项模板和扩展。

- 将多个扩展的输出包装在一个部署包中。

## <a name="packaging-an-extension-in-an-empty-vsix-project"></a>在空 VSIX 项目中打包扩展

可以通过将现有的扩展包装到空的 VSIX 项目中来打包现有扩展或尚未提供 VSIX 支持的扩展。 要包装的扩展必须是 [VSIX 架构](../extensibility/vsix-extension-schema-2-0-reference.md)支持的类型。

### <a name="to-package-an-extension-by-using-a-vsix-project"></a>使用 VSIX 项目打包扩展

1. 生成组成扩展的项目。

2. 使用 **vsix Project** 模板创建 vsix 项目。

    *Source.extension.vsixmanifest* 在 **清单设计器** 中打开。

3. 在 " **资产** " 选项卡上，选择 " **新建** " 按钮。

    此时将显示 " **添加新资产** " 对话框。

4. 在 " **类型** " 列表中，选择要添加的扩展的类型。

5. 若要添加当前解决方案中包含的 extension 或 content 元素 (例如，项模板或编译的程序集) ，请执行以下步骤：

   1. 在 " **源** " 列表中，选择 " **当前解决方案中的项目**"。

   2. 在 **Project** 列表中，选择扩展插件的名称。

   3. 在 " **嵌入此文件夹** " 框中，输入要嵌入资产的文件夹的名称，然后选择 **"确定"** 按钮。

6. 若要添加当前解决方案中未包含的 extension 或 content 元素，请执行以下步骤：

   1. 在 " **源** " 列表框中，选择 **文件系统上的文件**。

   2. 在 " **路径** " 字段中，输入编译或压缩的扩展文件的完整路径，或者使用 " **浏览** " 按钮浏览到该文件。

   3. 在 " **嵌入此文件夹** " 框中，输入要嵌入资产的文件夹的名称，然后选择 **"确定"** 按钮。

7. 如果希望包包含其他扩展，请以相同方式添加它们。

8. 生成解决方案。

    [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 生成一个 *.vsix* 文件，该文件包含 vsix 清单文件、[Content_Types]*.xml* 文件以及添加到项目中的所有扩展资产。

## <a name="see-also"></a>请参阅

- [VSIX 扩展架构2.0 引用](../extensibility/vsix-extension-schema-2-0-reference.md)
- [查找并使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)
