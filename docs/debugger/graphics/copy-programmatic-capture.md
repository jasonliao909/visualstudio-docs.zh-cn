---
title: 复制（编程捕获）| Microsoft Docs
description: 使用 VsgDbg 类的 Copy 方法将活动图形日志 (.vsglog) 文件的内容复制到新文件中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 30ec235a-0abb-44b9-8852-61bc9e67ce22
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 26a9aff077e3cb7cda6e809546f850fc6a9fc754
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640715"
---
# <a name="copy-programmatic-capture"></a>复制（编程捕获）
将活动图形日志 (.vsglog) 文件的内容复制到新文件。

## <a name="syntax"></a>语法

```C++
void Copy(
  wchar_t const * szNewVSGLog
);
```

#### <a name="parameters"></a>参数
 `szNewVSGLog` 新图形日志文件的文件名。

## <a name="remarks"></a>备注
 若要将图形信息复制到新文件，您必须已捕获一些图形信息；否则，不会执行任何操作。