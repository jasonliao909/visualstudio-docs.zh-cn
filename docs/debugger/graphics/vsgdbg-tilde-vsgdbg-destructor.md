---
description: 销毁 VsgDbg 类的实例。
title: VsgDbg::~VsgDbg（析构函数）| Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 7a3b97fb-d344-4df7-b195-9347d1edfcf7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ddc942d2ef3a33f1f8d843ff5657f76bb58104c4
ms.sourcegitcommit: aeed3eb503d0b282537b073ebae8c028c4fef750
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2021
ms.locfileid: "114232383"
---
# <a name="vsgdbgvsgdbg-destructor"></a>VsgDbg::~VsgDbg（析构函数）
销毁 `VsgDbg` 类的实例。 如果正在主动记录图形信息，则完成并关闭图形日志文件，并释放在主动捕获图形信息时使用的资源。

## <a name="syntax"></a>语法

```C++
~VsgDbg();
```

## <a name="see-also"></a>请参阅
- [VsgDbg::VsgDbg（构造函数）](vsgdbg-vsgdbg-constructor.md)
