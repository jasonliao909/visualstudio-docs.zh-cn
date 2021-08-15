---
title: VSIX Project模板|Microsoft Docs
description: 了解如何使用 VSIX Project模板将 Visual Studio 扩展包装在 VSIX 项目中，然后将包发布到 Visual Studio Marketplace。
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
ms.openlocfilehash: 781ee248999510bf28323d34e6fe8025bd40f9c317656045b3c196f15499d029
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121335220"
---
# <a name="vsix-project-template"></a>VSIX 项目模板

可以使用 VSIX Project模板将一个或多个 Visual Studio 扩展包装在 VSIX 项目中，然后在 Visual Studio [Marketplace](https://marketplace.visualstudio.com/)网站上发布包。

 VSIX 部署支持 VSPackage、程序集、MEF 组件、项目模板、项模板、工具箱控件和自定义扩展类型。

> [!NOTE]
> 若要使用 VSIX 项目，必须安装 Visual Studio SDK。 有关 Visual Studio SDK Visual Studio，请参阅 Visual Studio [SDK。](../extensibility/visual-studio-sdk.md)

## <a name="where-to-find-the-vsix-project-template"></a>在哪里可以找到 VSIX 项目模板

VSIX Project模板在"新建 **Project对话框中通过** 搜索"vsix"提供。  C# 和 Visual Basic版本。

> [!TIP]
> 应确保在"新建.NET Framework对话框顶部的下拉列表框中指定 4.5 **Project更高版本。**

## <a name="uses-of-the-vsix-project-template"></a>VSIX 项目模板的用法

VSIX 项目模板有两个主要用途：

- 部署项目模板、项模板和扩展。

- 将多个扩展的输出包装到一个部署包中。

## <a name="packaging-an-extension-in-an-empty-vsix-project"></a>在空的 VSIX 项目中打包扩展

可以通过将现有扩展或尚未具有 VSIX 支持的扩展打包到空的 VSIX 项目中。 要包装的扩展必须是 [VSIX](../extensibility/vsix-extension-schema-2-0-reference.md)架构 支持的类型。

### <a name="to-package-an-extension-by-using-a-vsix-project"></a>使用 VSIX 项目打包扩展

1. 生成生成扩展的项目。

2. 使用 VSIX 模板创建 **VSIX Project** 项目。

    *Source.extension.vsixmanifest* 将在清单 **设计器 中打开**。

3. 在" **资产"** 选项卡上，选择" **新建"** 按钮。

    将出现 **"添加新资产** "对话框。

4. 在 **"类型** "列表中，选择要添加的扩展的类型。

5. 若要添加当前解决方案中包含的扩展或内容元素，例如 (模板或编译的程序集) ，请执行以下步骤：

   1. 在" **源"** 列表中， **选择当前解决方案 中的项目**。

   2. 在 **Project** 列表中，选择扩展的名称。

   3. 在" **嵌入到此文件夹** "框中，输入要嵌入资产的文件夹的名称，然后选择"确定 **"** 按钮。

6. 若要添加当前解决方案中未包含的扩展或内容元素，请执行以下步骤：

   1. 在"**源"** 列表框中，选择 **"文件系统上的文件"。**

   2. 在 **"路径**"字段中，输入已编译或压缩扩展文件的完整路径，或使用"浏览"按钮浏览到该文件。

   3. 在" **嵌入到此文件夹** "框中，输入要嵌入资产的文件夹的名称，然后选择"确定 **"** 按钮。

7. 如果希望包包含其他扩展，请以相同的方式添加它们。

8. 生成解决方案。

    [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 生成 *一个 .vsix* 文件，其中包含 VSIX 清单文件、[Content_Types]**.xml文件以及添加到项目的所有扩展资产。

## <a name="see-also"></a>另请参阅

- [VSIX 扩展架构 2.0 参考](../extensibility/vsix-extension-schema-2-0-reference.md)
- [查找和使用Visual Studio扩展](../ide/finding-and-using-visual-studio-extensions.md)
