---
title: 注册 Project 类型 |Microsoft Docs
description: 了解如何创建允许 Visual Studio 识别和使用您的新项目类型的注册表项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], new project registry entries
- registry, new project types
- registration, new project types
ms.assetid: dfc0e231-6b4e-447d-9d64-0e66dea3394a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 0d20db232bc340e241f2fc4ab05927c59660741b5b0bc5e77e4280a6a1498d41
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401266"
---
# <a name="registering-a-project-type"></a>注册项目类型
当你创建新的项目类型时，你必须创建允许 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 识别和使用你的项目类型的注册表项。 通常使用注册表脚本 () 文件创建这些注册表项。

 在下面的示例中，注册表中的语句提供默认路径和数据（如果适用），后跟一个表，其中包含来自每个语句的注册表脚本的条目。 这些表提供了这些语句的脚本项和其他信息。

> [!NOTE]
> 下面的注册表信息旨在作为要为注册项目类型而编写的注册表脚本中的项的类型和用途的示例。 你的实际条目及其使用情况可能因你的项目类型的特定要求而异。 应查看可用的示例，查找与要开发的项目类型非常相似的示例，然后查看该示例的注册表脚本。

 以下示例来自 HKEY_CLASSES_ROOT。

## <a name="example-1"></a>示例 1

```
\.figp
   @="FigPrjFile"
   "Content Type"="text/plain"
\.figp\ShellNew
   "NullFile"=""
\FigPrjFile
   @="Figure Project File"
\DefaultIcon
   @="<Visual Studio SDK installation path>\\9.0VSIntegration\\SomeFolder\\FigPkgs\\FigPrj\\Debug\\FigPrj.dll,-206"
\shell\open
   @="&Open in Visual Studio"
\shell\open\command
   @="devenv.exe \"%1\""
```

|名称|类型|数据|说明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`FigPrjFile`|扩展名为 figp 的项目类型文件的名称和说明。|
|`Content Type`|REG_SZ|`Text/plain`|项目文件的内容类型。|
|`NullFile`|REG_SZ|`Null`||
|`@`|REG_SZ|`%MODULE%,-206`|用于此类型的项目的默认图标。 在注册表中完成% MODULE% 语句到项目类型 DLL 的默认位置。|
|`@`|REG_SZ|`&Open in Visual Studio`|将在其中打开此项目类型的默认应用程序。|
|`@`|REG_SZ|`devenv.exe "%1"`|将在打开此类型的项目时运行的默认命令。|

 以下示例来自 HKEY_LOCAL_MACHINE，位于注册表项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\99.0Exp\Packages] 下的注册表中。

## <a name="example-2"></a>示例 2

```
\{ACEF4EB2-57CF-11D2-96F4-000000000000} (The CLSID for the VSPackage)
   @="FigPrj Project Package"
   "InprocServer32"="9.0<Visual Studio SDK installation path>\\VSIntegration\\Archive\\FigPkgs\\FigPrj\\                      Debug\\FigPrj.dll"
   "CompanyName"="Microsoft"
   "ProductName"="Figure Project Sample"
   "ProductVersion"="9.0"
   "MinEdition"="professional"
   "ID"=dword:00000001
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\SatelliteDLL
   "DllName"="FigPrjUI.dll"
   "Path"="9.0<Visual Studio SDK installation path>\\VSIntegration\\Archive\\FigPkgs\\FigPrj\\Debug\\"
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\Automation
   "FigProjects"=""
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\AutomationEvents
   "FigProjectsEvents"="Returns the FigProjectsEvents Object"
   "FigProjectItemsEvents"="Returns the FigProjectItemsEvents Object"
```

|名称|类型|数据|说明|
|----------|----------|----------|-----------------|
|`@`（默认值）|REG_SZ|`FigPrj Project VSPackage`|此注册的 VSPackage (项目类型) 的可本地化的名称。|
|`InprocServer32`|REG_SZ|`%MODULE%`|项目类型 DLL 的路径。 IDE 将加载此 DLL，并将 VSPackage CLSID 传递到 `DllGetClassObject` 来 <xref:Microsoft.VisualStudio.OLE.Interop.IClassFactory> 构造 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> 对象。|
|`CompanyName`|REG_SZ|`Microsoft`|开发项目类型的公司的名称。|
|`ProductName`|REG_SZ|`Figure Project Sample`|项目类型的名称。|
|`ProductVersion`|REG_SZ|`9.0`|项目类型版本的版本号。|
|`MinEdition`|REG_SZ|`professional`|要注册的 VSPackage 的版本。|
|`ID`|REG_DWORD|`%IDS_PACKAGE_LOAD_KEY%`|项目的包加载键 VSPackage。 在环境启动后加载项目时，会对该密钥进行验证。|
|`DllName`|REG_SZ|`%RESOURCE_DLL%`|包含项目类型的本地化资源的附属 DLL 的文件名。|
|`Path`|REG_SZ|`%RESOURCE_PATH%`|附属 DLL 的路径。|
|`FigProjectsEvents`|REG_SZ|请参阅语句获取值。|确定为此自动化事件返回的文本字符串。|
|`FigProjectItemsEvents`|REG_SZ|请参阅语句获取值。|确定为此自动化事件返回的文本字符串。|

 以下所有示例都位于注册表项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects] 下。

