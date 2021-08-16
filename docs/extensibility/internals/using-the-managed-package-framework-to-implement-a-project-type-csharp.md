---
title: '对 c # (的项目类型使用托管包框架 ) '
description: 了解托管包框架，该框架提供可用于实现自己的项目类型的 .NET 类，您可以使用这些类或从继承这些类。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating with MPF
- MPF projects
- managed package framework, creating projects
ms.assetid: 926de536-eead-415b-9451-f1ddc8c44630
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: e05358c2e8ba33048fbeec4af798e77b66755cb9b9a1c5c6867cc20e630f71fe
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121375593"
---
# <a name="using-the-managed-package-framework-to-implement-a-project-type-c"></a>使用托管包框架实现项目类型 (C#)
托管包框架 (MPF) 提供可用于实现自己的项目类型的 c # 类。 MPF 实现了许多接口 Visual Studio 需要提供一个项目类型，让你自由地集中精力实现项目类型的细节。

## <a name="using-the-mpf-project-source-code"></a>使用 MPF Project 源代码
  (MPFProj 的项目的托管包框架) 提供用于创建和管理新项目系统的帮助程序类。 与 MPF 中的其他类不同，项目类不包括在 Visual Studio 随附的程序集中。 相反，项目类作为 [2013](https://github.com/tunnelvisionlabs/MPFProj10)中项目的源代码提供。

 若要将此项目添加到 VSPackage 解决方案，请执行以下操作：

1. 将 MPFProj 文件下载到 *MPFProjectDir*。

2. 在 *MPFProjectDir*\Dev10\Src\CSharp\ProjectBase.file 中，更改以下块：

```
<!-- Provide a default value for $(ProjectBasePath) -->
  <PropertyGroup>
    <ProjectBasePath >MPFProjDir\Dev10\Src\CSharp</ProjectBasePath>
  </PropertyGroup>
```

1. 创建 VSPackage 项目。

2. 卸载 VSPackage 项目。

3. 编辑 VSPackage 文件，方法是在其他块之前添加以下块 `<Import>` ：

```
<Import Project="MPFProjectDir\Dev10\Src\CSharp\ProjectBase.files" />
  <PropertyGroup>
    <!--To specify a different registry root to register your package, uncomment the TargetRegistryRoot tag and specify a registry root in it.
    <TargetRegistryRoot></TargetRegistryRoot>-->
    <RegisterOutputPackage>true</RegisterOutputPackage>
    <RegisterWithCodebase>true</RegisterWithCodebase>
  </PropertyGroup>
```

1. 保存项目。

2. 关闭并重新打开 VSPackage 解决方案。

3. 重新打开 VSPackage 项目。 应会看到名为 ProjectBase 的新目录。

4. 将以下引用添加到 VSPackage 项目：

     Microsoft. 4。0

5. 生成项目。

## <a name="hierarchy-classes"></a>层次结构类
 下表汇总了支持项目层次结构的 MPFProj 中的类。 有关详细信息，请参阅 [层次结构和选择](../../extensibility/internals/hierarchies-and-selection.md)。

|类名|
|----------------|
|`Microsoft.VisualStudio.Package.HierarchyNode`|
|`Microsoft.VisualStudio.Package.ProjectNode`|
|`Microsoft.VisualStudio.Package.ProjectContainerNode`|
|`Microsoft.VisualStudio.Package.FileNode`|
|`Microsoft.VisualStudio.Package.FolderNode`|
|`Microsoft.VisualStudio.Package.ReferenceContainerNode`|
|`Microsoft.VisualStudio.Package.ReferenceNode`|
|`Microsoft.VisualStudio.Package.ProjectReferenceNode`|
|`Microsoft.VisualStudio.Package.ComReferenceNode`|
|`Microsoft.VisualStudio.Package.AssemblyReferenceNode`|
|`Microsoft.VisualStudio.Package.BuildDependency`|

## <a name="document-handling-classes"></a>Document-Handling 类
 下表列出了支持文档处理的 MPF 中的类。 有关详细信息，请参阅[打开和保存 Project 项](../../extensibility/internals/opening-and-saving-project-items.md)。

|类名|
|----------------|
|`Microsoft.VisualStudio.Package.DocumentManager`|
|`Microsoft.VisualStudio.Package.FileDocumentManager`|

## <a name="configuration-and-output-classes"></a>配置和输出类
 下表列出了 MPF 中的类，这些类允许项目类型支持多个配置，例如调试和发布以及项目输出的集合。 有关详细信息，请参阅 [管理配置选项](../../extensibility/internals/managing-configuration-options.md)。

|类名|
|----------------|
|`Microsoft.VisualStudio.Package.ConfigProvider`|
|`Microsoft.VisualStudio.Package.ProjectConfig`|
|`Microsoft.VisualStudio.Package.BuildableProjectConfig`|
|`Microsoft.VisualStudio.Package.OutputGroup`|
|`Microsoft.VisualStudio.Package.ProjectElement`|

## <a name="automation-support-classes"></a>Automation-Support 类
 下表列出了支持自动化的 MPF 中的类，以便您的项目类型的用户可以编写外接程序。

|类名|
|----------------|
|`Microsoft.VisualStudio.Package.Automation.OAProject`|
|`Microsoft.VisualStudio.Package.Automation.OANavigableProjectItems`|
|`Microsoft.VisualStudio.Package.Automation.OAProjectItems`|
|`Microsoft.VisualStudio.Package.Automation.OAProjectItem`|
|`Microsoft.VisualStudio.Package.Automation.OANestedProjectItem`|

## <a name="properties-classes"></a>Properties 类
 下表列出了 MPF 中的类，这些类允许项目类型添加用户可以在属性浏览器中浏览和修改的属性。

|类名|
|----------------|
|`Microsoft.VisualStudio.Package.LocalizableProperties`|
|`Microsoft.VisualStudio.Package.NodeProperties`|
|`Microsoft.VisualStudio.Package.FileNodeProperties`|
|`Microsoft.VisualStudio.Package.ProjectNodeProperties`|
|`Microsoft.VisualStudio.Package.FolderNodeProperties`|
|`Microsoft.VisualStudio.Package.ReferenceNodeProperties`|
