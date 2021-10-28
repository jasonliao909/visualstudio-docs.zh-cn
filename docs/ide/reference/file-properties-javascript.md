---
title: 文件属性，JavaScript
description: 了解如何使用文件属性来指示项目系统应对文件执行的操作。
ms.custom: SEO-VS-2020
ms.date: 06/21/2017
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- javascript.project.property.expandedsdknode.fileversion
- javascript.project.property.expandedsdknode.uri
- javascript.project.property.expandedsdknode.filename
- javascript.project.property.reference.description
- javascript.project.property.reference.specificversion
- javascript.project.property.reference.identity
- javascript.project.property.fullpath
- javascript.project.property.packageaction
- javascript.project.property.reference.package
- javascript.project.property.copytooutputdirectory
- javascript.project.property.expandedsdknode.sdkpath
- javascript.project.property.reference.filetype
- javascript.project.property.reference.culture
- javascript.project.property.filename
- javascript.project.property.reference.resolvedpath
- javascript.project.property.reference.version
ms.assetid: 085913b8-a97b-45f7-85fa-bbb0902f3ee9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c54ce24025f9ec15bc03d02825e961f9a03f3715
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126644416"
---
# <a name="file-properties-javascript"></a>文件属性，JavaScript

文件属性可用于指示项目系统应对文件执行的操作。 例如，可以设置文件属性，指示是否应将文件作为资源文件添加到包。

可以在解决方案资源管理器中选择任何文件，然后在“属性”窗口中检查其属性。 JavaScript 文件具有四个属性：复制到输出目录、包操作、文件名和文件路径。

## <a name="file-properties"></a>文件属性
本部分介绍 JavaScript 文件的共同属性。

### <a name="copy-to-output-directory-property"></a>“复制到输出目录”属性
此属性指定将选定源文件复制到输出目录的条件。 如果文件始终不复制到输出目录，则选择“不复制”。 如果文件始终复制到输出目录，则选择“始终复制”。 如果只有文件比输出目录中现有的同名文件更新时才复制该文件，则选择“如果较新则复制”。

### <a name="package-action"></a>包操作
“包操作”属性指示执行生成时，Visual Studio 对文件执行的操作。 “包操作”可以具有任一以下值：

- 无 - 文件未包含在程序包清单中。 其中一个示例是包含自述文件等文档的文本文件。

- 内容 - 文件包含在程序包清单中。 例如，此设置为 .htm、.js、.css、图像、音频或视频文件的默认值。

- 清单 - 文件未包含在程序包清单中。 相反，文件用于生成程序包清单时的输入。 这是 package.appxmanifest 文件的默认值。

- 资源 - 文件未包含在程序包清单中。 但是，文件的内容在程序包清单的包资源索引 (PRI) 中建立了索引。 通常用于资源文件。

“包操作”的默认值取决于添加到解决方案的文件的扩展名。

### <a name="file-name-property"></a>“文件名”属性
以只读值的方式显示文件名。 若要重命名文件，必须在解决方案资源管理器中右键单击该文件，选择“重命名”。

### <a name="full-path-property"></a>“完整路径”属性
以只读值的形式显示文件的完整路径。 若要更改文件的路径，可以在解决方案资源管理器中拖放文件。

## <a name="reference-file-properties"></a>“引用文件”属性
本部分介绍从使用 JavaScript 生成的 UWP 应用引用的文件的共同属性。 在解决方案资源管理器中选择 .winmd 文件、SDK 引用、项目到项目的引用或程序集引用等引用时，其他属性会根据文件类型显示在“属性”窗口中。

### <a name="culture"></a>环境
显示与引用相关联的语言。

### <a name="file-type"></a>文件类型
显示引用的文件类型。

### <a name="file-version"></a>文件版本
显示引用的文件版本。

### <a name="identity"></a>标识
显示用于存储在项目文件中的项目的引用标识。

### <a name="package"></a>程序包
显示与引用相关联的程序包清单的名称。

### <a name="resolved-path"></a>已解析的路径
显示项目中使用的引用的路径。

### <a name="sdk-path"></a>SDK 路径
显示已引用 SDK 文件的路径。

### <a name="uri"></a>Uri
显示必须包含在项目的 HTML 或 JavaScript 文件中才能将文件作为源文件包含在内的 URI。

### <a name="version"></a>版本
显示引用的版本。

## <a name="see-also"></a>另请参阅

- [管理项目和解决方案属性](../../ide/managing-project-and-solution-properties.md)