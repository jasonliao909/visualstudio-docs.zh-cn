---
title: 为代码添加注释
description: 本指南介绍如何使用 Visual Studio for Mac 的源代码编辑器中的注释
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 03/03/2022
ms.custom: devdivchpfy22
ms.assetid: 0FE5E929-1846-4F48-B5E3-70990FAF9504
ms.topic: reference
ms.openlocfilehash: 42051a43bd665c186cb6ec8148809954653b5c68
ms.sourcegitcommit: fcf47a9c356df7e9636bcab92186923e5c9b8892
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2022
ms.locfileid: "144505383"
---
# <a name="comments"></a>注释

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

调试或试验代码时，可能需要暂时或长期注释代码块。

注释掉整个代码块：

* 选择代码并从上下文菜单中选择“切换行注释”

或

* 对 `cmd + /` 所选代码使用键绑定。

这些方法可用来注释和取消注释代码部分。

在 C# 文件中，可以添加其他级别的行注释，以允许注释和取消注释代码区域，同时仍然保留实际注释：

![多级别注释](media/source-editor-image8.png)

注释还可用于为可能与之交互的未来开发人员记录代码。 它以多行注释的形式完成，每种语言以以下方式添加：

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