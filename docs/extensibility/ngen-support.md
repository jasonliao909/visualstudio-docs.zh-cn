---
title: VSIX v3 中的 Ngen 支持|Microsoft Docs
description: 了解如何启用本机映像生成器，这是扩展开发人员可用于提高托管应用程序性能的工具。
ms.custom: SEO-VS-2020
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 1472e884-c74e-4c23-9d4a-6d8bdcac043b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 0ca58451057c1cea15e0e99ff221595d525c1732
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122094563"
---
# <a name="ngen-support-in-vsix-v3"></a>VSIX v3 中的 Ngen 支持

使用 Visual Studio 2017 和新的 VSIX v3 (版本 3) 扩展清单格式，扩展开发人员现在可以在安装时"ngen"其程序集。

下面是 MSDN 的摘录，其中解释了"ngen"有什么功能：

>本机映像生成器 *(Ngen.exe)* 是一种提高托管应用程序性能的工具。 *Ngen.exe* 创建本机映像，即包含编译处理器特定计算机代码的文件，并安装到本地计算机的本机映像缓存中。 运行时可从缓存中使用本机映像，而不必使用实时 (JIT) 编译器编译原始程序集。
>
>从 [Ngen.exe (本机映像生成器) ](/dotnet/framework/tools/ngen-exe-native-image-generator)

若要"ngen"程序集，必须"每台计算机每实例"安装 VSIX。 可以通过选中设计器中的"所有用户"复选框来启用 `extension.vsixmanifest` 此功能：

![检查所有用户](media/check-all-users.png)

## <a name="how-to-enable-ngen"></a>如何启用 Ngen

若要为程序集启用 ngen，可以使用程序集 **中的"属性**"Visual Studio。

可以设置 4 个属性：

1. **Ngen** (布尔) - 如果为 true，则Visual Studio安装程序将"ngen"程序集。
2. **Ngen 应用程序** (字符串) - Ngen 提供了使用应用程序的app.config *文件来* 解析程序集依赖项的机会。 此值应设置为一个应用程序 *，app.config* 其 (安装目录Visual Studio应用程序) 。
3. **Ngen 体系结构** (枚举) - 本机编译程序集的体系结构。 选项包括：a. NotSpecified b. X86 c. X64 d. 全部
4. **Ngen 优先级** (1 到 3 之间的整数) - Ngen 优先级级别记录在Ngen.exe [ 级别](/dotnet/framework/tools/ngen-exe-native-image-generator#priority-levels)。

下面查看"属性 **"** 窗口的"操作"：

![属性中的 ngen](media/ngen-in-properties.png)

这会将元数据添加到 VSIX 项目的 *.csproj* 文件内的项目引用：

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
    <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
    <Name>ClassLibrary1</Name>
    <Ngen>True</Ngen>
    <NgenApplication>vsn.exe</NgenApplication>
    <NgenArchitecture>X86</NgenArchitecture>
    <NgenPriority>2</NgenPriority>
</ProjectReference>
```

> [!NOTE]
> 如果需要，可以直接编辑 .csproj 文件。

## <a name="extra-information"></a>额外的信息

属性设计器更改仅适用于项目引用;可以使用上述相同方法为项目内的项设置 Ngen 元数据 (，只要这些项是 .NET 程序集) 就可以。
