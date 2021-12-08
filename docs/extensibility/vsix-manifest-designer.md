---
title: VSIX 清单设计器 |Microsoft Docs
description: 了解 vsix 清单设计器如何修改 vsix 包清单文件，该文件用于为 Visual Studio 扩展设置安装行为。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.Sdk.VsixManifestEditor
helpviewer_keywords:
- vsixmanifest
- vsix manifest
- manifest designer
ms.assetid: 5a691e77-cf91-430d-90ea-361d9031ef83
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 75d11020681cb89d8e87e67abb907e84e4308348
ms.sourcegitcommit: 64d6c5cf93984bbb22812577af17128cd2239f79
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2021
ms.locfileid: "134366795"
---
# <a name="vsix-manifest-designer"></a>VSIX 清单设计器
修改 VSIX 包清单文件，该文件用于为 Visual Studio 扩展设置安装行为。

**Vsix 清单设计器** 映射到基础 VSIX 架构。 架构中的每个元素都可以通过使用设计器中的相应控件进行设置。 有关架构的详细信息，请参阅 [VSIX 扩展架构2.0 引用](../extensibility/vsix-extension-schema-2-0-reference.md)。

若要打开 **VSIX 清单设计器**，请在 **解决方案资源管理器** 中找到 *source.extension.vsixmanifest* 文件，然后打开该文件。 如果该文件不包含有效的 XML，则清单设计器将不会打开。

> [!NOTE]
> 生成包时， *source.extension.vsixmanifest* 文件会输出到 *source.extension.vsixmanifest。*

## <a name="uielement-list"></a>UIElement 列表
**VSIX 清单设计器** 包含四个部分，这些部分对应于架构的这些顶级元素：

- 元数据
- 安装目标
- 资产
- 依赖项

标题区包含下列控件：

- **产品名称** 描述扩展名称。
- **PRODUCT ID** 指定此包的唯一标识信息。
- **Author** 指定扩展的作者名称。
- **版本** 指定扩展的版本号。

" **元数据** " 选项卡包含下列控件：

- **说明** 提供要在 " **扩展管理器**" 中显示的扩展的文本说明。
- **语言** 指定包的默认语言，该语言对应于清单中的文本数据。 此 `Language` 属性遵循公共语言运行时 (CLR) 区域设置代码约定（例如 en-us、en、fr）。 默认情况下，该值为中立，这意味着包将在 Visual Studio 的任何语言版本上运行。
- **许可证** 指定包含用户许可证（如果存在）的文本文件。
- **图标** 指定图形文件 (*.png*， *.bmp*， *. jpeg*， *.Ico*) ，其中包含要在 " **扩展管理器**" 中显示的图标（如果存在图标）。 图标图像必须是32x32 像素或调整其大小。 如果未指定图标，则 **扩展管理器** 将使用默认图标。
- **预览图像** 指定图形文件 (*.png*， *.bmp*， *. jpeg*， *.Ico*) ，其中包含要在 " **扩展管理器**" 中显示的预览图像（如果存在预览图像）。 预览图像必须为200x200 大小像素。 如果未指定预览图像， **扩展管理器** 将使用默认映像。
- **标记** 添加了用于搜索提示的文本标记。
- **发行说明** 指定包含发行说明的文件 (*.txt*、 *.rtf*) 。 还获取显示发行说明的网站的 URL。
- **入门指南** 指定文件 (*.txt*、 *.rtf*) ，其中包含有关如何使用该扩展或 VSIX 包中内容的信息。 当扩展安装完成时，将显示此指南。 还获取显示指南的网站的 URL。
- **详细信息 URL** 指定包含有关产品的其他信息的网站的 url。

" **安装目标** " 选项卡包含下列控件：

- **安装类型** 列表 **Visual Studio 扩展** 和 **扩展 SDK** 作为目标安装类型。 选项会有所不同，具体取决于你选择的类型。
  - **Visual Studio 扩展** 列出了 **InstallationTarget** 元素，这些元素描述如何安装包以及此扩展可以安装到哪些 Visual Studio 产品。 每个产品都按名称和版本或版本范围单独标识。 产品可添加到列表、修改和删除。 产品的名称和版本与关联的 **InstallationTarget** 元素的 **Id** 和 **版本** 特性相对应。
    - **版本范围** 为 [12.0，14.0]，并使用以下表示法：
      - `[` -最小版本包含
      - `]` -最高版本包含
      - `(` -最小版本专用
      - `)` -最高独占版本
      - 单个版本 #-仅指定的版本

  - **扩展 SDK** 指定的全局安装的范围不是特定的产品和版本。 **目标平台标识符** 是目标平台，如 "Windows"。 **目标平台版本** 是目标平台的版本，例如8.0。 **Sdk 名称** 和 **sdk 版本** 分别是 sdk 的名称和版本号。

- **将为所有用户安装此 VSIX， (需要在安装) 提升**。 如果选中此复选框，则将为所有用户安装扩展;否则，只会为当前用户安装此程序。

- **此 VSIX 由 Windows Installer 安装**。 如果选中此复选框，则由 Windows Installer (*.msi* 文件) 安装扩展; 否则，它将作为典型的 vsix 包安装 (*.vsix* 文件) 。

" **资产** " 选项卡包含下列控件：

- **资产列表** 列出了描述此包所表面的扩展或内容元素的资产元素。 每个 extension 或 content 元素按源、类型和路径单独列出。 可以向列表中添加扩展和内容元素，还可以修改和删除它们。 扩展或内容元素的类型和路径对应于 `Type` 关联的元素的和 `Path` 特性 `Asset` 。 以下是已知的类型：
  - VisualStudio
  - Microsoft.VisualStudio.MefComponent
  - VisualStudio. ToolboxControl
  - VisualStudio
  - VisualStudio. ProjectTemplate
  - VisualStudio
  - VisualStudio. 程序集
  - ExtensionSDK

   若要添加或编辑资产，则必须指定资产类型、资产是当前解决方案中的项目还是文件系统中的文件以及项目的名称。 还可以指定要嵌入的文件夹的名称。

   您还可以创建自己的类型，并为它们指定唯一名称。

" **依赖关系** " 选项卡包含下列控件：

- **"名称"、"源" 和 "版本范围** " 列出此包所依赖的其他包中的依赖项元素。 如果指定了某个依赖项包，则必须先安装它，然后才能安装此包;否则，此软件包必须安装它。

   依赖项包由标识符、名称、版本范围、源以及依赖项的解析方式来指定。 每个依赖项包都按名称、版本和源单独列出。 可以向列表中添加、修改和删除依赖项包。

   标识符必须与 `ID` 依赖项包元数据的特性匹配。 源可以是当前解决方案中的项目、当前安装的扩展或文件。 " **依赖项解析方式** " 设置可以是嵌套包的相对路径，也可以是依赖项的下载位置的 URL。 依赖项包的 ID、版本和解析与 `Id` `Version` 关联元素的、和特性相对应 `Location` `Dependency` 。

## <a name="see-also"></a>请参阅
- [VSIX 扩展架构2.0 引用](../extensibility/vsix-extension-schema-2-0-reference.md)
- [VSIX 包的解析](../extensibility/anatomy-of-a-vsix-package.md)
