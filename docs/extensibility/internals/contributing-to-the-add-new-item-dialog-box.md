---
title: 参与"添加新项"对话框|Microsoft Docs
description: 了解如何通过注册"项目注册表"子项Visual Studio"添加项"模板，为项目中的"添加新项"对话框做出贡献。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, contributing to
ms.assetid: b2e53175-9372-4d17-8c2b-9264c9e51e9c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a99ccd5375f91baf0f91fceaadd803ee30d5b985
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600747"
---
# <a name="contribute-to-the-add-new-item-dialog-box"></a>参与"添加新项"对话框
项目子类型可以通过在"项目注册表"子项下注册"添加项模板"，为"添加新项"对话框 **提供** 完整的新项目录。

## <a name="register-add-new-item-templates"></a>注册"添加新项"模板
 本部分位于 **注册表HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects的** "配置"下。 下面的注册表项假定项目 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 由假设项目子类型聚合。 下面列出了项目的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 条目。

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}]
@="#2143"
"DefaultProjectExtension"="vbproj"
"PossibleProjectExtensions"="vbproj;vbp"
"ProjectTemplatesDir"="visualStudioInstallPath\\Vb\\.\\VBProjects"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}\AddItemTemplates\TemplateDirs\{12345678-1234-1234-1122334455667788}\/1]
@="#100"
"TemplatesDir"="projectSubTypeTemplatesDir\\VBProjectItems"
```

 **AddItemTemplates\TemplateDirs** 子项包含注册表项，其中包含放置"添加新项"对话框中可用项的目录的路径。 

 环境会自动加载 **Projects** 注册表子项下的所有 **AddItemTemplates** 数据。 此数据可以包括基本项目实现的数据，以及特定项目子类型类型的数据。 每个项目子类型由项目类型 **GUID 标识**。 项目子类型可以指定一组备用的"添加项"模板，用于特定风格项目实例，具体方法为支持实现中的 中的 枚举，以返回项目子类型的 `VSHPROPID_ AddItemTemplatesGuid` <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> GUID 值。 如果 `VSHPROPID_AddItemTemplatesGuid` 未指定 属性，则使用基本项目 GUID。

 可以通过在项目子类型聚合器对象上实现 接口来筛选"添加新项 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> "对话框中的项。 例如，通过聚合项目实现数据库项目的项目子类型可以通过实现筛选来筛选"添加新项"对话框中的特定项，而反过来，可以通过在 中支持 来添加数据库项目特定的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]  `VSHPROPID_ AddItemTemplatesGuid` 项 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> 。 有关筛选项和将项添加到"添加新项"对话框的详细信息，请参阅向"添加新项["对话框添加项](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [通常用于扩展项目的 对象的 CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
