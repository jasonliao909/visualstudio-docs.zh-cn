---
title: 注册项目和项模板|Microsoft Docs
description: 了解如何Visual Studio类型的注册信息来确定在"添加新项目"和"添加新项"对话框中显示哪些内容。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- projects [Visual Studio SDK], adding items
- registry, Add New Item dialog box
- Add New Item dialog box
- Add New Project dialog box
- registry, Add New Project dialog box
ms.assetid: 6b909f93-d7f5-4aec-81c6-ee9ff0f31638
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8b60022c6adf65d0b0d60d32b4ad7ae72067726d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905626"
---
# <a name="registering-project-and-item-templates"></a>注册项目和项模板
项目类型必须注册其项目和项目项模板所在的目录。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用与项目类型关联的注册信息来确定在"添加新项目"和"添加新项"**对话框中要显示** 哪些内容。

 有关模板的详细信息，请参阅 [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。

## <a name="registry-entries-for-projects"></a>项目的注册表项
 以下示例显示"版本"下HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\ < *注册表*>。 随附的表说明了示例中使用的元素。

```
[Projects\{ProjectGUID}]
@="MyProjectType"
"DisplayName"="#2"
"Package"="{VSPackageGUID}"
"ProjectTemplatesDir"="C:\\MyProduct\\MyProjectTemplates"
```

|名称|类型|描述|
|----------|----------|-----------------|
|@|REG_SZ|此类项目的默认名称。|
|DisplayName|REG_SZ|从"包"下注册的附属 DLL 中检索的名称的资源 ID。|
|程序包|REG_SZ|在"包"下注册的包的类 ID。|
|ProjectTemplatesDir|REG_SZ|项目模板文件的默认路径。 "项目模板"文件由"新建 **项目"模板** 显示。|

### <a name="registering-item-templates"></a>注册项模板
 必须注册存储项模板的目录。

```
[Projects\{ProjectGUID}\AddItemTemplates\TemplateDirs\{VSPackageGUID}\1]
@="#7"
"TemplatesDir"="C:\\MyProduct\\MyProjectItemTemplates "
"TemplatesLocalizedSubDir"="#10"
"SortPriority"=dword:00000064
```

| 名称 | 类型 | 描述 |
|--------------------------|-----------| - |
| @ | REG_SZ | 添加项模板的资源 ID。 |
| TemplatesDir | REG_SZ | "添加新项"向导的对话框中显示 **的项目项** 的路径。 |
| TemplatesLocalizedSubDir | REG_SZ | 字符串的资源 ID，该字符串命名包含本地化模板的 TemplatesDir 的子目录。 由于 从附属 DLL 加载字符串资源（如果有），因此每个附属 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] DLL 可以包含不同的本地化子目录名称。 |
| SortPriority | REG_DWORD | 设置 SortPriority 以控制模板在"添加新项"对话框中的 **显示顺序** 。 较大的 SortPriority 值之前显示在模板列表中。 |

### <a name="registering-file-filters"></a>注册文件筛选器
 （可选）可以注册在提示输入文件名 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 时使用的筛选器。 例如 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] ，"打开文件 **"对话框的** 筛选器为：

 **Visual C# 文件 (\* \* .cs、.resx、.settings、.xsd、.wsdl \* \* \* \*) ;。\* \* cs、.resx、.settings、.xsd、.wsdl \* \*)**

 为了支持注册多个筛选器，每个筛选器在 HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\ < *Version*>\Projects \\ { \<*ProjectGUID*> }\Filters \\ < *Subkey*> 下注册。 子项名称是任意的; [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 忽略子项的名称，并仅使用其值。

 可以通过设置标志来控制使用筛选器的上下文，如下表所示。 如果筛选器未设置任何标志，它将在"添加现有项"对话框和"打开文件"对话框中的常用筛选器之后列出，但不在"在文件中查找"对话框中使用。 

```
[Projects\{ProjectGUID}\Filters\MyLanguageFilter]
@="#3"
"CommonOpenFilesFilter"=dword:00000000
"CommonFindFilesFilter"=dword:00000000
"FindInFilesFilter"=dword:00000000
"NotOpenFileFilter"=dword:00000000
"NotAddExistingItemFilter"=dword:00000000
"SortPriority"=dword:00000064
```

|名称|类型|描述|
|----------|----------|-----------------|
|CommonFindFilesFilter|REG_DWORD|使筛选器成为"在文件中查找"对话框中 **的常用** 筛选器之一。 常见筛选器在筛选器列表中列出，然后筛选器未标记为通用。|
|CommonOpenFilesFilter|REG_DWORD|使筛选器成为"打开文件"对话框中的常用 **筛选器** 之一。 常见筛选器在筛选器列表中列出，然后筛选器未标记为通用。|
|FindInFilesFilter|REG_DWORD|在"在文件中查找"对话框中列出 **常用筛选器后的** 筛选器。|
|NotOpenFileFilter|REG_DWORD|指示筛选器未在"打开文件 **"对话框中** 使用。|
|NotAddExistingItemFilter|REG_DWORD|指示筛选器未在"添加现有项 **"对话框中** 使用。|
|SortPriority|REG_DWORD|设置 SortPriority 以控制筛选器的显示顺序。 较大的 SortPriority 值显示在筛选器列表中。|

## <a name="directory-structure"></a>目录结构
 VSPackages 可以将模板文件和文件夹放在本地或远程磁盘上的任意位置，只要该位置是通过 IDE (环境注册) 。 但是，为便于组织，我们建议在产品的安装路径下设置以下目录结构。

 \Templates

 \Projects (包含项目模板) 

 \Applications

 \Components

 \ ...

 \ProjectItems (包含项目项) 

 \Class

 \Form

 \网页

 \HelperFiles (包含多文件项目项中使用的文件) 

 \WizardFiles

## <a name="see-also"></a>另请参阅

- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [向导](../../extensibility/internals/wizards.md)
- [本地化应用程序](../../ide/globalizing-and-localizing-applications.md)
- [通常用于扩展项目的对象的 CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
