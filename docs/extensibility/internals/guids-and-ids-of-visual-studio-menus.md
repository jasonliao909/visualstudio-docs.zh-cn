---
title: 菜单菜单的 GUID Visual Studio|Microsoft Docs
description: 在 IDE Visual Studio 集成开发环境中包含的 Visual Studio 菜单栏上，查看菜单和组的 GUID 和 ID (值) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- visual studio menus
- visual studio groups
- id
- existing menus
- guid
- menus
ms.assetid: 84639d86-dd21-4b35-9988-6bb654162488
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bceee5fce8a77ad5169020bd3d21896bdbc71443
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898066"
---
# <a name="guids-and-ids-of-visual-studio-menus"></a>菜单的 GUID 和 VISUAL STUDIO
本文枚举菜单栏上菜单和组的 GUID 和 ID Visual Studio值。 这些值在作为 Visual Studio SDK 的一部分安装的 *.vsct* 文件中定义。 有关详细信息，请参阅 [IDE 定义的命令、菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)。

 若要详细了解如何使用 *.vsct* 文件中定义的 (IDE) 集成开发环境，请参阅 [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

 菜单栏上的菜单Visual Studio组使用 GUID `guidSHLMainMenu` 。 菜单栏本身的 ID 为 `IDM_VS_TOOL_MAINMENU` 。

## <a name="groups-on-the-visual-studio-menu-bar"></a>菜单栏Visual Studio组
 若要将菜单添加到菜单栏，请设置其中一个组作为其父级。

|组|ID|
|-----------|--------|
|文件/编辑/视图|IDG_VS_MM_FILEEDITVIEW|
|重构|IDG_VS_MM_REFACTORING：|
|Project|IDG_VS_MM_PROJECT|
|构建|IDG_VS_MM_BUILDDEBUGRUN|
|格式/工具|IDG_VS_MM_TOOLSADDINS|
|窗口/帮助/社区|IDG_VS_MM_WINDOWHELP|
|加载项|IDG_VS_MM_MACROS|
|FullScreenBar|IDG_VS_MM_FULLSCREENBAR|

## <a name="menus-on-the-visual-studio-menu-bar"></a>菜单栏Visual Studio菜单
 若要将组添加到现有菜单Visual Studio，请设置以下菜单之一作为其父级。 此列表中不包含子项。

|菜单|ID|
|----------|--------|
|文件|IDM_VS_MENU_FILE|
|编辑|IDM_VS_MENU_EDIT|
|视图|IDM_VS_MENU_VIEW|
|重构|IDM_VS_MENU_REFACTORING|
|Project|IDM_VS_MENU_PROJECT|
|构建|IDM_VS_MENU_BUILD|
|格式|IDM_VS_MENU_FORMAT|
|工具|IDM_VS_MENU_TOOLS|
|扩展|IDM_VS_MENU_EXTENSIONS|
|窗口|IDM_VS_MENU_WINDOW|
|加载项|IDM_VS_MENU_ADDINS|
|社区|IDM_VS_MENU_COMMUNITY|
|帮助|IDM_VS_MENU_HELP|

## <a name="groups-on-visual-studio-menus"></a>菜单上的Visual Studio组
 以下列表显示直接从菜单栏上的菜单Visual Studio组。 将命令添加到菜单的最Visual Studio就是将其中一个组设置为父级。 从子项降序的组不会出现在此部分中。

### <a name="file-menu-groups"></a>文件菜单组

|组|ID|
|-----------|--------|
|新建/打开|IDG_VS_FILE_FILE|
|添加|IDG_VS_FILE_ADD|
|解决方案|IDG_VS_FILE_SOLUTION|
|杂项|IDG_VS_FILE_MISC|
|保存|IDG_VS_FILE_SAVE|
|重命名|IDG_VS_FILE_RENAME|
|浏览者|IDG_VS_FILE_BROWSER|
|打印|IDG_VS_FILE_PRINT|
|最近使用|IDG_VS_FILE_MRU|
|移动|IDG_VS_FILE_MOVE|
|退出|IDG_VS_FILE_EXIT|

### <a name="edit-menu-groups"></a>编辑菜单组

|组|ID|
|-----------|--------|
|撤消/重做|IDG_VS_EDIT_UNDOREDO|
|剪切/复制/粘贴|IDG_VS_EDIT_CUTCOPY|
|Select|IDG_VS_EDIT_SELECT|
|GoTo|IDG_VS_EDIT_GOTO|
|查找|IDG_VS_EDIT_FIND|
|对象|IDG_VS_EDIT_OBJECTS|
|OLE 谓词|IDG_VS_EDIT_OLEVERBS|
|命令良好|IDG_VS_EDIT_COMMANDWELL|

### <a name="refactor-menu-groups"></a>重构菜单组

|组|ID|
|-----------|--------|
|通用|IDG_REFACTORING_COMMON|
|高级|IDG_REFACTORING_ADVANCED|

### <a name="view-menu-groups"></a>查看菜单组

|组|ID|
|-----------|--------|
|表单代码|IDG_VS_VIEW_FORMCODE|
|浏览者|IDG_VS_VIEW_BROWSER|
|定义视图|IDG_VS_VIEW_DEFINEVIEWS|
|Windows|IDG_VS_VIEW_WINDOWS|
|架构师窗口|IDG_VS_VIEW_ARCH_WINDOWS|
|组织窗口|IDG_VS_VIEW_ORG_WINDOWS|
|代码浏览器|IDG_VS_VIEW_CODEBROWSENAV_WINDOWS|
|开发 Windows|IDG_VS_VIEW_DEV_WINDOWS|
|工具栏|IDG_VS_VIEW_TOOLBARS|
|符号|IDG_VS_VIEW_SYMBOLNAVIGATE|
|导航|IDG_VS_VIEW_NAVIGATE|
|小型导航|IDG_VS_VIEW_SMALLNAVIGATE|
|对象浏览器|IDG_VS_VIEW_OBJBRWSR|
|命令良好|IDG_VS_VIEW_COMMANDWELL|
|属性页|IDG_VS_VIEW_PROPPAGES|
|刷新|IDG_VS_VIEW_REFRESH|

### <a name="project-menu-groups"></a>项目菜单组

|组|ID|
|-----------|--------|
|其他添加|IDG_VS_PROJ_MISCADD|
|添加|IDG_VS_PROJ_ADD|
|文件夹|IDG_VS_PROJ_FOLDER|
|卸载/重载|IDG_VS_PROJ_UNLOADRELOAD|
|参考|IDG_VS_PROJ_REFERENCE|
|选项|IDG_VS_PROJ_OPTIONS|
|设置|IDG_VS_PROJ_SETTINGS|

### <a name="build-menu-groups"></a>生成菜单组

|组|ID|
|-----------|--------|
|解决方案|IDG_VS_BUILD_SOLUTION|
|选择|IDG_VS_BUILD_SELECTION|
|按配置优化|IDG_VS_PGO_SELECTION|
|杂项|IDG_VS_BUILD_MISC|
|取消|IDG_VS_BUILD_CANCEL|

### <a name="tools-menu-groups"></a>工具菜单组

|组|ID|
|-----------|--------|
|命令行|IDG_VS_TOOLS_CMDLINE|
|代码片段|IDG_VS_TOOLS_SNIPPETS|
|对象子集|IDG_VS_TOOLS_OBJSUBSET|
|选项|IDG_VS_TOOLS_OPTIONS|
|其他2|IDG_VS_TOOLS_OTHER2|
|外部工具|IDG_VS_TOOLS_EXT_TOOLS|
|外部自定义|IDG_VS_TOOLS_EXT_CUST|

### <a name="window-menu-groups"></a>窗口菜单组

|组|ID|
|-----------|--------|
|新建|IDG_VS_WINDOW_NEW|
|停靠/关闭|IDG_VS_DOCKCLOSE|
|停靠/隐藏|IDG_VS_DOCKHIDE|
|排列|IDG_VS_WINDOW_ARRANGE|
|导航|IDG_VS_WINDOW_NAVIGATION|
|列出|IDG_VS_WINDOW_LIST|

### <a name="help-menu-groups"></a>帮助菜单组

|组|ID|
|-----------|--------|
|示例|IDG_VS_HELP_SAMPLES|
|支持|IDG_VS_HELP_SUPPORT|
|关于|IDG_VS_HELP_ABOUT|

## <a name="submenus-of-visual-studio-menus"></a>菜单的子Visual Studio菜单
 以下层次结构显示与菜单栏上的菜单关联的子菜单Visual Studio菜单。 由于只有组才能将菜单作为父级，因此每个子菜单都必须从菜单上的组降序，而不是直接从菜单降序。 有关菜单、组和子菜单之间的关系详细信息，请参阅 [将子菜单添加到菜单](../../extensibility/adding-a-submenu-to-a-menu.md)。

> [!NOTE]
> 此层次结构中不会单独显示 Visual Studio 菜单栏上菜单的名称，因为它们可以从 IDE 中组的命名约定推断，如下所示：IDG_VS_ *\<Menu Name\> _ \<Group Name\>*。

|父组|子|子组|
|------------------|-------------|------------------|
|IDG_VS_FILE_FILE|IDM_VS_CSCD_NEW|IDG_VS_FILE_NEW_CASCADE|
||IDM_VS_CSCD_OPEN|IDG_VS_FILE_OPENP_CASCADE|
|||IDG_VS_FILE_OPENF_CASCADE|
|IDG_VS_FILE_ADD|IDM_VS_CSCD_ADD|IDG_VS_FILE_ADD_PROJECT_NEW|
|||IDG_VS_FILE_ADD_PROJECT_EXI|
|IDG_VS_FILE_MRU|IDM_VS_CSCD_FILEMRU|IDG_VS_FILE_FMRU_CASCADE|
||IDM_VS_CSCD_PROJMRU|IDG_VS_FILE_PMRU_CASCADE|
|IDG_VS_FILE_MOVE|IDM_VS_CSCD_MOVETOPRJ|IDG_VS_FILE_MOVE_CASCADE|
|||IDG_VS_FILE_MOVE_PICKER|
|IDG_VS_VIEW_DEV_WINDOWS|IDM_VS_CSCD_FINDRESULTS|IDG_VS_WNDO_FINDRESULTS|
||IDM_VS_CSCD_WINDOWS|IDG_VS_VIEW_CALLBROWSER|
|||IDG_VS_WNDO_OTRWNDWS1...6|
|||IDG_VS_WNDO_WINDOWS2|
|IDG_VS_VIEW_TOOLBARS|IDM_VS_CSCD_COMMANDBARS||
|IDG_VS_EDIT_GOTO|IDM_VS_EDITOR_FIND_MENU||
|IDG_VS_EDIT_OBJECTS|IDM_VS_CSCD_MNUDES|IDG_VS_MNUDES_INSERT|
|||IDG_VS_MNUDES_EDITNAMES|
||IDM_VS_CSCD_OLEVERBS|IDG_VS_EDIT_OLEVERBS|
|IDG_VS_BUILD_SELECTION|IDM_VS_CSCD_BUILD|IDG_VS_BUILD_CASCADE|
|||IDG_VS_BUILD_PROJPICKER|
||IDM_VS_CSCD_REBUILD|IDG_VS_REBUILD_CASCADE|
|||IDG_VS_REBUILD_PROJPICKER|
||IDM_VS_CSCD_PROJONLY|IDG_VS_PROJONLY_CASCADE|
||IDM_VS_CSCD_CLEAN|IDG_VS_CLEAN_CASCADE|
|||IDG_VS_CLEAN_PROJPICKER|
||IDM_VS_CSCD_DEPLOY|IDG_VS_DEPLOY_CASCADE|
|||IDG_VS_DEPLOY_PROJPICKER|
|IDG_VS_PGO_SELECTION|IDM_VS_CSCD_PGO_BUILD|IDG_VS_PGO_BUILD_CASCADE_BUILD|
|||IDG_VS_PGO_BUILD_CASCADE_RUN|

## <a name="see-also"></a>另请参阅
- [工具栏的 GUID Visual Studio的](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)
- [命令的 GUID Visual Studio的](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)
- [Visual Studio命令表 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
