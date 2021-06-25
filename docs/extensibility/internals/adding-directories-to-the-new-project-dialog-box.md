---
title: 将目录添加到"新建项目"对话框|Microsoft Docs
description: 了解如何将目录添加到 Visual Studio 中的"新建项目"对话框中，以便你可以创建新项目类型并显示它们以用作模板。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- New Project dialog box, extending
ms.assetid: 53b328f5-20bb-49a3-bf9e-1818f4fbdf50
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 44554c8bd7b758f1bf191d1a4bef9ba07941191d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901833"
---
# <a name="add-directories-to-the-new-project-dialog-box"></a>将目录添加到"新建项目"对话框
创建新项目类型时，还可以在"新建项目"对话框中注册新目录，以将其显示为模板。 下面的代码示例说明如何注册新目录（也称为节点）。 在示例中，注册了 VSPackage *公开的* CLSID_Package模板。 因此，"新建项目"对话框的左侧提供了添加的节点，其名称由资源 *Folder_Label_ResID确定。* 此资源从 VSPackage 附属 DLL 加载。

 **Folder** 值表示文件夹的 GUID，该文件夹Folder_Label_ResID *节点。* 在示例中，GUID 表示" **新建** 项目"对话框的"项目类型 **"窗格中的** "其他 **项目"** 文件夹。 如果 **"其他项目"** 值不存在，则标签将定位在顶层。

 `TemplatesDir`值指定包含项目模板的目录的完整路径。 这些文件可以是 *.vsz* 文件或要克隆的典型模板文件。

 如果指定 ，则它必须是字符串的资源 ID，该字符串为保存本地化模板 `TemplatesLocalizedSubDir` 的 `TemplatesDir` 的子目录命名。 由于 从附属 DLL 加载字符串资源（如果有），因此每个附属 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] DLL 可以包含不同的子目录名称。 `SortPriority`值指定排序优先级。

```
NoRemove NewProjectTemplates
{
    NoRemove TemplateDirs
  {
    ForceRemove %CLSID_Package%
    {
      ForceRemove /1 = s '#%Folder_Label_ResID%'
      {
        val Folder = s '{DCF2A94A-45B0-11D1-ADBF-00C04FB6BE4C}'
        val TemplatesDir = s '%Template_Path%'
        val TemplatesLocalizedSubDir = s '#100'
        val SortPriority = d 1000
      }
    }
  }
}
```

## <a name="see-also"></a>另请参阅
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [将项添加到"添加新项"对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [将目录添加到"添加新项"对话框](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)
