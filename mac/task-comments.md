---
title: 任务注释
description: 将任务注释添加到代码
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 11/09/2020
ms.topic: reference
ms.assetid: 562DCB46-D8FA-4DC4-AAEA-F274448C4CD2
ms.openlocfilehash: c696aa991592118caf70ddcd7e5226d59d6fc755
ms.sourcegitcommit: fcf47a9c356df7e9636bcab92186923e5c9b8892
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2022
ms.locfileid: "144524071"
---
# <a name="task-comments"></a>任务注释

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

编写代码时，标准做法是显式注释未完成代码、可疑代码或带有警告的快速解决方法。 Visual Studio for Mac 提供的默认信号令牌包括 TODO、HACK、FIXME 和 UNDONE。 可以在“Visual Studio”>“首选项”>“环境”>“任务”下定义个性化令牌，如下图所示  ：

![任务列表首选项](media/source-editor-image10.png)

要添加新的任务注释，请添加包含任务关键字的注释。 例如：

```csharp
//TODO: Finish this for all properties.
```

Visual Studio for Mac 通过在“任务列表”窗口中突出显示这些标记提醒大家注意，可以使用“视图”>“任务”菜单显示该窗口 ：

![显示单个 TODO 项的任务列表窗口](media/source-editor-image11.png)

## <a name="see-also"></a>另请参阅

- [使用任务列表（Windows 上的 Visual Studio）](/visualstudio/ide/using-the-task-list)