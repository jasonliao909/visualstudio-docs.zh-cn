---
title: 为代码添加注释
description: 本指南介绍如何使用 Visual Studio for Mac 的源代码编辑器中的注释
author: cobey
ms.author: cobey
ms.date: 05/06/2018
ms.assetid: 0FE5E929-1846-4F48-B5E3-70990FAF9504
ms.topic: how-to
ms.openlocfilehash: a0aa3de91f1a2c75d73409d89f3cbc8894faacab
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736766"
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