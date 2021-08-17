---
title: VSIX 清单设计器|Microsoft Docs
description: 了解 VSIX 清单设计器如何修改 VSIX 包清单文件，该文件设置扩展插件Visual Studio行为。
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
ms.openlocfilehash: 4fc696d14ca7eb7c9efd3f038ce399cb19f1a926be8bbe515f694b5aa23d4af1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121335233"
---
# <a name="vsix-manifest-designer"></a>VSIX 清单设计器
修改 VSIX 包清单文件，该文件设置扩展插件Visual Studio行为。

 **VSIX 清单设计器** 映射到基础 VSIX 架构。 架构中的每个元素都可以通过使用设计器中的相应控件进行设置。 有关架构详细信息，请参阅 [VSIX 扩展架构 2.0 参考](../extensibility/vsix-extension-schema-2-0-reference.md)。

 若要打开 **VSIX 清单设计器**，请在 解决方案资源管理器 找到 *source.extension.vsixmanifest* 文件并打开该文件。  如果文件不包含有效的 XML，则清单设计器不会打开。

> [!NOTE]
> 生成 *包时，source.extension.vsixmanifest* 文件将输出到 *extension.vsixmanifest。*

## <a name="uielement-list"></a>UIElement 列表
 **VSIX 清单设计器** 包含四个部分，这些部分对应于架构的这些顶级元素：

- 元数据

- 安装目标

- 资产

- 依赖关系

  标题区域包含以下控件。

  **产品名称** 描述扩展名。

  **产品 ID** 指定此包的唯一标识信息。

  **作者** 指定扩展的作者的名称。

  **版本** 指定扩展的版本号。

  " **元数据** "选项卡包含以下控件。

  **说明** 提供要显示在扩展管理器 中的扩展 **的文本说明**。

  **语言** 指定包的默认语言，该语言对应于清单中的文本数据。 属性遵循公共语言运行时 (CLR) 资源程序集（例如 `Language` en-us、en、fr-fr）区域设置代码约定。 默认情况下，该值是非特定值，这意味着包将在任何语言版本的 Visual Studio。

  **许可证** 指定包含用户许可证的文本文件（如果存在）。

  **图标** 指定图形文件 (.png、.bmp、.jpeg、.ico) ，其中包含要显示在扩展管理器 中的图标（如果存在图标）。 ** **   图标图像必须为 32x32 像素，或者大小调整为这些尺寸。 如果未指定图标，则 **扩展管理器** 使用默认图标。

  **预览图像** 指定图形文件 (.png、.bmp、.jpeg、.ico ) ，其中包含要显示在扩展管理器 中的预览图像（如果存在预览图像）。 ** **  预览图像必须为 200x200 像素。 如果未指定预览映像， **则扩展管理器** 将使用默认映像。

  **标记** 添加要用于搜索提示的文本标记。

  **发行说明** 指定包含发行 *(.txt**的 .rtf*) 文件。 还采用显示发行说明的网站的 URL。

  **入门指南** 指定一 (.txt *、.rtf*) ，其中包含有关如何使用 VSIX 包中的扩展名或内容的信息。 ** 当扩展安装完成时，将显示本指南。 还采用显示指南的网站的 URL。

  **详细信息 URL** 指定包含有关产品的其他信息的网站的 URL。

  " **安装目标"** 选项卡包含以下控件。

  **安装类型** 列出 **Visual Studio扩展** 和 **扩展 SDK** 作为目标安装类型。 选项因选择的类型不同而不同。

  **Visual Studio 扩展** 列出 **InstallationTarget** 元素，这些元素描述如何安装包以及Visual Studio此扩展的哪些产品。 每个产品按名称和版本范围单独标识。 可以将产品添加到列表、修改和删除产品。 产品的名称和版本对应于关联的 **InstallationTarget** 元素的 **Id** 和 Version 属性。

  **版本范围** 为 [12.0， 14.0]，并采用以下表示法：

- [ - 最低版本（含）

- ] - 最大版本（含）

-  ( - 最低版本独占

- ) - 独占的最大版本

- 单个版本 # - 仅指定版本

  **扩展 SDK** 指定不以特定产品和版本为作用域的全局安装。 **目标平台** 标识符是目标平台，例如"Windows"。 **目标平台** 版本是目标平台的版本，例如 8.0。 **SDK 名称和** **SDK 版本** 分别为 SDK 的名称和版本号。

  **此 VSIX 适用于要求在安装 (提升权限的所有用户)** 如果选中此复选框，则为所有用户安装扩展;否则，它仅为当前用户安装。

  **此 VSIX 由 Windows 安装程序安装** 如果选中此复选框，则安装程序会安装扩展Windows安装程序 *(.msi文件*) ;否则，它会作为典型的 VSIX 包 (*.vsix* 文件) 。

  " **资产** "选项卡包含以下控件。

  **资产列表** 列出描述此包所显示扩展名或内容元素的资产元素。 每个扩展或内容元素按源、类型和路径单独列出。 扩展和内容元素可以添加到列表、修改和删除。 扩展或内容元素的类型和路径对应于关联元素的 和 `Type` `Path` `Asset` 属性。 以下是已知的类型：

- Microsoft.VisualStudio.Package

- Microsoft.VisualStudio.MefComponent

- Microsoft.VisualStudio.ToolboxControl

- Microsoft.VisualStudio.Samples

- Microsoft.VisualStudio.ProjectTemplate

- Microsoft.VisualStudio.ItemTemplate

- Microsoft.VisualStudio.Assembly

- Microsoft.ExtensionSDK

  若要添加或编辑资产，必须指定资产类型、资产是当前解决方案中的项目还是文件系统中的文件，以及项目的名称。 还可以指定要嵌入的文件夹的名称。

  还可以创建自己的类型，并赋予它们唯一的名称。

  " **依赖项"** 选项卡包含以下控件。

  **名称、源和版本范围** 列出此包的依赖项元素，这些元素是此包所依赖的其他包。 如果指定了依赖项包，则必须在安装此包之前安装它;否则，此包必须安装它。

  依赖项包由标识符、名称、版本范围、源以及依赖项的解析方式指定。 每个依赖项包按名称、版本和源单独列出。 依赖项包可以添加到列表、修改和删除。

  标识符必须与依赖项 `ID` 包元数据的 属性匹配。 源可以是当前解决方案中的项目、当前安装的扩展名或文件。 **"如何解析依赖项"** 设置可以是嵌套包的相对路径或依赖项下载位置的 URL。 依赖项包的 ID、版本和解析对应于关联元素的 、 和 `Id` `Version` `Location` `Dependency` 属性。

## <a name="see-also"></a>请参阅
- [VSIX 扩展架构 2.0 参考](../extensibility/vsix-extension-schema-2-0-reference.md)
- [VSIX 包剖析](../extensibility/anatomy-of-a-vsix-package.md)
