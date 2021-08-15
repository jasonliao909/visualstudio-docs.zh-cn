---
title: Visual Studio 2017 扩展性中的重大更改
description: 了解 Visual Studio 2017 中对扩展性模型所做的重大更改的技术详细信息以及解决这些问题的方法。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 54d5af60-0b44-4ae1-aa57-45aa03f89f3d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: de83f2504f6810b00265b0abf7b4630e3e0c4cc2a1da98931a0518c4dd3ea12b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121308371"
---
# <a name="changes-in-visual-studio-2017-extensibility"></a>Visual Studio 2017 扩展性中的更改

Visual Studio 2017 提供了[更快、更轻量的 Visual Studio 安装体验](https://devblogs.microsoft.com/visualstudio/faster-leaner-visual-studio-installer)，从而降低了 Visual Studio 用户系统的影响，同时使用户能够更好地选择所安装的工作负载和功能。 为了支持这些改进，我们对扩展性模型进行了更改，包括一些重大更改。 本文介绍了这些更改的技术详细信息以及解决这些更改可以执行的操作。

> [!NOTE]
> 某些信息是时间点实现细节，以后可能会更改。

## <a name="changes-affecting-vsix-format-and-installation"></a>影响 VSIX 格式和安装的更改

Visual Studio 2017 引入了 VSIX v3 (版本 3) 格式以支持轻型安装体验。

对 VSIX 格式的更改包括：

* 安装必备组件的声明。 为满足轻型、快速安装 Visual Studio 的承诺，安装程序现在为用户提供了更多的配置选项。 因此，为了确保安装了扩展所需的功能和组件，扩展需要声明其依赖项。

  * Visual Studio 2017 安装程序自动提供为用户获取和安装所需的组件，作为安装扩展的一部分。
  * 当尝试安装不是使用新的 VSIX v3 格式生成的扩展时，也会发出警告，即使已在其清单中将其标记为面向版本15.0。

* VSIX 格式的增强功能。 为了提供对同时支持并行安装的 Visual Studio 的[影响较小的安装](https://devblogs.microsoft.com/visualstudio/anatomy-of-a-low-impact-visual-studio-install)，我们不再会将大多数配置数据保存到系统注册表中，并已将特定于 Visual Studio 的程序集移出 GAC。 我们还增加了 VSIX 格式和 VSIX 安装引擎的功能，使你可以使用它而不是 MSI 或 EXE 为某些安装类型安装扩展。

新功能包括：

* 注册到指定的 Visual Studio 实例中。
* 在 [extensions 文件夹](set-install-root.md)外部安装。
* 检测处理器体系结构。
* 依赖于语言的语言包。
* 具有 [NGEN 支持](ngen-support.md)的安装。

## <a name="build-an-extension-for-visual-studio-2017"></a>为 Visual Studio 2017 生成扩展

Visual Studio 2017 中提供了用于创作新的 VSIX v3 清单格式的设计器工具。 请参阅随附文档[如何：将扩展性项目迁移到 Visual Studio 2017](how-to-migrate-extensibility-projects-to-visual-studio-2017.md) ，以了解有关使用设计器工具或手动更新项目和清单以开发 VSIX v3 扩展的详细信息。

## <a name="change-visual-studio-user-data-path"></a>更改： Visual Studio 用户数据路径

以前，每台计算机上只能有一次安装 Visual Studio 的每个主版本。 为了支持 Visual Studio 2017 的并行安装，用户计算机上可能存在 Visual Studio 的多个用户数据路径。

应更新 Visual Studio 进程内运行的代码，使其使用 Visual Studio 设置管理器。 在 Visual Studio 进程外部运行的代码可按照[此处的指南](locating-visual-studio.md)查找特定 Visual Studio 安装的用户路径。

## <a name="change-global-assembly-cache-gac"></a>Change：全局程序集缓存 (GAC) 

大多数 Visual Studio 核心程序集不再安装到 GAC 中。 进行了以下更改，以便 Visual Studio 进程中运行的代码在运行时仍可找到所需的程序集。

> [!NOTE]
> [INSTALLDIR] 下面是指 Visual Studio 的安装根目录。 *VSIXInstaller.exe* 将自动填充此代码，但要编写自定义部署代码，请阅读 [查找 Visual Studio](locating-visual-studio.md)。

* 仅安装到 GAC 中的程序集：

  这些程序集现在安装在 <em>[INSTALLDIR] \Common7\IDE \* 、* [INSTALLDIR] \Common7\IDE\PublicAssemblies</em> 或 *[INSTALLDIR] \Common7\IDE\PrivateAssemblies* 下。 这些文件夹是 Visual Studio 进程的探测路径的一部分。

* 安装到非探测路径和 GAC 中的程序集：

  * GAC 中的副本已从安装程序中删除。
  * 添加了 *.pkgdef* 文件以指定程序集的基本代码项。

    例如：

    ```
    [$RootKey$\RuntimeConfiguration\dependentAssembly\codeBase\{UniqueGUID}]
    "name"="AssemblyName" "codeBase"="$PackageFolder$\AssemblyName.dll"
    "publicKeyToken"="Public Key Token"
    "culture"="neutral"
    "version"=15.0.0.0
    ```

    在运行时，Visual Studio 的 .pkgdef 子系统将这些项合并到 Visual Studio 进程的运行时配置文件中 (*[VSAPPDATA] \devenv.exe.config*) 作为 [`<codeBase>`](/dotnet/framework/configure-apps/file-schema/runtime/codebase-element) 元素。 这是允许 Visual Studio 进程查找程序集的建议方法，因为这样可以避免搜索探测路径。

### <a name="reacting-to-this-breaking-change"></a>应对此重大更改

* 如果扩展正在 Visual Studio 过程中运行：

  * 你的代码将能够查找 Visual Studio 核心程序集。
  * 如果需要，请考虑使用 *.pkgdef* 文件指定程序集的路径。

* 如果扩展在 Visual Studio 进程外运行：

  请考虑使用配置文件或程序集冲突解决程序查找 <em>[INSTALLDIR] \Common7\IDE \* 、* [INSTALLDIR] \Common7\IDE\PublicAssemblies</em>或 *[INSTALLDIR] \Common7\IDE\PrivateAssemblies* 下的 Visual Studio 核心程序集。

## <a name="change-reduce-registry-impact"></a>更改：降低注册表影响

### <a name="global-com-registration"></a>全局 COM 注册

* 以前，Visual Studio 在 HKEY_CLASSES_ROOT 中安装了多个注册表项，并 HKEY_LOCAL_MACHINE 配置单元来支持本机 COM 注册。 为了消除这种影响，Visual Studio 现在使用[COM 组件无注册激活](/previous-versions/dotnet/articles/ms973913(v=msdn.10))。
* 因此，默认情况下，Visual Studio (x86) % \ Common Files\Microsoft Shared\MSEnv 下的大多数 TLB/.OLB/DLL 文件不再安装。 这些文件现在安装在 [INSTALLDIR] 下，并附带 Visual Studio 主机进程使用的相应 Registration-Free COM 清单。
* 因此，依赖于 Visual Studio COM 接口的全局 COM 注册的外部代码将不再查找这些注册。 在 Visual Studio 进程内运行的代码看不到差异。

### <a name="visual-studio-registry"></a>Visual Studio 注册表

* 以前，Visual Studio 将多个注册表项安装到系统的 **HKEY_LOCAL_MACHINE** 中，并在 Visual Studio 特定的密钥下 **HKEY_CURRENT_USER** 配置单元：

  * **HKLM\Software\Microsoft\VisualStudio \{Version}**：由 MSI 安装程序和每台计算机扩展创建的注册表项。
  * **HKCU\Software\Microsoft\VisualStudio \{Version}**： Visual Studio 创建的注册表项，用于存储特定于用户的设置。
  * **HKCU\Software\Microsoft\VisualStudio \{版本} _Config**：上面 Visual Studio HKLM 密钥的副本，以及从 *.pkgdef* 文件按扩展名合并的注册表项。

* 为了降低对注册表的影响，Visual Studio 现在使用 [RegLoadAppKey](/windows/desktop/api/winreg/nf-winreg-regloadappkeya)函数将注册表项存储在 *[VSAPPDATA] \privateregistry.bin* 下的专用二进制文件中。 系统注册表中仅保留一小部分 Visual Studio 特定的键。
* Visual Studio 进程内运行的现有代码不受影响。 Visual Studio 会将 HKCU Visual Studio 特定密钥下的所有注册表操作重定向到专用注册表。 读取和写入到其他注册表位置将继续使用系统注册表。
* 外部代码将需要在此文件中加载和读取 Visual Studio 注册表项。

### <a name="react-to-this-breaking-change"></a>React 此重大更改

* 应将外部代码转换为使用 Registration-Free 的 COM 组件激活。
* 外部组件可按照[此处的指南](https://devblogs.microsoft.com/setup/changes-to-visual-studio-15-setup)查找 Visual Studio 位置。
* 建议外部组件使用[外部设置管理器](/dotnet/api/microsoft.visualstudio.settings.externalsettingsmanager)，而不是直接读取/写入 Visual Studio 注册表项。
* 检查扩展所使用的组件是否可能已实现了另一种注册技术。 例如，调试器扩展或许能够利用新的 [MSVSMON JSON 文件 COM 注册](migrate-debugger-COM-registration.md)。