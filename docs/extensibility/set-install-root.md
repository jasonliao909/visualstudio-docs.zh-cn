---
title: 在扩展文件夹外部安装 VSIX v3 |Microsoft Docs
description: 了解如何在扩展Visual Studio外部安装 SDK 扩展资产，以及哪些位置有效。
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

从 Visual Studio 2017 和 VSIX v3 (版本 3) 开始，扩展资产可以安装在 extensions 文件夹之外。 目前，以下位置作为有效的安装位置启用 (其中 [INSTALLDIR] 映射到 Visual Studio 实例的安装目录) ：

* [INSTALLDIR]\MSBuild
* [INSTALLDIR]\Xml\Schemas
* [INSTALLDIR]\Common7\IDE\PublicAssemblies
* [INSTALLDIR]\Licenses
* [INSTALLDIR]\Common7\IDE\ReferenceAssemblies
* [INSTALLDIR]\Common7\IDE\RemoteDebugger
* [INSTALLDIR]\Common7\IDE\VC\VCTargets (仅支持 Visual Studio 2017;2019 Visual Studio及更高版本已弃) 

> [!NOTE]
> VSIX 格式不允许在安装文件夹结构Visual Studio外部安装。 

为了支持安装到这些目录，必须"每台计算机按实例"安装 VSIX。 可以通过选中 extension.vsixmanifest 设计器中的"所有用户"复选框来启用此功能：

![检查所有用户](media/check-all-users.png)

## <a name="how-to-set-the-installroot"></a>如何设置 InstallRoot

若要设置安装目录，可以使用"属性 **"** 窗口Visual Studio。 例如，可以将项目 `InstallRoot` 引用的 属性设置为上述位置之一：

![安装根属性](media/install-root-properties.png)

这会将一些元数据添加到 `ProjectReference` VSIX 项目的 .csproj 文件内的相应属性：

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
        <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
        <Name>ClassLibrary1</Name>
        <InstallRoot>PublicAssemblies</InstallRoot>
 </ProjectReference>
```

> [!NOTE]
> 如果需要，可以直接编辑 .csproj 文件。

## <a name="how-to-set-a-subpath-under-the-installroot"></a>如何在 InstallRoot 下设置子路径

如果要安装到 下的子路径，可以通过像设置 属性一样设置 属性 `InstallRoot` `VsixSubPath` 来 `InstallRoot` 这样做。 例如，假设我们希望项目引用的输出安装到"[INSTALLDIR]\MSBuild\MyCompany\MySDK\1.0"。 可以使用属性设计器轻松完成此操作：

![set 子路径](media/set-subpath.png)

相应的 .csproj 更改将如下所示：

```xml
<ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
       <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
       <Name>ClassLibrary1</Name>
       <InstallRoot>MSBuild</InstallRoot>
       <VSIXSubPath>MyCompany\MySDK\1.0</VSIXSubPath>
</ProjectReference>
```

## <a name="extra-information"></a>额外的信息

属性设计器更改仅适用于项目引用;可以使用上述方法设置项目中项的元数据， (`InstallRoot` 上述方法) 。
