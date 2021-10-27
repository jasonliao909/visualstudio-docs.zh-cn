---
title: 调试源文件/解决方案属性页面
description: 访问 Visual Studio 中的“调试源文件”属性页，方法是在“解决方案资源管理器”中右键单击你的解决方案，然后选择“属性”>“通用属性”。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.options.FindSource
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
helpviewer_keywords:
- Debug Source Files property page
- debugging [Visual Studio], specifying source and symbol files
- source files, specifying in debugger
- debugger, source files
ms.assetid: 0af11464-eeb1-4d0b-87a6-0cc96779afb1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 4f7e6b894d891004ca275fa4bead1de48ff421f3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640740"
---
# <a name="debug-source-files-common-properties-solution-property-pages-dialog-box"></a>“解决方案属性页”对话框 ->“通用属性”->“调试源文件”
该属性页指定调试器调试解决方案时查找源文件的位置。

 若要访问“调试源文件”属性页，请在“解决方案资源管理器”中右键单击你的解决方案，并从快捷菜单中选择“属性”  。 展开“公共属性”文件夹并单击“调试源文件”页 。

 **包含源代码的目录**：包含一个目录列表，调试器在调试解决方案时将在这些目录中搜索源文件。 还可搜索指定目录的子目录。

 **不查找这些源文件**：输入不希望调试器读取的任何文件的名称。 如果调试器在以上指定的某个目录中找到这些文件之一，它将忽略该文件。 如果调试时出现“查找源”对话框，并点击“取消”，正在搜索的文件会被添加到此列表中，以使调试器不会再搜索该文件 。

## <a name="see-also"></a>请参阅

- [调试器安全](../debugger/debugger-security.md)
- [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)