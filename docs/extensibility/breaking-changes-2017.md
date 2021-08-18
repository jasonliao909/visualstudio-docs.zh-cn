---
title: Visual Studio 2017 扩展性中的中断性变更
description: 了解 2017 年 1 月对扩展性模型Visual Studio的技术详细信息，以及可以执行哪些操作来解决这些问题。
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
ms.openlocfilehash: 00158c527ba4e5ea084836c49c5a8b7f5ba95366
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122051308"
---
# <a name="changes-in-visual-studio-2017-extensibility"></a>2017 Visual Studio扩展性中的更改

Visual Studio 2017 提供了更快、[](https://devblogs.microsoft.com/visualstudio/faster-leaner-visual-studio-installer)更轻Visual Studio的 Visual Studio 安装体验，减少了 Visual Studio 对用户系统的影响，同时为用户提供了对已安装工作负载和功能的更大选择。 为了支持这些改进，我们对扩展性模型进行了更改，包括一些中断性更改。 本文介绍这些更改的技术详细信息，以及可以执行哪些操作来解决这些问题。

> [!NOTE]
> 某些信息是时间点实现详细信息，稍后可能会更改。

## <a name="changes-affecting-vsix-format-and-installation"></a>影响 VSIX 格式和安装的更改

Visual Studio 2017 年 3 月引入了 VSIX v3 (版本 3) ，以支持轻型安装体验。

VSIX 格式的更改包括：

* 设置先决条件的声明。 为了履行轻型快速安装服务的承诺Visual Studio，安装程序现在为用户提供更多配置选项。 因此，为了确保已安装扩展所需的功能和组件，扩展需要声明其依赖项。

  * 2017 Visual Studio 2017 安装程序会自动提供，在安装扩展时为用户获取和安装必要的组件。
  * 尝试安装不是使用新的 VSIX v3 格式构建的扩展时，用户也会受到警告，即使其清单中已将其标记为面向版本 15.0。

* VSIX 格式的增强功能。 为了提供也支持[](https://devblogs.microsoft.com/visualstudio/anatomy-of-a-low-impact-visual-studio-install)并行安装的 Visual Studio 的低影响安装，我们不再将大多数配置数据保存到系统注册表，并且将 Visual Studio 特定的程序集从 GAC 中移开。 我们还增加了 VSIX 格式和 VSIX 安装引擎的功能，允许使用它而不是 MSI 或 EXE 来安装某些安装类型的扩展。

新功能包括：

* 注册到指定的 Visual Studio 实例。
* 在扩展 [文件夹 之外安装](set-install-root.md)。
* 处理器体系结构的检测。
* 依赖于语言分隔的语言包。
* 使用 [NGEN 安装支持](ngen-support.md)。

## <a name="build-an-extension-for-visual-studio-2017"></a>为 2017 Visual Studio扩展

用于创作新的 VSIX v3 清单格式的设计器工具在 2017 Visual Studio中提供。 有关使用设计器工具或手动更新项目和清单以开发 VSIX v3 扩展的详细信息，请参阅随附的文档如何：将扩展性项目迁移到[Visual Studio 2017。](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)

## <a name="change-visual-studio-user-data-path"></a>更改：Visual Studio用户数据路径

以前，每台计算机只能安装一Visual Studio版本的主要版本。 若要支持并行安装 Visual Studio 2017，Visual Studio计算机上可能存在多个用户数据路径。

应更新在 Visual Studio 中运行的代码，以使用 Visual Studio 设置 Manager。 在进程Visual Studio运行的代码可以按照此处的指南Visual Studio特定应用程序安装[的用户路径](locating-visual-studio.md)。

## <a name="change-global-assembly-cache-gac"></a>更改：全局程序集缓存 (GAC) 

大多数Visual Studio核心程序集不再安装到 GAC 中。 进行了以下更改，使在 Visual Studio 中运行的代码仍可以运行时找到所需的程序集。

> [!NOTE]
> [INSTALLDIR] 下面引用了 Visual Studio 的安装根目录。 *VSIXInstaller.exe* 将自动填充此内容，但若要编写自定义部署代码，请阅读 [Visual Studio。](locating-visual-studio.md)

* 仅安装到 GAC 中的程序集：

  这些程序集现在安装在 <em>[INSTALLDIR]\Common7\IDE \* 、*[INSTALLDIR]\Common7\IDE\PublicAssemblies</em> 或 *[INSTALLDIR]\Common7\IDE\PrivateAssemblies* 下。 这些文件夹是进程Visual Studio路径的一部分。

* 安装到非探测路径和 GAC 中的程序集：

  * GAC 中的副本已从安装程序中删除。
  * 添加了 *.pkgdef* 文件以指定程序集的代码基项。

    例如：

    ```
    [$RootKey$\RuntimeConfiguration\dependentAssembly\codeBase\{UniqueGUID}]
    "name"="AssemblyName" "codeBase"="$PackageFolder$\AssemblyName.dll"
    "publicKeyToken"="Public Key Token"
    "culture"="neutral"
    "version"=15.0.0.0
    ```

    在运行时，Visual Studio pkgdef 子系统会将这些条目合并到 Visual Studio 进程的运行时配置文件 (*[VSAPPDATA]下\devenv.exe.config)* [`<codeBase>`](/dotnet/framework/configure-apps/file-schema/runtime/codebase-element) 元素。 这是允许进程查找Visual Studio的建议方法，因为它可以避免通过探测路径进行搜索。

### <a name="reacting-to-this-breaking-change"></a>对此中断性变更做出反应

* 如果扩展在进程内Visual Studio：

  * 代码将能够查找Visual Studio程序集。
  * 如有必要，请考虑使用 *.pkgdef* 文件指定程序集的路径。

* 如果扩展在进程外部Visual Studio：

  请考虑使用配置文件或程序集解析程序在 <em>[INSTALLDIR]\Common7\IDE \* 、 *[INSTALLDIR]\Common7\IDE\PublicAssemblies</em>或 *[INSTALLDIR]\Common7\IDE\PrivateAssemblies* 下查找 Visual Studio 核心程序集。

## <a name="change-reduce-registry-impact"></a>更改：降低注册表影响

### <a name="global-com-registration"></a>全局 COM 注册

* 以前，Visual Studio将许多注册表项安装到 HKEY_CLASSES_ROOT 配置单元HKEY_LOCAL_MACHINE以支持本机 COM 注册。 为了消除这种影响，Visual Studio COM 组件[使用免注册激活](/previous-versions/dotnet/articles/ms973913(v=msdn.10))。
* 因此，默认情况下，%ProgramFiles (x86) %\Common Files\Microsoft Shared\MSEnv 下大多数 TLB/OLB/DLL 文件在 Visual Studio。 这些文件现在安装在 [INSTALLDIR] 下，Registration-Free主机进程使用的对应 COM Visual Studio清单。
* 因此，依赖于 COM 接口的全局 COM 注册的外部Visual Studio将不再查找这些注册。 在进程Visual Studio运行的代码不会看到差异。

### <a name="visual-studio-registry"></a>Visual Studio注册表

* 以前，Visual Studio将许多注册表项安装到系统的 HKEY_LOCAL_MACHINE，HKEY_CURRENT_USER特定密钥下Visual Studio配置单元： 

  * **HKLM\Software\Microsoft\VisualStudio \{Version}**：由 MSI 安装程序和每台计算机扩展创建的注册表项。
  * **HKCU\Software\Microsoft\VisualStudio \{Version}**：由 Visual Studio创建的注册表项，用于存储用户特定的设置。
  * **HKCU\Software\Microsoft\VisualStudio \{Version}_Config：** 上述 HKLM Visual Studio的副本，以及扩展从 *.pkgdef* 文件合并的注册表项。

* 为了减少对注册表的影响，Visual Studio [RegLoadAppKey](/windows/desktop/api/winreg/nf-winreg-regloadappkeya)函数将注册表项存储在 *[VSAPPDATA]\privateregistry.bin* 下的专用二进制文件中。 系统注册表中仅Visual Studio个特定密钥。
* 在进程内部运行Visual Studio代码不会受到影响。 Visual Studio会将 HKCU Visual Studio下的所有注册表操作重定向到专用注册表。 读取和写入其他注册表位置将继续使用系统注册表。
* 外部代码需要从此文件加载和读取Visual Studio注册表项。

### <a name="react-to-this-breaking-change"></a>React此中断性变更

* 还应转换外部代码，Registration-Free COM 组件的激活。
* 外部组件可以按照此处Visual Studio[查找位置](https://devblogs.microsoft.com/setup/changes-to-visual-studio-15-setup)。
* 我们建议外部组件使用 External[设置 Manager，](/dotnet/api/microsoft.visualstudio.settings.externalsettingsmanager)而不是直接读取/写入Visual Studio注册表项。
* 检查扩展使用的组件是否实现了另一种注册技术。 例如，调试器扩展可能能够利用新的 [msvsmon JSON-file COM 注册](migrate-debugger-COM-registration.md)。