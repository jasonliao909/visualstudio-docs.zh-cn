---
title: T4 CleanUpBehavior 指令
description: 了解 CleanUpBehavior 指令以及如何在处理文本模板后删除 appDomain。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 454522337d57f5f480aecdc30ef69efd39d6a11ab181f6a0324a84109e9c09db
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121370484"
---
# <a name="t4-cleanupbehavior-directive"></a>T4 CleanUpBehavior 指令

若要在处理文本模板之后删除 appDomain，请包括以下行：

```
<#@ CleanupBehavior processor="T4VSHost" CleanupAfterProcessingtemplate="true" #>
```

文本模板是在独立于主机进程之外的 appDomain 中进行处理的。 在大多数情况下，在处理了一个文本模板之后，则将再次使用 appdomain 处理下一个模板。 但如果你指定 CleanupBehavior，则将删除 appDomain 并且将在新的 appDomain 中处理下一个模板。

这将减慢文本处理的速度，但可用于确保释放资源。

此指令将仅在 Visual Studio 主机中起作用。
