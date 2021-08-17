---
title: 注册和注销 Vspackage |Microsoft Docs
description: 了解注册和注销 Vspackage，包括所用的属性和 .pkgdef 文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: e25e7a46-6a55-4726-8def-ca316f553d6b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 77929647b86f5397fa5986f2223b8e52c9d65c86
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122041589"
---
# <a name="register-and-unregister-vspackages"></a>注册和注销 Vspackage
使用特性来注册 VSPackage，但

## <a name="register-a-vspackage"></a>注册 VSPackage
 您可以使用属性来控制托管 Vspackage 的注册。 所有注册信息都包含在一个 *.pkgdef* 文件中。 有关基于文件的注册的详细信息，请参阅 [CreatePkgDef utility](../extensibility/internals/createpkgdef-utility.md)。

 下面的代码演示如何使用标准注册特性来注册你的 VSPackage。

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[Guid("0B81D86C-0A85-4f30-9B26-DD2616447F95")]
public sealed class BasicPackage : Package
{
    // ...
}
```

## <a name="unregister-an-extension"></a>注销扩展
 如果你已经尝试过大量不同的 Vspackage，并想要将它们从实验实例中删除，则可以直接运行 **Reset** 命令。 在计算机的 "开始" 页上查找 **"重置 Visual Studio 实验实例**"，或从命令行运行以下命令：

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe" /Reset /VSInstance=14.0 /RootSuffix=Exp
```

 如果要卸载在 Visual Studio 的开发实例上安装的扩展，请依次  >  单击 "工具" "**扩展和更新**" 和 "**卸载**"。

 如果出于某种原因，这两种方法都不会在卸载扩展时成功完成，您可以从命令行中注销 VSPackage 程序集，如下所示：

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\regpkg" /unregister <pathToVSPackage assembly>
```

<a name="using-a-custom-registration-attribute-to-register-an-extension"></a>

## <a name="use-a-custom-registration-attribute-to-register-an-extension"></a>使用自定义注册特性注册扩展

在某些情况下，可能需要为扩展创建新的注册属性。 您可以使用注册属性来添加新的注册表项，或向现有的键添加新的值。 新特性必须派生自 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> ，并且它必须重写 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A> 和 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A> 方法。

### <a name="create-a-custom-attribute"></a>创建自定义属性

下面的代码演示如何创建新的注册属性。

```csharp
[AttributeUsage(AttributeTargets.Class, Inherited = true, AllowMultiple = false)]
public class CustomRegistrationAttribute : RegistrationAttribute
{
}
```

 <xref:System.AttributeUsageAttribute>用于特性类的指定程序元素 (类、方法等 ) 到特性所属的，是否可以多次使用该元素，以及是否可继承。

### <a name="create-a-registry-key"></a>创建注册表项

在下面的代码中，自定义属性在要注册的 VSPackage 的注册表项下创建一个 **自定义** 子项。

```csharp
public override void Register(RegistrationAttribute.RegistrationContext context)
{
    Key packageKey = null;
    try
    {
        packageKey = context.CreateKey(@"Packages\{" + context.ComponentType.GUID + @"}\Custom");
        packageKey.SetValue("NewCustom", 1);
    }
    finally
    {
        if (packageKey != null)
            packageKey.Close();
    }
}

public override void Unregister(RegistrationContext context)
{
    context.RemoveKey(@"Packages\" + context.ComponentType.GUID + @"}\Custom");
}
```

### <a name="create-a-new-value-under-an-existing-registry-key"></a>在现有注册表项下创建新值

您可以向现有的键添加自定义值。 下面的代码演示如何将新值添加到 VSPackage 注册密钥。

```csharp
public override void Register(RegistrationAttribute.RegistrationContext context)
{
    Key packageKey = null;
    try
    {
        packageKey = context.CreateKey(@"Packages\{" + context.ComponentType.GUID + "}");
        packageKey.SetValue("NewCustom", 1);
    }
    finally
    {
        if (packageKey != null)
            packageKey.Close();
    }
}

public override void Unregister(RegistrationContext context)
{
    context.RemoveValue(@"Packages\" + context.ComponentType.GUID, "NewCustom");
}
```

## <a name="see-also"></a>请参阅
- [VSPackages](../extensibility/internals/vspackages.md)
