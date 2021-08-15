---
title: 部署自定义起始页|Microsoft Docs
description: 了解如何通过使用 VSIX 部署或将文件复制到目标计算机上的正确位置来部署自定义起始页。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- package start page
- deploy start page
ms.assetid: 4a7eb360-de83-41d5-be53-3cfb160d19f9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 6cbe93af3737526a5adf1719f0f4b129cb3076a7dadaa2bade9a413e0a69407e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414917"
---
# <a name="deploy-custom-start-pages"></a>部署自定义起始页

可以使用 VSIX 部署或将文件复制到目标计算机上的正确位置来部署自定义起始页。

## <a name="vsix-deployment-by-using-the-start-page-project-template"></a>使用起始页项目模板进行 VSIX 部署

使用起始页项目模板创建起始页，然后生成项目时，Visual Studio创建可分发的 *.vsix* 文件。 在 *.vsix* 文件中打包起始页提供以下部署选项，具体取决于目标受众：

- 可以将 *.vsix* 文件放在网络共享或公共网站上。 当有人打开该文件时，将自动安装起始页。

- 可以将 *.vsix* 文件上传到 Visual Studio [Marketplace](https://marketplace.visualstudio.com/)网站，以便用户可以使用扩展管理器 **进行安装**。

起始页项目模板在起始页Visual Studio创建默认副本，以便修改副本并保留原始副本。

可以使用扩展管理器或从网站下载起始页项目模板来获取该模板。

## <a name="vsix-deployment-without-using-the-start-page-project-template"></a>无需使用起始页项目模板即可进行 VSIX 部署
 成功的 VSIX 部署要求在 VSIX 注册过程和扩展管理器识别的文件夹中 **安装扩展**。 由于起始页项目模板已指定正确的文件夹，因此建议每当要打包 VSIX 部署的扩展时使用它。 但是，如果无法使用模板，可以在不使用的情况下创建 VSIX 部署。

 若要在不使用起始页项目模板的情况下创建 VSIX 部署，请首先通过以下两种方式之一为起始页创建 *.vsix* 文件：

- 通过将自定义起始页文件添加到空的 VSIX Project。 有关详细信息，请参阅 [VSIX 项目模板](../extensibility/vsix-project-template.md)。

- 通过手动创建 *.vsix* 文件。 若要手动 *创建 .vsix* 文件，请执行：

   1. 创建新 *文件夹中的 extension.vsixmanifest* 文件和 *[Content_Types].xml* 文件。 有关详细信息，请参阅 [VSIX 包剖析](../extensibility/anatomy-of-a-vsix-package.md)。

   2. 在Windows资源管理器中，右键单击包含两个 XML 文件的文件夹，单击"发送到"，然后单击"压缩 (压缩) 文件夹" 。 将生成的 *.zip* 文件重命名为 *Filename.vsix*，其中 Filename 是安装包的可再发行文件的名称。

若要Visual Studio起始页，VSIX 清单的 必须包含将 属性设置为 `Content Element` 的 `CustomExtension Element` `Type` `"StartPage"` 。 使用 VSIX 部署安装的起始页扩展在"启动选项"页上的"自定义起始页"列表中显示为 **"[已安装扩展]** 扩展 *名"。*

如果起始页包包含程序集，则必须添加绑定路径注册，以便它们可在启动Visual Studio可用。 为此，请确保包包含包含以下信息的 *.pkgdef* 文件。

```
[$RootKey$\BindingPaths\{Insert a new GUID here}]
"$PackageFolder$"=""
```

### <a name="vsix-deployment-for-all-users"></a>所有用户的 VSIX 部署
 默认情况下，VSIX 包中部署的扩展仅为当前用户安装。 可以通过创建目标计算机部署，为目标计算机的所有All-Users安装。

### <a name="to-create-an-all-users-deployment"></a>创建All-Users部署

1. 在代码 *视图中打开 extension.vsixmanifest* 文件。

2. 在 `Identifier` vsix 清单的 元素中，添加值为 `AllUsers` 的元素 `true` 。

    ```
    <AllUsers>true</AllUsers>
    ```

     这将导致 vsix 安装程序提示输入管理员权限，然后将文件安装到 *\Common7\IDE\Extensions*。

3. 打开 *.pkgdef* 文件。

4. 通过 *添加以下内容修改 .pkgdef* 以在 HKLM 下设置默认起始页，其中 *MyStartPage.xaml* 是 *包含起始页的 .xaml* 文件的名称。

     [$RootKey$\StartPage\Default]

     "Uri"="$PackageFolder$ \\ *MyStartPage.xaml*"

     这Visual Studio查找新的起始页位置。

## <a name="file-copy-deployment"></a>文件复制部署
 不需要创建 *.vsix* 文件来部署自定义起始页。 相反，可以将标记和支持文件直接复制到用户的 <em>\StartPages \* 文件夹中。"启动 *选项"页上</em>* 的"自定义起始页"列表列出了该文件夹中每个 *.xaml* 文件以及路径，例如 *%USERPROFILE%\我的文档\Visual Studio {version}\StartPages \\ {File Name}.xaml 。* 如果起始页包含对私有程序集的引用，则必须复制这些程序集并将其粘贴到 *\PrivateAssemblies \* 文件夹中。

 若要分发在未将其打包到 *.vsix* 文件中的情况下创建的起始页，建议使用基本文件复制策略，例如批处理脚本，或允许将文件放入所需目录中的其他任何部署技术。

### <a name="to-manually-install-a-custom-start-page"></a>手动安装自定义起始页

1. 复制包含起始页标记的 *.xaml* 文件以及除程序集外的任何支持文件，并将其粘贴到用户的 *\StartPages \* 文件夹中。

2. 如果起始页需要程序集，请复制这些程序集并将其粘贴到 *中。 \\{Visual Studio安装文件夹}\Common7\IDE\PrivateAssemblies \\*。

3. 在"**启动选项"页上** 的"自定义起始页"列表中，选择新的起始页。 有关详细信息，请参阅 [自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)。

## <a name="see-also"></a>另请参阅

- [自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)
- [将用户控件添加到起始页](../extensibility/adding-user-control-to-the-start-page.md)
