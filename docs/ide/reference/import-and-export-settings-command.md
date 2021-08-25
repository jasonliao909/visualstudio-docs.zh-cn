---
description: 导入、导出或重置 Visual Studio 设置。 vssettings 文件扩展名
title: “导入和导出设置”命令
ms.date: 05/28/2021
ms.topic: reference
f1_keywords:
- Tools.ImportandExportSettings
helpviewer_keywords:
- Tools.ImportandExportSettings
- Import and Export Settings command
ms.assetid: 94a06468-a44d-403d-a931-77bbc9d06e56
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 3074371bbf76d3f393e89655d85e2ed1a08ec58e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122101266"
---
# <a name="import-and-export-settings-command-vssettings-file"></a>导入和导出设置命令（.vssettings 文件）

导入、导出或重置 Visual Studio 设置文件 `.vssettings`。

文件的架构是开放的。 大多数情况下，架构遵循 XML 结构，其中每个类别都是一个标记，该标记本身可以包含子类别标记。 这些子类别标记可以包含属性值标记。 虽然大多数包都使用相同结构，但 Visual Studio 中的包都可以使用它选择的架构向文件提供任意 XML。

## <a name="syntax"></a>语法

```cmd
Tools.ImportandExportSettings [/export:filename | /import:filename | /reset]
```

## <a name="switches"></a>交换机

/export:`filename`

可选。 将当前设置导出到指定文件。

/import:`filename`

可选。 导入指定文件中的设置。

/reset

可选。 重置当前设置。

## <a name="remarks"></a>备注

不带任何开关运行此命令将打开“导入和导出设置”向导。 有关详细信息，请参阅[同步设置](../synchronized-settings-in-visual-studio.md)和[环境设置](../environment-settings.md)。

## <a name="example"></a>示例

以下命令将当前设置导出到文件 `MyFile.vssettings`：

```cmd
Tools.ImportandExportSettings /export:"c:\Files\MyFile.vssettings"
```



## <a name="see-also"></a>另请参阅

- [环境设置](../../ide/environment-settings.md)
- [同步设置](../../ide/synchronized-settings-in-visual-studio.md)
- [个性化设置 Visual Studio IDE](../../ide/personalizing-the-visual-studio-ide.md)
- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
