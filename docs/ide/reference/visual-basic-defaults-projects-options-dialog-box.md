---
title: “选项”对话框 ->“项目”->“Visual Basic 默认值”
description: 了解如何使用“项目和解决方案”部分中的“Visual Basic 默认值”页来指定 Visual Basic 项目选项的默认设置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Projects.VBDefaults
helpviewer_keywords:
- Option Explicit statement, setting in the IDE
- Option Compare statement, setting in the IDE
- Option Strict statement, setting in the IDE
ms.assetid: 2465cd9d-18b6-4c4a-b1ea-86dbab23fc79
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 8252581f7255e8fd04ee6e01bfed7fb7e7fe08c2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122123705"
---
# <a name="visual-basic-defaults-projects-options-dialog-box"></a>“选项”对话框 ->“项目”->“Visual Basic 默认值”
指定 Visual Basic 项目选项的默认设置。 创建新项目时，指定选项语句会添加到代码编辑器的项目标头中。 选项应用于所有 Visual Basic 项目。

若要访问此对话框，在“工具”菜单上，单击“选项”，展开“项目和解决方案”文件夹，单击“VB 默认值”。

 Option Explicit

设置编译器默认设置，以便要求变量的显式声明。 默认情况下，“Option Explicit”设置为“On”。 有关详细信息，请参阅 [/optionexplicit](/dotnet/visual-basic/reference/command-line-compiler/optionexplicit)。

 Option Strict

设置编译器默认值，以便要求显式收缩转换且不允许后期绑定。 默认情况下，“Option Strict”设置为“Off”。 有关详细信息，请参见 [/optionstrict](/dotnet/visual-basic/reference/command-line-compiler/optionstrict)。

 Option Compare

设置字符串比较的编译器默认设置：二进制（区分大小写）或文本（不区分大小写）。默认情况下，“Option Compare”设置为“二进制” 。 有关详细信息，请参阅 [/optioncompare](/dotnet/visual-basic/reference/command-line-compiler/optioncompare)。

 Option Infer

设置本地类型推断的编译器默认设置。 默认情况下，新创建的项目的“Option Infer”设置为“On”，在 Visual Basic 以前版本中创建的迁移项目的“Option Infer”设置为“Off”。 有关详细信息，请参阅 [/optioninfer](/dotnet/visual-basic/reference/command-line-compiler/optioninfer)。

## <a name="see-also"></a>另请参阅

- [解决方案和项目](../../ide/solutions-and-projects-in-visual-studio.md)
