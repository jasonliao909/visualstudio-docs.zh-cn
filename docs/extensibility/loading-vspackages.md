---
title: 加载 VSPackages |Microsoft Docs
description: 了解如何在 Visual Studio加载 VSPackage，包括延迟加载，尽可能使用延迟加载来提高性能。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, loading
ms.assetid: f4c3dcea-5051-4065-898f-601269649d92
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: d56192fed9138e6edd8f18753893b195c174c5b9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122041719"
---
# <a name="load-vspackages"></a>加载 VSPackage
只有在需要 VSPackage Visual Studio，VSPackage 才加载到该组件中。 例如，当 VSPackage 使用项目工厂Visual Studio VSPackage 实现的服务时，将加载 VSPackage。 此功能称为延迟加载，它尽可能用于提高性能。

> [!NOTE]
> Visual Studio可以确定某些 VSPackage 信息，例如 VSPackage 提供的命令，而无需加载 VSPackage。

 VSPackages 可以设置为在 UI 环境上下文中 (用户界面) 自动加载，例如，当解决方案打开时。 <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>属性设置此上下文。

### <a name="autoload-a-vspackage-in-a-specific-context"></a>自动加载特定上下文中的 VSPackage

- 将 `ProvideAutoLoad` 属性添加到 VSPackage 属性：

    ```csharp
    [DefaultRegistryRoot(@"Software\Microsoft\VisualStudio\14.0")]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid("00000000-0000-0000-0000-000000000000")] // your specific package GUID
    public class MyAutoloadedPackage : Package
    {. . .}
    ```

     有关 UI 上下文及其 <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> GUID 值的列表，请参阅 的枚举字段。

- 在 方法中设置 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 断点。

- 生成 VSPackage 并开始调试。

- 加载解决方案或创建一个解决方案。

     VSPackage 在断点处加载和停止。

## <a name="force-a-vspackage-to-load"></a>强制加载 VSPackage
 在某些情况下，VSPackage 可能需要强制加载另一个 VSPackage。 例如，轻型 VSPackage 可能在无法作为 CMDUIContext 提供的上下文中加载更大的 VSPackage。

 可以使用 方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackage%2A> 强制加载 VSPackage。

- 将以下代码插入到 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 强制加载另一个 VSPackage 的 VSPackage 的 方法中：

    ```csharp
    IVsShell shell = GetService(typeof(SVsShell)) as IVsShell;
    if (shell == null) return;

    IVsPackage package = null;
    Guid PackageToBeLoadedGuid =
        new Guid(Microsoft.PackageToBeLoaded.GuidList.guidPackageToBeLoadedPkgString);
    shell.LoadPackage(ref PackageToBeLoadedGuid, out package);

    ```

     初始化 VSPackage 时，它将强制 `PackageToBeLoaded` 加载。

     不应将强制加载用于 VSPackage 通信。 请 [改为使用 并提供](../extensibility/using-and-providing-services.md) 服务。

## <a name="see-also"></a>请参阅
- [VSPackages](../extensibility/internals/vspackages.md)