## <a name="example-3"></a>示例 3

```
\{C061DB26-5833-11D2-96F5-000000000000} (The CLSID for projects of this type)
   @="FigPrj Project"
   "DisplayName"="#2"
   "Package"="{ACEF4EB2-57CF-11D2-96F4-000000000000}"
   "ProjectTemplatesDir"="C:\\Program Files\\VSIP 9.0\\EnvSDK\\FigPkgs\\                           FigPrj\\FigPrjProjects"
   "ItemTemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                           FigPrjProjectItems"
   "DisplayProjectFileExtensions"="#3"
   "PossibleProjectExtensions"="figp"
   "DefaultProjectExtension"=".figp"
\{C061DB26-5833-11D2-96F5-000000000000}\Filters\1       (Folder 1 contains settings for Open Files filters.)
   @="#4"
   "CommonOpenFilesFilter"=dword:00000000
   "CommonFindFilesFilter"=dword:00000000
   "NotAddExistingItemFilter"=dword:00000000
   "FindInFilesFilter"=dword:00000000
   "NotOpenFileFilter"=dword:00000000
   "SortPriority"=dword:000003e8
\{C061DB26-5833-11D2-96F5-000000000000}\Filters\2
      (Folder 2 contains settings for Find in Files filters.)
   @="#5"
   "CommonOpenFilesFilter"=dword:00000000
   "CommonFindFilesFilter"=dword:00000000
   "NotAddExistingItemFilter"=dword:00000001
   "FindInFilesFilter"=dword:00000001
   "NotOpenFileFilter"=dword:00000000
   "SortPriority"=dword:000003e8
\{C061DB26-5833-11D2-96F5-000000000000}\AddItemTemplates\TemplateDirs\ {ACEF4EB2-57CF-11D2-96F4-000000000000}\1 (Second GUID indicates the registered project type for the Add Items templates.)
   @="#6"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                    FigPrjProjectItems"
   "SortPriority"=dword:00000064
```

|名称|类型|数据|说明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`FigPrj Project`|此类型项目的默认名称。|
|`DisplayName`|REG_SZ|`#%IDS_PROJECT_TYPE%`|要从在包下注册的附属 DLL 检索的名称的资源 ID。|
|`Package`|REG_SZ|`%CLSID_Package%`|在包下注册的 VSPackage 的类 ID。|
|`ProjectTemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|Project 模板文件的默认路径。 这是由新的 Project 模板显示的文件。|
|`ItemTemplatesDir`|REG_SZ|`%TEMPLATE_PATH% \FigPrjProjectItems`|Project 项模板文件的默认路径。 这些是 "添加新项" 模板显示的文件。|
|`DisplayProjectFileExtensions`|REG_SZ|`#%IDS_DISPLAY_PROJ_FILE_EXT%`|启用 IDE 以实现 " **打开** " 对话框。|
|`PossibleProjectExtensions`|REG_SZ|`figp`|由 IDE 用于确定所打开的项目是否由此项目类型 (项目工厂) 进行处理。 多个项的格式是以分号分隔的列表。 例如 ".vdproj; vdp"。|
|`DefaultProjectExtension`|REG_SZ|`.figp`|由 IDE 用于 "另存为" 操作的默认文件扩展名。|
|`Filter Settings`|REG_DWORD|请参阅下表中的语句和注释。|这些设置用于设置在 UI 对话框中显示文件的各种筛选器。|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|添加项模板的资源 ID。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|显示在 " **添加新项** " 模板的对话框中的项目项的路径。|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|确定在 " **添加新项** " 对话框中显示的文件的树节点中的排序顺序。|

 下表显示了上一个代码段中可用的筛选器选项。

|筛选器选项|说明|
|-------------------|-----------------|
|`CommonFindFilesFilter`|指示筛选器是 "在 **文件中查找** " 对话框中的一个常见筛选器。 常见筛选器在筛选器列表中列出，在未标记为通用筛选器之前。|
|`CommonOpenFilesFilter`|指示筛选器是"打开文件"对话框中的常用 **筛选器之一** 。 常见筛选器在筛选器列表中列出，在未标记为通用筛选器之前。|
|`FindInFilesFilter`|指示筛选器将是"在文件中查找"对话框中的筛选器之一，并且将在常用筛选器之后列出。|
|`NotOpenFileFilter`|指示不会在"打开文件"对话框中 **使用** 筛选器。|
|`NotAddExistingItemFilter`|指示不会在"添加现有项"对话框中 **使用** 筛选器。|

 默认情况下，如果筛选器未设置其中一个或多个标志，则列出常用筛选器后，筛选器将用在"添加现有项"对话框和"打开文件"对话框中。 筛选器未在"在文件中 **查找"对话框中** 使用。

 以下所有示例都位于注册表中的项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects]。

## <a name="example-4"></a>示例 4

