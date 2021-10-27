---
title: MSBuild 项目文件架构引用 | Microsoft Docs
description: 请参阅列出了所有 MSBuild XML 架构元素及其可用特性和子元素的表。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, file schema
ms.assetid: d9a68146-1f43-4621-ac78-2c8c3f400936
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 49e2b4196ce6ac08177aa9a4b3c7b484de8194c2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640819"
---
# <a name="msbuild-project-file-schema-reference"></a>MSBuild 项目文件架构引用

提供列有所有 MSBuild XML 架构元素及其可用属性和子元素的表。

 MSBuild 使用项目文件指示生成引擎要生成哪些内容以及生成方法。 MSBuild 项目文件是 XML 文件，其遵循 MSBuild XML 架构。 本部分介绍 MSBuild 的 XML 架构定义 (.xsd) 文件。

Visual Studio 2017 和更高版本不需要 MSBuild 项目文件中的架构链接。 如果该链接存在，则无论 Visual Studio 的版本如何，它都应为 ` http://schemas.microsoft.com/developer/msbuild/2003`。

## <a name="msbuild-xml-schema-elements"></a>MSBuild XML 架构元素

 下表列出了所有 MSBuild XML 架构元素及其子元素和属性。

|元素|子元素|属性|
|-------------|--------------------|----------------|
|[Choose 元素 (MSBuild)](../msbuild/choose-element-msbuild.md)|Otherwise<br /><br /> When|--|
|[Import 元素 (MSBuild)](../msbuild/import-element-msbuild.md)|--|条件<br /><br /> Project|
|[ImportGroup 元素](../msbuild/importgroup-element.md)|导入|条件|
|[Item 元素 (MSBuild)](../msbuild/item-element-msbuild.md)|*ItemMetaData*|条件<br /><br /> Exclude<br /><br /> 包括<br /><br /> 删除|
|[ItemDefinitionGroup 元素 (MSBuild)](../msbuild/itemdefinitiongroup-element-msbuild.md)|*Item*|条件|
|[ItemGroup 元素 (MSBuild)](../msbuild/itemgroup-element-msbuild.md)|*Item*|条件|
|[ItemMetadata 元素 (MSBuild)](../msbuild/itemmetadata-element-msbuild.md)|*Item*|条件|
|[OnError 元素 (MSBuild)](../msbuild/onerror-element-msbuild.md)|--|条件<br /><br /> ExecuteTargets|
|[Otherwise 元素 (MSBuild)](../msbuild/otherwise-element-msbuild.md)|Choose<br /><br /> ItemGroup<br /><br /> PropertyGroup|--|
|[Output 元素 (MSBuild)](../msbuild/output-element-msbuild.md)|--|条件<br /><br /> ItemName<br /><br /> PropertyName<br /><br /> TaskParameter|
|[Parameter 元素](../msbuild/parameter-element.md)|--|输出<br /><br /> ParameterType<br /><br /> 必需|
|[ParameterGroup 元素](../msbuild/parametergroup-element.md)|*参数*|--|
|[Project 元素 (MSBuild)](../msbuild/project-element-msbuild.md)|Choose<br /><br /> 导入<br /><br /> ItemGroup<br /><br /> ProjectExtensions<br /><br /> PropertyGroup<br /><br /> 目标<br /><br /> UsingTask|DefaultTargets<br /><br /> InitialTargets<br /><br /> Sdk<br /><br /> ToolsVersion<br /><br /> TreatAsLocalProperty<br /><br /> xmlns|
|[ProjectExtensions 元素 (MSBuild)](../msbuild/projectextensions-element-msbuild.md)|--|--|
|[Property 元素 (MSBuild)](../msbuild/property-element-msbuild.md)|--|条件|
|[PropertyGroup 元素 (MSBuild)](../msbuild/propertygroup-element-msbuild.md)|*属性*|条件|
|[Sdk 元素 (MSBuild)](../msbuild/sdk-element-msbuild.md)|--|名称<br /><br /> 版本|
|[Target 元素 (MSBuild)](../msbuild/target-element-msbuild.md)|OnError<br /><br /> *任务*|AfterTargets<br /><br /> BeforeTargets<br /><br /> 条件<br /><br /> DependsOnTargets<br /><br /> 输入<br /><br /> KeepDuplicateOutputs<br /><br /> 名称<br /><br /> 输出<br /><br /> 返回|
|[Target 的 Task 元素 (MSBuild)](../msbuild/task-element-msbuild.md)|输出|条件<br /><br /> ContinueOnError<br /><br /> *参数*|
|[UsingTask 的 Task 元素 (MSBuild)](../msbuild/taskbody-element-msbuild.md)|*数据*|评估|
|[UsingTask 元素 (MSBuild)](../msbuild/usingtask-element-msbuild.md)|ParameterGroup<br /><br /> 任务|AssemblyFile<br /><br /> AssemblyName<br /><br /> 条件<br /><br /> TaskFactory<br /><br /> TaskName|
|[When 元素 (MSBuild)](../msbuild/when-element-msbuild.md)|Choose<br /><br /> ItemGroup<br /><br /> PropertyGroup|条件|

## <a name="see-also"></a>另请参阅

- [任务参考](../msbuild/msbuild-task-reference.md)
- [条件](../msbuild/msbuild-conditions.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [MSBuild](../msbuild/msbuild.md)
