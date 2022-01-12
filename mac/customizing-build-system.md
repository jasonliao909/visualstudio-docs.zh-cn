---
title: 自定义生成系统
description: 本文简要介绍 Visual Studio for Mac 使用的 MSBuild 生成系统
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 09/19/2019
ms.topic: conceptual
ms.assetid: 6958B102-8527-4B40-BC65-3505DB63F9D3
ms.openlocfilehash: b8521a3f962950999c77301fe5034b21536696d3
ms.sourcegitcommit: 965372ad0d75f015403c1af508080bf799914ce3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "135803201"
---
# <a name="customizing-the-build-system"></a>自定义生成系统

Microsoft 生成引擎是一个用于生成应用程序的平台。 该引擎（也称为 MSBuild）是由 Microsoft 开发的，可用于生成 .NET 应用程序。 Mono 框架也有自己的 Microsoft 生成引擎实现，被称为“xbuild”。 但目前 xbuild 已被淘汰，改而支持在所有操作系统上使用 MSBuild。

MSBuild 用作 Visual Studio for Mac 中项目的生成系统，其工作原理是获取一组输入（例如，源文件）并将其转换为输出（例如，可执行文件）。 它通过调用编译器等工具获取此输出。

## <a name="msbuild-file"></a>MSBuild 文件

MSBuild 使用 XML 文件作为项目文件，该文件定义项目（如图像资源）中的“项”  和生成项目所需的“属性”  。 该项目文件总是以 `proj` 文件扩展名结尾，例如：C# 项目的 `.csproj`。

### <a name="viewing-the-msbuild-file"></a>查看 MSBuild 文件

可通过右键单击项目名称并选择“在查找器中展现”  定位 MSBuild 文件。 查找器窗口将显示和项目有关的所有文件和文件夹，包括 `.csproj` 文件，如下图所示：

![查找器中的 csproj 位置](media/customizing-build-system-image1.png)

通过右键单击项目名称并浏览到“工具”>“编辑文件”，在 Visual Studio for Mac 中新建的选项卡中显示 `.csproj`：

![在源代码编辑器中打开 csproj](media/customizing-build-system-image2.png)

### <a name="composition-of-the-msbuild-file"></a>MSBuild 文件的构成

所有 MSBuild 文件都包含必需的根元素 `Project`，如下所示：

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="14.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
</Project>
```

通常情况下，项目还将导入一个 `.targets` 文件。 该文件包含众多描述如何处理和生成各种文件的规则。 此导入常常出现在 `proj` 文件底部附近，在 C# 项目则如下所示：

```xml
<Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
```

目标文件是另一个 MSBuild 文件。 此文件包含可被多个项目重复使用的 MSBuild 代码。 例如，`Microsoft.CSharp.targets` 文件（位于由 `MSBuildBinPath` 属性（或变量）表示的目录中）包含从 C# 源文件生成 C# 程序集的逻辑。

### <a name="items-and-properties"></a>项和属性

MSBuild 有两种基础数据类型：“项”  和“属性”  ，下列部分将详细介绍这两种类型。

#### <a name="properties"></a>属性

属性是键/值对，用来存储影响编译的设置（如编译器选项）。

属性使用 PropertyGroup 进行设置，且可以包含任意数量的 PropertiesGroup，而 PropertiesGroup 又可以包含任意数量的属性。

例如，简单的控制台应用程序的 PropertyGroup 可能如以下 XML 所示：

```xml
<PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Platform Condition=" '$(Platform)' == '' ">x86</Platform>
    <ProjectGuid>{E248730E-1393-43CC-9183-FFA42F63BE81}</ProjectGuid>
    <OutputType>Exe</OutputType>
    <RootNamespace>refactoring</RootNamespace>
    <AssemblyName>refactoring</AssemblyName>
    <TargetFrameworkVersion>v4.5</TargetFrameworkVersion>
</PropertyGroup>
```

可在使用 `$()` 语法的表达式中引用属性。 例如，`$(Foo)` 将被评估为 `Foo` 属性的值。 如果还未设置该属性，则其将被视为空字符串，不会出现任何错误。

#### <a name="items"></a>Items

项提供一种将输入作为列表或集处理到生成系统的方法，同时通常代表文件。 每个项都有项类型  、项规范  和可选任意元数据  。 请注意，MSBuild 不对单个项进行操作，而是对给定类型的所有项（称为项集）进行操作 

可通过声明 `ItemGroup` 创建项。 可以有任意数量的 ItemGroup，后者也可以包含任意数量的项。

例如，以下代码片段创建 iOS 启动屏幕。 启动屏幕具有生成类型 `BundleResource`，将 spec 作为映像的路径：

```xml
 <ItemGroup>
    <BundleResource Include="Resources\Default-568h%402x.png" />
    <BundleResource Include="Resources\Default%402x.png" />
    <BundleResource Include="Resources\Default.png" />
    <BundleResource Include="Resources\Default-Portrait.png" />
    <BundleResource Include="Resources\Default-Portrait%402x.png" />
    <BundleResource Include="Resources\Default-Landscape%402x.png" />
  </ItemGroup>
 ```

 可在使用 `@()` 语法的表达式中引用项集。 例如，`@(BundleResource)` 将被评估为 BundleResource 项集，即所有 BundleResource 项。 如果没有此类型的项，则其将为空，且不会有任何错误。

## <a name="resources-for-learning-msbuild"></a>MSBuild 的介绍性资源

以下资源可用来了解 MSBuild 的详细信息：

* [MSBuild 概述](/visualstudio/msbuild/msbuild)
* [MSBuild 概念](/visualstudio/msbuild/msbuild-concepts)