```
{FE3BBBB6-72D5-11d2-9ACE-00C04F79A2A4} (The CLSID for Enterprise Projects)
\{FE3BBBB6-72D5-11d2-9ACE-00C04F79A2A4}\AddItemTemplates\TemplateDirs\ {ACEF4EB2-57CF-11D2-96F4-000000000000}\1 (CLSID for projects of this type)
   @="#7"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPrj\\FigPrjProjects"
   "SortPriority"=dword:00000029
   "NewProjectDialogOnly"=dword:00000000
```

|名称|类型|数据|说明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`#%IDS_NEWPROJ_ TEMPLATES_ENTRY%`|"新建"模板Project ID。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|已注册项目类型的项目的默认路径。|
|`SortPriority`|REG_DWORD|`41 (x29)`|设置"新建项目向导"对话框中显示的项目的排序顺序。|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0 指示此类型的项目只显示在"新建Project对话框中。|

 以下所有示例都位于注册表中的项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects]。

## <a name="example-5"></a>示例 5

```
\{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3} (CLSID for Miscellaneous Files projects)
   @="Miscellaneous Files Project"
\AddItemTemplates\TemplateDirs\{ACEF4EB2-57CF-11D2-96F4-000000000000}\1
                                 (CLSID for Figures Project projects)
   @="#6"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                    FigPrjProjectItems"
   "SortPriority"=dword:00000064
```

|名称|类型|数据|说明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|无|默认值，指示以下条目用于杂项文件项目条目。|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|"添加新项"模板文件的资源 ID 值。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|将在"添加新项"对话框中显示的项 **的默认** 路径。|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|建立排序顺序，以便显示在"添加新项"对话框的 **树节点中** 。|

 以下示例位于注册表中的项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Menus]。

## <a name="example-6"></a>示例 6

```
"{ACEF4EB2-57CF-11D2-96F4-000000000000}"=",1000,1"
```

 菜单条目将 IDE 指向用于检索菜单信息的资源。 当此数据合并到菜单数据库中时，将在注册表的 MenuMerged 节中添加相同的键。 VSPackage 不应直接修改"菜单合并"部分下的内容。 在下表的"数据"字段中，有三个逗号分隔字段。 第一个字段标识菜单资源文件的完整路径：

- 如果省略第一个字段，则从 VSPackage GUID 标识的附属 DLL 加载菜单资源。

  第二个字段标识类型为 CTMENU 的菜单资源 ID：

- 如果指定了资源 ID，并且文件路径由第一个参数提供，则从完整文件路径加载菜单资源。

- 如果提供了资源 ID，但文件路径未提供，则从附属 DLL 加载菜单资源。

- 如果提供了完整文件路径并省略了资源 ID，则要加载的文件应该是 CTO 文件。

  最后一个字段标识 CTMENU 资源的版本号。 可以通过更改版本号来再次合并菜单。

|名称|类型|数据|说明|
|----------|----------|----------|-----------------|
|%CLSID_Package%|REG_SZ|`,1000,1`|要检索菜单信息的资源。|

 以下所有示例都位于注册表中的项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\NewProjectTemplates]。

```
\TemplateDirs\{ACEF4EB2-57CF-11D2-96F4-000000000000}\1                (CLSID for Figures Project projects)
   @="#7"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\FigPrjProjects"
   "SortPriority"=dword:00000029
   "NewProjectDialogOnly"=dword:00000000
```

|名称|类型|数据|说明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`#%IDS_NEWPROJ_TEMPLATES_ENTRY%`|"图形"和"新建Project模板Project ID 值。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|"新建项目"目录的默认路径。 此目录中的项将显示在"新建Project **向导**"对话框中。|
|`SortPriority`|REG_DWORD|`41 (x29)`|确定项目在"新建项目"对话框的树节点 **Project顺序。**|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0 指示此类型的项目只显示在"新建 **Project对话框中。**|

 以下示例位于注册表中的项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\InstalledProducts]。

```
\FiguresProductSample
   "Package"="{ACEF4EB2-57CF-11D2-96F4-000000000000}"
   "UseInterface"=dword:00000001
```

|名称|类型|数据|说明|
|----------|----------|----------|-----------------|
|`Package`|REG_SZ|`%CLSID_Package%`|已注册的 VSPackage 的类 ID。|
|`UseInterface`|REG_DWORD|`1`|1 表示 UI 将用于与此项目交互。 0 表示没有 UI 接口。|

 控制新项目类型的 .vsz 文件通常包含RELATIVE_PATH条目。 此路径相对于以下设置键中项目类型的 \ProductDir 条目下指定的路径：

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\7.0Exp\Setup

 例如，Enterprise Frameworks 项目模板添加以下注册表项：

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\7.0Exp\Setup\EF\ProductDir = C：\Program Files\Microsoft Visual Studio\EnterpriseFrameworks\

 这意味着，如果在 .vsz PROJECT_TYPE包含一个 PROJECT_TYPE=EF 条目，则环境在之前指定的 ProductDir 目录中查找 .vsz 文件。

## <a name="see-also"></a>请参阅
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)
- [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
