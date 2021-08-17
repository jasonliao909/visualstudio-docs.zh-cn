---
title: 如何：将依赖项添加到 VSIX 包|Microsoft Docs
description: 了解如何设置 VSIX 包部署，以安装目标计算机上尚未存在的任何依赖项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- package reference
- package assembly
- package dll
- vsix reference
ms.assetid: 8f20177b-dab9-43a3-b959-81a591b451d6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 0335e243fe0779060282cecdc58ad9deb608c948
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122050411"
---
# <a name="how-to-add-a-dependency-to-a-vsix-package"></a>如何：向 VSIX 包添加依赖项

可以设置 VSIX 包部署，以安装目标计算机上尚未存在的任何依赖项。 为此，请包括 *source.extension.vsixmanifest 文件的* VSIX 依赖项。

## <a name="to-add-a-dependency"></a>添加依赖项

1. 在"*设计"视图中打开 source.extension.vsixmanifest***文件。** 转到"依赖项 **"选项卡，** 然后单击"新建 **"。**

2. 若要添加已安装的扩展：在"添加新 **依赖项**"对话框中，选择"已安装的扩展"，然后在"名称"列表中选择一个扩展。

3. 若要添加另一个未安装的 VSIX：在"添加新依赖项"对话框中，选择"文件系统上的文件"，然后使用"浏览"按钮选择 VSIX。 

## <a name="require-a-specific-visual-studio-release"></a>需要特定的Visual Studio版本

例如，如果扩展需要特定版本的 Visual Studio 2017，则它依赖于 15.3 中发布的功能，可以在 VSIX **InstallationTarget** 中指定内部版本号。 例如，版本 15.3 的生成号为"15.0.26730.3"。 可在此处查看版本与生成号 [的映射](../install/visual-studio-build-numbers-and-release-dates.md)。 请注意，使用发行号"15.3"将无法正常工作。

如果扩展需要 15.3 或更高版本，则需要将 **InstallationTarget 版本** 声明为 [15.0.26730.3， 16.0) ：

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```

VSIXInstaller 将检测早期版本Visual Studio并通知用户需要更高版本的更新。

## <a name="see-also"></a>请参阅

- [VSIX 扩展架构 1.0 参考](/previous-versions/dd393700(v=vs.110))
- [VSIX 包剖析](../extensibility/anatomy-of-a-vsix-package.md)
- [为安装程序部署Windows扩展](../extensibility/preparing-extensions-for-windows-installer-deployment.md)