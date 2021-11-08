---
title: Visual Studio 2022 中创建扩展时的目标 Visual Studio 2019
description: 如果使用 Visual Studio 2022 创建项目，则了解如何使 Visual Studio 扩展与 Visual Studio 2019 一起工作。
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
ms.openlocfilehash: 448d615dab608a1f4a86fa2a36572163bb305da7
ms.sourcegitcommit: 67dc39e93c86ba50eb5ca877b0471fb8ab8475ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2021
ms.locfileid: "132001538"
---
# <a name="target-a-previous-version-when-creating-an-extension-in-visual-studio-2022"></a>在 Visual Studio 2022 中创建扩展时面向以前的版本

[!INCLUDE [preview-note](../includes/preview-note.md)]

使用 Visual Studio 2022 创建新的 VSIX 项目时，将从以 Visual Studio 2022 为目标的模板创建项目。 如果要以 Visual Studio 2019 或更早版本为目标，则必须修改创建的项目。

在共享扩展中的大多数或全部代码时，请考虑使用[共享项目](update-visual-studio-extension.md#use-shared-projects-for-multi-targeting)以 Visual Studio 2019 和 Visual Studio 2022 为目标。

在应针对 Visual Studio 2019 的 VSIX 项目上执行以下步骤：

1. 编辑 `source.extension.vsixmanifest` 文件以删除 `ProductArchitecture` 元素和版本范围：

    ```diff
    -<InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
    +<InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[16.0,17.0)">
    -  <ProductArchitecture>amd64</ProductArchitecture>
     </InstallationTarget>
    ```

   还要更新必备组件：

    ```diff
    -<Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[17.0,18.0)" DisplayName="Visual Studio core editor" />
    +<Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[16.0,17.0)" DisplayName="Visual Studio core editor" />
    ```

    检查文件中是否有任何其他可能需要的更新。

1. 更改在项目文件中引用的 VS SDK 包的版本：

    ```diff
    -<PackageReference Include="Microsoft.VisualStudio.SDK" Version="17.0.0-preview.1" />
    +<PackageReference Include="Microsoft.VisualStudio.SDK" Version="16.0.206" />
    -<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="17.0.63-preview.1" />
    +<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="16.10.32" />
    ```
