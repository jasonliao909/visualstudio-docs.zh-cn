---
title: CommandName 元素|Microsoft Docs
description: CommandName 元素指定在"选项"对话框的键盘类别和"自定义"对话框中的"命令"列表中显示的文本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- CommandName element (VSCT XML schema)
- VSCT XML schema elements, CommandName
ms.assetid: a338b767-aa7e-4536-9908-e19a50ab60ac
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c76a96c86a9c6e83ca6b787286ce22ed881161bb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600996"
---
# <a name="commandname-element"></a>CommandName 元素
`CommandName`元素指定在"选项"对话框的键盘类别和"自定义"对话框中的"命令"**列表中** 显示的文本。

## <a name="syntax"></a>语法

```
<CommandName>MyCommand</CommandName>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[Strings 元素](../extensibility/strings-element.md)|对文本元素（如 和 ） `ButtonText` 进行分组 `CommandName` 。|

## <a name="see-also"></a>另请参阅
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
