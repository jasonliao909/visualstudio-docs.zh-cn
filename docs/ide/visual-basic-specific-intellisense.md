---
title: Visual Basic IntelliSense
description: 了解如何使用 Visual Basic 源代码编辑器提供的 IntelliSense 功能。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.Basic.IntelliSense
helpviewer_keywords:
- IntelliSense [Visual Basic]
- IntelliSense [Visual Studio], Visual Basic
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 44b6e8eb5b44089f0aa87c579ea98f6be947bdb9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122150802"
---
# <a name="intellisense-for-visual-basic-code-files"></a>Visual Basic 代码文件的 IntelliSense

Visual Basic 源代码编辑器提供以下 IntelliSense 功能：

## <a name="syntax-tips"></a>语法提示

语法提示显示正在键入的语句的语法。 这对语句而言是有用的，如 [Declare](/dotnet/visual-basic/language-reference/statements/declare-statement)。

## <a name="automatic-completion"></a>自动完成

- 完成各种关键字

     例如，如果键入 `goto` 和一个空格，IntelliSense 会在下拉菜单中显示已定义的标签列表。 支持的其他关键字包括 `Exit`、`Implements`、`Option` 和 `Declare`。

- 完成 `Enum` 和 `Boolean`

    语句引用枚举成员时，IntelliSense 会显示 `Enum` 成员列表。 语句引用 `Boolean` 时，IntelliSense 会显示 true-false下拉菜单。

可默认关闭完成，方法是在“Visual Basic”文件夹中，从“常规”属性页取消选择“自动列出成员”。

可通过调用列表成员、完成单词或 Alt+向右键，手动调用完成。 有关详细信息，请参阅[使用 IntelliSense](../ide/using-intellisense.md)。

## <a name="intellisense-in-zone"></a>IntelliSense in Zone

IntelliSense in Zone 可在 Visual Basic 开发人员需要通过 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署应用程序并限制为部分信任设置时提供帮助。 此功能：

- 使你可以选择运行应用程序的权限。

- 显示所选区域中在列表成员中可用的 API，并显示需要将其他权限设置为不可用的 API。

有关详细信息，请参阅 [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)。

## <a name="filtered-completion-lists"></a>经过筛选的完成列表

在 Visual Basic 中，IntelliSense 完成列表在列表底部附近有两个选项卡控件。 “常规”选项卡：在默认情况下处于选中状态，显示了最常用的补全正在编写的语句的项。 “全部”选项卡：显示了可用来自动补全的所有项，其中包括“常规”选项卡中的项。

## <a name="see-also"></a>请参阅

- [使用 IntelliSense](../ide/using-intellisense.md)
