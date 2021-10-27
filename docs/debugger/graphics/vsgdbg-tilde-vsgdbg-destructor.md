---
description: 销毁 VsgDbg 类的实例。
title: VsgDbg::~VsgDbg（析构函数）| Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 7a3b97fb-d344-4df7-b195-9347d1edfcf7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 3a0331d0919a52ed91cf973a274a01220dc88f2a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640961"
---
# <a name="vsgdbgvsgdbg-destructor"></a>VsgDbg::~VsgDbg（析构函数）
销毁 `VsgDbg` 类的实例。 如果正在主动记录图形信息，则完成并关闭图形日志文件，并释放在主动捕获图形信息时使用的资源。

## <a name="syntax"></a>语法

```C++
~VsgDbg();
```

## <a name="see-also"></a>请参阅
- [VsgDbg::VsgDbg（构造函数）](vsgdbg-vsgdbg-constructor.md)
