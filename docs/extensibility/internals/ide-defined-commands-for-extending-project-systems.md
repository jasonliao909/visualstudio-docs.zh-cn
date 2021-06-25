---
title: IDE-Defined扩展项目系统扩展的 |Microsoft Docs
description: 了解用于扩展项目系统的 Visual Studio集成开发 (IDE) 中定义的命令和命令组。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- commands, project systems
- project systems, environment-defined commands
ms.assetid: 0e33b8e9-16fa-4400-a941-e92d56120e7e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4525802bf308d740ea5c468fac171e74bff2b34e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901157"
---
# <a name="ide-defined-commands-for-extending-project-systems"></a>用于扩展项目系统的 IDE 定义的命令
若要扩展项目系统，可以使用 IDE 提供的命令和命令 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 组。

 以下部分列出了对扩展项目系统特别有用的命令项。

## <a name="command-menus"></a>命令菜单
 下表显示了命令菜单，这些菜单是一个有用的位置，可用于输入调用项目扩展程序的高级别命令。

|命令菜单|描述|
|------------------|-----------------|
|IDM_VS_MENU_PROJECT|" **项目** "顶级菜单。|
|IDM_VS_TOOL_PROJWIN|**"解决方案资源管理器** 工具栏" 。|

## <a name="shortcut-menus"></a>快捷菜单
 下表显示了在 **解决方案资源管理器** 中选择了单个节点时或 解决方案资源管理器 中有多个同质选择（即所有所选节点都具有相同的类型）时所应用快捷菜单。

|快捷菜单|描述|
|-------------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE>|在选择项目节点时应用。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_ITEMNODE>|在选择文件时适用。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_FOLDERNODE>|在选择文件夹时应用。|
|IDM_VS_CTXT_WEBREFFOLDER|在选择"Web 引用"文件夹时适用。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCEROOT>|当选择了名为"引用"的引用根节点时适用。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCE>|在选择引用节点时适用;这些仅包括程序集、COM 和项目引用。 不包括 Web 引用。|

 下表显示了当所选内容跨多个层次结构时解决方案资源管理器菜单， 

|快捷菜单|描述|
|-------------------|-----------------|
|IDM_VS_CTXT_XPROJ_SLNPROJ|当当前选择包含解决方案节点和根项目节点时适用。|
|IDM_VS_CTXT_XPROJ_SLNITEM|当当前选择包含解决方案节点和项目项时适用。|
|IDM_VS_CTXT_XPROJ_MULTIPROJ|当当前选择仅包含多个根项目节点时适用。|
|IDM_VS_CTXT_XPROJ_PROJITEM|当当前选择包含根项目节点和项目项的组合时适用。 此外，所选内容可能包含解决方案节点。|
|IDM_VS_CTXT_XPROJ_MULTIITEM|当当前选定内容包含解决方案中多个项目的项目项时，或在同一项目中选择不同类型的项时适用。|

## <a name="command-groups"></a>命令组
 下表显示了扩展项目时可以使用的命令组，以及可以通过快捷菜单 <xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE> 访问的命令组。

|命令组|描述|
|-------------------|-----------------|
|IDG_VS_CTXT_PROJECT_BUILD|用于生成、重新生成和部署项目的命令。|
|IDG_VS_CTXT_COMPILELINK|用于编译和链接项目的命令。|
|IDG_VS_CTXT_PROJECT_CONFIG|用于设置项目配置和生成顺序的命令。|
|IDG_VS_CTXT_PROJECT_ADD|将项添加到项目的命令。|
|IDG_VS_CTXT_PROJECT_START|用于设置与 F5 键关联的启动项目的命令。|
|IDG_VS_CTXT_PROJECT_SAVE|用于保存项目项的命令。|
|IDG_VS_CTXT_PROJECT_DEBUG|用于调试的命令。|
|IDG_VS_CTXT_PROJECT_SCC|源代码管理的命令。|
|IDG_VS_CTXT_PROJECT_TRANSFER|用于剪切、复制和粘贴操作的命令。|
|IDG_VS_CTXT_PROJECT_PROPERTIES|提供对"项目属性 **"对话框** 的访问权限的命令。|

## <a name="see-also"></a>另请参阅

- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [创建可重复使用的按钮组](../../extensibility/creating-reusable-groups-of-buttons.md)
