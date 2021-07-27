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
ms.workload:
- multiple
ms.openlocfilehash: 5e4006803364407fed4b837ea992a95429c1db39
ms.sourcegitcommit: aeed3eb503d0b282537b073ebae8c028c4fef750
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2021
ms.locfileid: "114232656"
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