---
title: VSIX 包结构|Microsoft Docs
description: 了解 VSIX 包的内容，Visual Studio包含一个或多个扩展名的文件Visual Studio元数据清单文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- visual studio extension
- vsix
- packages
ms.assetid: 8b86d62f-c274-4e91-82e0-38cdb9a423d5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 9485aeba7d531c0a05f33ad759688e9fd05a29f9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122111978"
---
# <a name="anatomy-of-a-vsix-package"></a>VSIX 包剖析
VSIX 包是一个 *.vsix* 文件，其中包含一个或多个Visual Studio扩展，以及用于Visual Studio和安装扩展的元数据。 该元数据包含在 VSIX 清单和 *[Content_Types].xml* 文件中。 VSIX 包还可以包含一个或多个 *Extension.vsixlangpack* 文件以提供本地化的设置文本，并且可能包含其他 VSIX 包来安装依赖项。

 VSIX 包格式遵循 开放打包约定 (OPC) 标准。 包包含二进制文件和支持文件，以及 *[Content_Types].xml* 文件以及 *.vsix* 清单文件。 一个 VSIX 包可能包含多个项目的输出，甚至是具有自己的清单的多个包的输出。

> [!NOTE]
> VSIX 包中包含的文件的名称不得包含空格，也不能包括[ \[ RFC2396 \] ](https://www.rfc-editor.org/rfc/rfc2396.txt)下定义的统一资源标识符 (URI) 保留的字符。

## <a name="the-vsix-manifest"></a>VSIX 清单
 VSIX 清单包含有关要安装的扩展的信息，并遵循 VSX 架构。 有关详细信息，请参阅 [VSIX 扩展架构 1.0 参考](/previous-versions/dd393700(v=vs.110))。 有关 VSIX 清单的示例，请参阅根元素的[PackageManifest (，VSX 架构) 。 ](/previous-versions/dd393754(v=vs.110))

 VSIX 清单包含在 `extension.vsixmanifest` ^.vsix* 文件中时，必须命名该清单。

## <a name="the-content"></a>内容
 VSIX 包可能包含模板、工具箱项、VSPackage 或由 Visual Studio。

## <a name="language-packs"></a>语言包
 VSIX 包可以包含一个或多个 *Extension.vsixlangpack* 文件，以在安装过程中提供本地化文本。 有关详细信息，请参阅本地化 [VSIX 包](../extensibility/localizing-vsix-packages.md)。

## <a name="dependencies-and-references"></a>依赖项和引用
 VSIX 包可能包含其他 VSIX 包作为引用。 其他每个包都必须包含自己的 VSIX 清单。

 如果用户尝试安装具有依赖项的扩展，安装程序将验证用户系统是否安装了所需的程序集。 如果找不到所需的程序集 **，扩展和更新** 将显示缺少的程序集的列表。

 如果扩展清单包含一个或多个 Reference[](/previous-versions/visualstudio/visual-studio-2010/dd393687(v=vs.100))元素，则扩展和更新会将每个引用的清单与系统上安装的扩展进行比较，并安装引用的扩展（如果尚未安装）。 如果安装了引用的扩展的早期版本，则较新版本将替换它。

 如果多项目解决方案中的项目包含对同一解决方案中另一个项目的引用，则 VSIX 包将包含该项目的依赖项。 可以通过选择内部项目的引用，然后在"属性"窗口中将 **"VSIX** 中包含的输出组"属性设置为 来替代此行为 `BuiltProjectOutputGroup` 。

 若要在 VSIX 包中包含引用程序集中的附属 DLL，请添加到 `SatelliteDllsProjectOutputGroup` **"VSIX** 中包含的输出组"属性。

## <a name="installation-location"></a>安装位置
 在安装 **过程中** ，扩展和更新在 *%LocalAppData%\Microsoft\VisualStudio\14.0\Extensions* 下的文件夹中查找 VSIX 包的内容。

 默认情况下，安装仅适用于当前用户，因为 *%LocalAppData%* 是特定于用户的目录。 但是，如果将清单的[AllUsers](/previous-versions/ee191547(v=vs.110))元素设置为 `True` ，则扩展将在<em>下安装。 \\ </em>VisualStudioInstallationFolder<em>\Common7\IDE\Extensions</em>和 将可供计算机的所有用户使用。

## <a name="content_typesxml"></a>[Content_Types].xml
 *[Content_Types].xml* 文件标识扩展的 *.vsix* 文件中文件类型。 Visual Studio安装包期间使用此文件，但不安装文件本身。 有关此文件的信息，请参阅 [[Content_types].xml 的结构](the-structure-of-the-content-types-dot-xml-file.md)。

 *[Content_Types].xml* OPC 开放打包约定 (标准) 文件。 有关 OPC 的信息，请参阅 [OPC：](/archive/blogs/msdnmagazine/opc-a-new-standard-for-packaging-your-data) 在 MSDN 网站上打包数据的新标准。