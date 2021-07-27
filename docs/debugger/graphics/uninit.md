---
title: UnInit | Microsoft Docs
description: 使用 VsgDbg 的 UnInit() 方法来完成和关闭图形日志文件，并释放日志记录资源。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 4cd4fc0b-974a-4e61-9ea8-0aaa1a0c52ea
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6bb87d210512a3f914384adb99d81695340b1ed5
ms.sourcegitcommit: aeed3eb503d0b282537b073ebae8c028c4fef750
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2021
ms.locfileid: "114232474"
---
# <a name="uninit"></a>UnInit
完成图形日志文件，将其关闭，并且在应用主动记录图形信息时释放已使用的资源。

## <a name="syntax"></a>语法

```C++
void UnInit();
```

## <a name="remarks"></a>备注
 在销毁 `VsgDbg` 类的实例后自动调用 `UnInit`。 如果 `VsgDbg` 实例未主动记录图形信息，则此操作不起作用。

 在对 `UnInit` 类的实例调用 `VsgDbg` 之后，可通过调用 `Init` 创建新的图形日志文件，并通过调用 `UnInit` 完成此日志文件。 您可以重复此操作所需次数以使用相同的 `VsgDbg` 实例来创建多个独立的图形日志文件。

## <a name="see-also"></a>请参阅
- [Init](init.md)