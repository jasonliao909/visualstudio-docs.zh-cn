---
title: 通常用于扩展项目的 对象的 CATID
description: 了解用于为 Visual Basic、Visual C# 和 Visual C++ 项目扩展 Project 和 ProjectItem 自动化对象的对象的 CATID。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSPackages, CATIDs
- GUIDs, VSPackages
- CATIDs for VSPackages
ms.assetid: 0c7fdb66-ed96-4b36-89f6-021bca573572
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 04253f9bfe45cd893ecbf1401fc9d7e12391a4c9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122159199"
---
# <a name="catids-for-objects-that-are-typically-used-to-extend-projects"></a>通常用于扩展项目的 对象的 CATID
下表列出了用于为 、 和 项目扩展和 `Project` `ProjectItem` 自动化对象的 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] CATID。 这些 CATID 在 *VSLangProj.olb 中定义*。

## <a name="listing-of-catids"></a>CATID 列表

|名称|GUID|
|----------|----------|
|<xref:VSLangProj.PrjCATID.prjCATIDProject>|{610D4614-D0D5-11D2-8599-006097C68E81}|
|<xref:VSLangProj.PrjCATID.prjCATIDProjectItem>|{610D4615-D0D5-11D2-8599-006097C68E81}|

## <a name="visual-basic-catids"></a>Visual BasicCATID
 下表列出了用于扩展浏览对象的 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] CATD。 它们全部在 *VSLangProj.olb 中定义*。

|名称|GUID|
|----------|----------|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBProjectBrowseObject>|{E0FDC879-C32A-4751-A3D3-0B3824BD575F}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBProjectConfigBrowseObject>|{67F8DD11-14EB-489b-87F0-F01C52AF3870}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBFileBrowseObject>|{EA5BD05D-3C72-40A5-95A0-28A2773311CA}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBFolderBrowseObject>|{932DC619-2EAA-4192-B7E6-3D15AD31DF49}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBReferenceBrowseObject>|{2289B812-8191-4e81-B7B3-174045AB0CB5}|

## <a name="visual-c-catids"></a>Visual C# CATID
 以下 CATID 可用于扩展 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 浏览对象。 它们全部在 *VSLangProj.olb 中定义*。

|名称|GUID|
|----------|----------|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpProjectBrowseObject>|{4EF9F003-DE95-4d60-96B0-212979F2A857}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpProjectConfigBrowseObject>|{A12CE10A-227F-4963-ADB6-3A43388513CA}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpFileBrowseObject>|{8D58E6AF-ED4E-48B0-8C7B-C74EF0735451}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpFolderBrowseObject>|{914FE278-054A-45DB-BF9E-5F22484CC84C}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpReferenceBrowseObject>|{2F0FA3B8-C855-4a4e-95A5-CB45C67D6C27}|

## <a name="c-catids"></a>C++ CATID
 以下 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 项目系统 CATID 不会在 .NET 2003 的类型库中公开，并且每当你想要扩展这些项目对象时，必须将其包含在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 代码中。 这些 CATID 将包含在更高版本的 的类型库中 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

|名称|GUID|
|----------|----------|
|`CVCProjectNode`|{EE8299CB-19B6-4f20-ABEA-E1FD9A33B683}|
|`CVCFolderNode`|{EE8299CA-19B6-4f20-ABEA-E1FD9A33B683}|
|`CVCFileNode`|{EE8299C9-19B6-4f20-ABEA-E1FD9A33B683}|

 下面的代码示例演示如何在代码中对这些 CATID 进行编程。

```
const LPOLESTR CVCProjectNode::s_wszCATID = L"{EE8299CB-19B6-4f20-ABEA-E1FD9A33B683}";
const LPOLESTR CVCFolderNode::s_wszCATID = L"{EE8299CA-19B6-4f20-ABEA-E1FD9A33B683}";
const LPOLESTR CVCFileNode::s_wszCATID = L"{EE8299C9-19B6-4f20-ABEA-E1FD9A33B683}";
```

 以下 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 项目系统 CATID 也不在 .NET 2003 的类型库中公开，并且每当要扩展这些项目对象时，必须将其包含在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 代码中。 这些 CATID 仅在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .NET 2003 中可用，在 的更高版本中不可用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

|名称|GUID|
|----------|----------|
|`CVCAssemblyReferenceNode`|{FE8299C9-19B6-4f20-ABEA-E1FD9A33B683}|
|`CVCProjectReferenceNode`|{593DCFCE-20A7-48e4-ACA1-49ADE9049887}|
|`CVCActiveXReferenceNode`|{9E8182D3-C60A-44f4-A74B-14C90EF9CACE}|
|`CVCReferences`|{FE8299CA-19B6-4f20-ABEA-E1FD9A33B683}|

 下面的代码示例演示如何在代码中对这些 CATID 进行编程：

```
const LPOLESTR CVCAssemblyReferenceNode::s_wszCATID = L"{FE8299C9-19B6-4f20-ABEA-E1FD9A33B683}";
const LPOLESTR CVCProjectReferenceNode::s_wszCATID = L"{593DCFCE-20A7-48e4-ACA1-49ADE9049887}";
const LPOLESTR CVCActiveXReferenceNode::s_wszCATID = L"{9E8182D3-C60A-44f4-A74B-14C90EF9CACE}";
const LPOLESTR CVCReferences::s_wszCATID = L"{FE8299CA-19B6-4f20-ABEA-E1FD9A33B683}";
```

 下表显示了 和 项目 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 类型的 GUID。

| 项目类型 | GUID |
| - | - |
| [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] | {FAE04EC0-301F-11D3-BF4B-00C04F79EFBC} |
| [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] | {F184B08F-C81C-45F6-A57F-5ABD9991F28F} |

## <a name="see-also"></a>请参阅
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
