---
title: WriteContextTLogs | Microsoft Docs
description: 了解为当前上下文写入日志文件的 WriteContextTLogs 的语法、要求和返回值。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- WriteContextTLogs
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- WriteContextTLogs
ms.assetid: ffc6c7be-3f22-4624-9ffc-0122fe72b6ec
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 32f692012c5a60caf4988142b03b5610a0ebf717
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122076965"
---
# <a name="writecontexttlogs"></a>WriteContextTLogs

写入当前上下文的日志文件。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI WriteContextTLogs(LPCTSTR intermediateDirectory, LPCTSTR tlogRootName);
```

#### <a name="parameters"></a>参数

[in] `intermediateDirectory`

 存储跟踪日志的目录。

[in] `tlogRootName`

 日志文件名的根名称。

## <a name="return-value"></a>返回值

 如果跟踪上下文创建完成，则返回带 SUCCEEDED 位集的 HRESULT 。

## <a name="requirements"></a>要求

 **标头：FileTracker.h** 

## <a name="see-also"></a>另请参阅

- [WriteAllTLogs](../msbuild/writealltlogs.md)