---
title: 为代码添加注释
description: 本指南介绍如何使用 Visual Studio for Mac 的源代码编辑器中的注释
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 05/06/2018
ms.assetid: 0FE5E929-1846-4F48-B5E3-70990FAF9504
ms.topic: reference
ms.openlocfilehash: 266d12d924740740c301dd74aec4358198ab0467
ms.sourcegitcommit: 965372ad0d75f015403c1af508080bf799914ce3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "135806399"
---
# <a name="comments"></a>注释

通过代码进行调试或试验时，它可用来临时或长期注释代码块。

注释掉整个代码块：

* 选择代码并从上下文菜单中选择“切换行注释”

或

* 在所选代码上使用 `cmd + /` 键绑定。

这些方法可用来注释和取消注释代码部分。 在 C# 文件中，可以添加其他级别的行注释，以允许注释和取消注释代码区域，同时仍然保留实际注释：

![多级别注释](media/source-editor-image8.png)

注释还可用于为可能与之交互的未来开发者编写代码。 这些功能通常以多行注释的形式完成，可以在每种语言中通过以下方法添加：

**C#**

```csharp
/*
 This is a multi-line
 comment in C#
*/
```

**F#**

```fsharp
(*
 This is a multi-line
  comment in F#
*)
```

## <a name="see-also"></a>请参阅

- [为代码添加注释（Windows 上的 Visual Studio）](/visualstudio/ide/quickstart-editor#comment-out-code)