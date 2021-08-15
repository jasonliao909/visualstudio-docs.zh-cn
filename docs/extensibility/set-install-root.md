---
title: 通过 VSIX v3 在 extension 文件夹外安装 |Microsoft Docs
description: 了解如何在 extension 文件夹之外安装 Visual Studio SDK 扩展资产以及哪些位置是有效的。
ms.custom: SEO-VS-2020
ms.date: 11/09/2016
ms.topic: how-to
ms.assetid: 913c3745-8aa9-4260-886e-a05aecfb2225
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 145fb9e4b94bb641ae0f491a09bc5b5c3cd0bc20bc8d9b2cc76c85e65170fa28
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121431486"
---
# <a name="install-outside-the-extensions-folder"></a>在扩展文件夹外进行安装

从 Visual Studio 2017 和 VSIX v3 (版本 3) 开始，扩展资产可安装在 extension 文件夹之外。 目前，以下位置将作为 (的有效安装位置启用，其中 [INSTALLDIR] 映射到 Visual Studio 实例的安装目录) ：

* [INSTALLDIR] \ MSBuild
* [INSTALLDIR] \Xml\Schemas
* [INSTALLDIR] \Common7\IDE\PublicAssemblies
* [INSTALLDIR] \Licenses
* [INSTALLDIR] \Common7\IDE\ReferenceAssemblies
* [INSTALLDIR] \Common7\IDE\RemoteDebugger
* [INSTALLDIR] \Common7\IDE\VC\VCTargets (仅支持 Visual Studio 2017;Visual Studio 2019 及更高版本弃用) 

> [!NOTE]
> VSIX 格式不允许在 Visual Studio 安装文件夹结构的外部安装。 

若要支持安装到这些目录，必须在 "每个实例每台计算机" 上安装 VSIX。 可以通过选中 source.extension.vsixmanifest 设计器中的 "所有用户" 复选框来启用此功能：

![检查所有用户](media/check-all-users.png)

## <a name="how-to-set-the-installroot"></a>如何设置 InstallRoot

若要设置安装目录，可以使用 Visual Studio 中的 "**属性**" 窗口。 例如，可以将 `InstallRoot` 项目引用的属性设置为上述位置之一：

![安装根属性](media/install-root-properties.png)

这会将某些元数据添加到 `ProjectReference` VSIX 项目的 .csproj 文件中的相应属性：

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
        <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
        <Name>ClassLibrary1</Name>
        <InstallRoot>PublicAssemblies</InstallRoot>
 </ProjectReference>
```

> [!NOTE]
> 如果愿意，可以直接编辑 .csproj 文件。

## <a name="how-to-set-a-subpath-under-the-installroot"></a>如何在 InstallRoot 下设置子路径

如果要将安装到下的子路径 `InstallRoot` ，可以通过设置属性来实现此操作，就 `VsixSubPath` 像属性一样 `InstallRoot` 。 例如，假设要将项目引用的输出安装到 "[INSTALLDIR] \ MSBuild \MyCompany\MySDK\1.0"。 可以通过属性设计器轻松实现此目的：

![设置子路径](media/set-subpath.png)

对应的 .csproj 更改将如下所示：

```xml
<ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
       <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
       <Name>ClassLibrary1</Name>
       <InstallRoot>MSBuild</InstallRoot>
       <VSIXSubPath>MyCompany\MySDK\1.0</VSIXSubPath>
</ProjectReference>
```

## <a name="extra-information"></a>额外的信息

属性设计器的更改仅适用于项目引用;你 `InstallRoot` 还可以使用上述) 的相同方法，设置项目内项的元数据 (。
