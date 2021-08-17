---
title: 在 Visual Studio 2022 预览版创建扩展时，Visual Studio 2019 年目标
description: 了解如何使用 Visual Studio 2022 预览版创建Visual Studio 2019 Visual Studio扩展。
ms.date: 06/08/2021
ms.topic: conceptual
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
monikerRange: vs-2022
ms.workload:
- vssdk
feedback_system: GitHub
ms.openlocfilehash: 0abd690d5c9d1af9e58bfa856d8880f01e34e8f0c4758188c6f2dd7f15303564
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121400889"
---
# <a name="target-a-previous-version-when-creating-an-extension-in-visual-studio-2022-preview"></a>在 2022 预览版中创建扩展时，Visual Studio以前的版本

[!INCLUDE [preview-note](../includes/preview-note.md)]

使用 Visual Studio 2022 预览版创建新的 VSIX 项目时，该项目从面向 Visual Studio 2022 的模板创建。 如果要以 2019 Visual Studio版本为目标，则必须修改创建的项目。

考虑使用[共享项目](update-visual-studio-extension.md#use-shared-projects-for-multi-targeting)面向 Visual Studio 2019 和 Visual Studio 2022，同时共享扩展中的大部分或所有代码。

在应面向 2019 年 1 月Visual Studio VSIX 项目执行以下步骤：

1. 编辑 `source.extension.vsixmanifest` 文件以删除 `ProductArchitecture` 元素和版本范围：

    ```diff
    -<InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
    +<InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[16.0,17.0)">
    -  <ProductArchitecture>amd64</ProductArchitecture>
     </InstallationTarget>
    ```

   另请更新先决条件：

    ```diff
    -<Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[17.0,18.0)" DisplayName="Visual Studio core editor" />
    +<Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[16.0,17.0)" DisplayName="Visual Studio core editor" />
    ```

    查看文件，查看可能需要的其他任何更新。

1. 更改在项目文件中引用的 VS SDK 包的版本：

    ```diff
    -<PackageReference Include="Microsoft.VisualStudio.SDK" Version="17.0.0-preview.1" />
    +<PackageReference Include="Microsoft.VisualStudio.SDK" Version="16.0.206" />
    -<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="17.0.63-preview.1" />
    +<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="16.10.32" />
    ```
