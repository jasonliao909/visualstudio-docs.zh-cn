---
title: Otherwise 元素 (MSBuild) | Microsoft Docs
description: 了解 MSBuild 如何使用 Otherwise 元素来指定在当且仅当所有 When 元素的条件都为 false 时执行的代码块。
ms.custom: SEO-VS-2020
ms.date: 03/13/2017
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Otherwise
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <Otherwise> Element [MSBuild]
- Otherwise Element [MSBuild]
ms.assetid: de3997e9-1595-4263-a886-95530b56a319
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: a11331b751a491c3c39562b0b3cd509a5e3d1d9a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736677"
---
# <a name="otherwise-element-msbuild"></a>Otherwise 元素 (MSBuild)

指定当且仅当所有 `When` 元素的条件的计算结果为 `false` 时才执行的代码块。

 \<Project> \<Choose>
 \<When>
 \<Choose>
... \<Otherwise>
 \<Choose>
...

## <a name="syntax"></a>语法

```xml
<Otherwise>
    <PropertyGroup>... </PropertyGroup>
    <ItemGroup>... </ItemGroup>
    <Choose>... </Choose>
</Otherwise>
```

## <a name="attributes-and-elements"></a>特性和元素

 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

 无。

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[Choose](../msbuild/choose-element-msbuild.md)|可选元素。<br /><br /> 评估子元素以选择代码的一部分来执行。 `Choose` 元素中可能有零个或零个以上的 `Otherwise` 元素。|
|[ItemGroup](../msbuild/itemgroup-element-msbuild.md)|可选元素。<br /><br /> 包含一组用户定义的 [Item](../msbuild/item-element-msbuild.md) 元素。 `ItemGroup` 元素中可能有零个或零个以上的 `Otherwise` 元素。|
|[PropertyGroup](../msbuild/propertygroup-element-msbuild.md)|可选元素。<br /><br /> 包含一组用户定义的 [Property](../msbuild/property-element-msbuild.md) 元素。 `PropertyGroup` 元素中可能有零个或零个以上的 `Otherwise` 元素。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[Choose](../msbuild/choose-element-msbuild.md)|评估子元素以选择代码的一部分来执行。|

## <a name="remarks"></a>备注

 `Choose` 元素中可能只有一个 `Otherwise`元素，并且它必须是最后一个元素。

 `Choose`、`When` 和 `Otherwise` 元素一起用来提供一种方式，通过这种方式选择代码的一部分来执行许多种可能的替代选择。 有关详细信息，请参阅[条件构造](../msbuild/msbuild-conditional-constructs.md)。

## <a name="example"></a>示例

 以下项目使用 `Choose` 元素来选择要在 `When` 元素中设置的属性值组。 如果两个 `When` 元素的 `Condition` 属性的计算结果均为 `false`，则将设置 `Otherwise` 元素中的属性值。

```xml
<Project
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >
    <PropertyGroup>
        <Configuration Condition="'$(Configuration)' == ''">Debug</Configuration>
        <OutputType>Exe</OutputType>
        <RootNamespace>ConsoleApplication1</RootNamespace>
        <AssemblyName>ConsoleApplication1</AssemblyName>
        <WarningLevel>4</WarningLevel>
    </PropertyGroup>
    <Choose>
        <When Condition=" '$(Configuration)'=='debug' ">
            <PropertyGroup>
                <DebugSymbols>true</DebugSymbols>
                <DebugType>full</DebugType>
                <Optimize>false</Optimize>
                <OutputPath>.\bin\Debug\</OutputPath>
                <DefineConstants>DEBUG;TRACE</DefineConstants>
            </PropertyGroup>
            <ItemGroup>
                <Compile Include="UnitTesting\*.cs" />
                <Reference Include="NUnit.dll" />
            </ItemGroup>
        </When>
        <When Condition=" '$(Configuration)'=='retail' ">
            <PropertyGroup>
                <DebugSymbols>false</DebugSymbols>
                <Optimize>true</Optimize>
                <OutputPath>.\bin\Release\</OutputPath>
                <DefineConstants>TRACE</DefineConstants>
            </PropertyGroup>
        </When>
        <Otherwise>
            <PropertyGroup>
                <DebugSymbols>true</DebugSymbols>
                <Optimize>false</Optimize>
                <OutputPath>.\bin\$(Configuration)\</OutputPath>
                <DefineConstants>DEBUG;TRACE</DefineConstants>
            </PropertyGroup>
        </Otherwise>
        </Choose>
    <Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
</Project>
```

## <a name="see-also"></a>另请参阅

- [条件构造](../msbuild/msbuild-conditional-constructs.md)
- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
