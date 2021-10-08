---
title: 如何：将项目配置为面向平台
description: 了解如何使用 Visual Studio 将应用程序设置为面向不同平台（包括 64 位平台）。
ms.custom: SEO-VS-2020
ms.date: 09/13/2021
ms.technology: vs-ide-compile
ms.topic: how-to
helpviewer_keywords:
- project settings [Visual Studio], targeting platforms
- platforms, targeting specific CPUs
- project properties [Visual Studio], targeting platforms
- projects [Visual Studio], targeting platforms
- 64-bit [Visual Studio]
- 64-bit programming [Visual Studio]
- CPUs, targeting specific
- 64-bit applications [Visual Studio]
ms.assetid: 845302fc-273d-4f81-820a-7296ce91bd76
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b74eb7d0220867b80337b89ef70506bac31b7f6a
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128429012"
---
# <a name="how-to-configure-projects-to-target-platforms"></a>如何：将项目配置为面向平台

可使用 Visual Studio 将应用程序版本设置为面向不同平台（包括 64 位平台）。 若要深入了解 Visual Studio 中对 64 位平台的支持，请参阅 [64 位应用程序](/dotnet/framework/64-bit-apps)。

::: moniker range="vs-2022"
> [!NOTE]
> Visual Studio 2022 预览版作为 64 位应用程序运行。 这完全独立于可以在 Visual Studio 中针对你的项目面向的平台。 可以使用任何版本的 Visual Studio 同时面向 32 位和 64 位平台。
::: moniker-end
::: moniker range="<=vs-2019"
> [!NOTE]
> Visual Studio 作为 32 位应用程序运行。 这完全独立于可以在 Visual Studio 中针对你的项目面向的平台。 可以使用任何版本的 Visual Studio 同时面向 32 位和 64 位平台。
::: moniker-end

## <a name="target-platforms-with-the-configuration-manager"></a>使用 Configuration Manager 设定目标平台

“配置管理器”提供了一种快速添加面向项目的新平台的方法。 如果选择 Visual Studio 附带的平台之一，则将修改项目属性，以便生成适用于所选平台的项目。

### <a name="to-configure-a-project-to-target-a-64-bit-platform"></a>将项目配置为面向 64 位平台

1. 在菜单栏上，依次选择“生成” > “Configuration Manager” 。

2. 在“活动解决方案平台”列表中，选择一个 64 位平台作为解决方案目标，然后选择“关闭”按钮。

    1. 如果所需平台未出现在“活动解决方案平台”列表中，请选择“新建” 。

         将显示“新建解决方案平台”对话框。

    2. 在“键入或选择新平台”列表中，选择“x64”。

        > [!NOTE]
        > 如果对配置进行了重命名，则可能需要修改“项目设计器”中的设置，以面向正确的平台。

    3. 如果要复制当前平台配置的设置，请选择它，然后选择“确定”按钮。

你的解决方案中面向 64 位平台的所有项目的属性均已更新，并将为 64 位平台优化项目的下一个生成。

> [!NOTE]
> Win32 平台名称用于 C++ 项目，这意味着 x86。 Visual Studio 同时考虑项目级平台和解决方案级平台，并且项目平台来自特定于语言的项目系统。 C++ 项目使用 Win32 和 x64，但解决方案平台使用 x86 和 x64。 选择 x86 作为解决方案配置时，Visual Studio 将为 C++ 项目选择 Win32 平台。 若要查看项目级平台和解决方案级平台设置，请打开“Configuration Manager”并记下这两个平台设置。 解决方案级平台显示在“活动解决方案平台”下拉列表中，表显示每个项目的项目级平台。
> ![显示解决方案平台和项目平台的屏幕截图](media/project-platform-win32.png)

## <a name="target-platforms-in-the-project-designer"></a>在项目设计器中设定平台目标

项目设计器还提供使项目面向不同平台的方法。 如果在“新建解决方案平台”对话框的列表中选择的平台之一不适合自己的解决方案，则可以创建自定义配置名称并修改“项目设计器”中的配置以面向正确的平台。

此任务的执行根据所用编程语言而有所不同。 有关详细信息，请参阅以下链接：

- 对于 Visual Basic 项目，请参阅 [/platform (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/platform)。

- 对于 C# 项目，请参阅[“项目设计器”->“生成”页 (C#)](../ide/reference/build-page-project-designer-csharp.md)。

- 对于 C++/CLI 项目，请参阅 [/clr（公共语言运行时编译）](/cpp/build/reference/clr-common-language-runtime-compilation)。

## <a name="manually-editing-the-project-file"></a>手动编辑项目文件

有时，需要手动编辑项目文件以进行某些自定义配置。 例如，当你有无法在 IDE 中指定的条件（例如对两个不同平台而言不同的引用）时，如以下示例所示。

### <a name="example-referencing-x86-and-x64-assemblies-and-dlls"></a>示例：引用 x86 和 x64 程序集和 DLL

你可能拥有同时具有 x86 和 x64 版本的 .NET 程序集或 DLL。 若要将项目设置为使用这些引用，请先添加引用，然后打开项目文件并对其进行编辑，以添加具有同时引用配置和目标平台的条件的 `ItemGroup`。  例如，假设引用的二进制文件是 ClassLibrary1，并且调试和发布配置以及 x86 和 x64 版本有不同路径。  然后，使用四个包含所有设置组合的 `ItemGroup` 元素，如下所示：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.0</TargetFramework>
    <Platforms>AnyCPU;x64;x86</Platforms>
  </PropertyGroup>

  <ItemGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x64'">
    <Reference Include="ClassLibrary1">
      <HintPath>..\..\ClassLibrary1\ClassLibrary1\bin\x64\Debug\netstandard2.0\ClassLibrary1.dll</HintPath>
    </Reference>
  </ItemGroup>

  <ItemGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|x64'">
    <Reference Include="ClassLibrary1">
      <HintPath>..\..\ClassLibrary1\ClassLibrary1\bin\x64\Release\netstandard2.0\ClassLibrary1.dll</HintPath>
    </Reference>
  </ItemGroup>

  <ItemGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x86'">
    <Reference Include="ClassLibrary1">
      <HintPath>..\..\ClassLibrary1\ClassLibrary1\bin\x86\Debug\netstandard2.0\ClassLibrary1.dll</HintPath>
    </Reference>
  </ItemGroup>
  
  <ItemGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|x86'">
    <Reference Include="ClassLibrary1">
      <HintPath>..\..\ClassLibrary1\ClassLibrary1\bin\x86\Release\netstandard2.0\ClassLibrary1.dll</HintPath>
    </Reference>
  </ItemGroup>
</Project>
```

::: moniker range="vs-2017"
> [!NOTE]
> 在 Visual Studio 2017 中，需要先卸载项目，然后才能编辑项目文件。 若要卸载项目，请右键单击项目节点，然后选择“卸载项目”。 完成编辑后，请右键单击项目节点并选择“重新加载项目”，以保存所做的更改并重新加载项目。
::: moniker-end

有关项目文件的详细信息，请参阅 [MSBuild 项目文件架构引用](../msbuild/msbuild-project-file-schema-reference.md)。

## <a name="see-also"></a>请参阅

- [了解生成平台](../ide/understanding-build-platforms.md)
- [/platform（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/platform-compiler-option)
- [64 位应用程序](/dotnet/framework/64-bit-apps)
- [Visual Studio IDE 64 位支持](../ide/visual-studio-ide-64-bit-support.md)
- [了解项目文件](/aspnet/web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file)
