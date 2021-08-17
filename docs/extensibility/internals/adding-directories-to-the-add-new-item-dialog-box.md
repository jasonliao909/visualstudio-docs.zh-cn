---
title: 将目录添加到"添加新项"对话框|Microsoft Docs
description: 了解如何通过使用注册表脚本注册目录，将目录添加到 Visual Studio 中的"添加新项"对话框。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Add New Item dialog box, extending
ms.assetid: 67ae8af6-3752-49e8-8ce3-007aca5f7982
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 258ff221893fc9ec10c9e37920c87fb242f4dc36
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122095070"
---
# <a name="add-directories-to-the-add-new-item-dialog-box"></a>将目录添加到"添加新项"对话框
下面的代码示例演示如何为"添加新项"对话框注册一 **组新目录** 。 每个项目的 **"添加新项** "对话框的目录都不同。 因此，目录在 "项目" 子 **项下注册**，该子项HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\Projects **。**

## <a name="registry-script"></a>注册表脚本

```
NoRemove Projects
{
  NoRemove %GUID_Project%
  {
    NoRemove AddItemTemplates
    {
      NoRemove TemplateDirs
      {
        ForceRemove %CLSID_Package%
        {
      ForceRemove /1 = s '#%Folder_Label_ResID%'
          {
            val TemplatesDir = s '%Template_Path%'
            val SortPriority = d 2000
          }
        }
      }
    }
  }
}
```

 `%Template_Path%`值指定包含项目模板的目录的完整路径。 这些模板可以是 *要克隆的 .vsz* 文件或原型模板文件。

 `SortPriority`值指定排序优先级。

## <a name="add-items-to-an-existing-project"></a>向现有项目添加项
 还可以将项添加到现有项目。 例如，对于项目，可以将项添加到 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] *\<root> \Program Files\Microsoft Visual Studio\VC#\CSharpProjectItems\LocalProjectItems* 文件夹。 在这种情况下， 是 C# 项目的 `%GUID_Project%` GUID ({FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}) 。

 还可通过编程项目子类型来扩展现有项目。 使用项目子类型，无需编写新项目类型即可扩展项目。 有关项目子类型的信息，请参阅 Project[子类型](../../extensibility/internals/project-subtypes.md)。

## <a name="see-also"></a>请参阅
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [将项添加到"添加新项"对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [将目录添加到"新建Project对话框](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)
