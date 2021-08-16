---
title: 将目录添加到 "添加新项" 对话框 |Microsoft Docs
description: 了解如何通过使用注册表脚本注册目录，将目录添加到 Visual Studio 中的 "添加新项" 对话框。
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
ms.openlocfilehash: f25059d48867af36776cd08b27871e621e56226c8f4f3ae7d99d74bae2486bd9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121275718"
---
# <a name="add-directories-to-the-add-new-item-dialog-box"></a>将目录添加到 "添加新项" 对话框
下面的代码示例演示如何为 " **添加新项** " 对话框注册一组新的目录。 每个项目的 " **添加新项** " 对话框的目录不同。 因此，在 " **项目** " 子项下注册目录，在 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\Projects** 中找到。

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

 `%Template_Path%`值指定包含项目模板的目录的完整路径。 这些模板可以是要克隆的 *.vsz* 文件或原型模板文件。

 `SortPriority`该值指定排序优先级。

## <a name="add-items-to-an-existing-project"></a>向现有项目中添加项
 你还可以向现有项目中添加项。 例如，对于 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 项目，可以将项添加到 *\<root> \Program Files \ Microsoft Visual Studio \VC # \CSharpProjectItems\LocalProjectItems* 文件夹中。 在这种情况下， `%GUID_Project%` 是 c # 项目 ( {FAE04EC0-301F-11D3-BF4B-00C04F79EFBC} ) 的 GUID。

 还可以通过编程项目子类型来扩展现有项目。 使用项目子类型，可以扩展项目，而无需编写新的项目类型。 有关项目子类型的详细信息，请参阅[Project 子类型](../../extensibility/internals/project-subtypes.md)。

## <a name="see-also"></a>另请参阅
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [向 "添加新项" 对话框添加项](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [将目录添加到 "新建 Project" 对话框](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)
