---
title: VsgDbg::~VsgDbg（析构函数）| Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7a3b97fb-d344-4df7-b195-9347d1edfcf7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 53d969e6be772b446598c9c3644582684be488a8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99861343"
---
# <a name="vsgdbgvsgdbg-destructor"></a>VsgDbg::~VsgDbg（析构函数）
销毁 `VsgDbg` 类的实例。 如果正在主动记录图形信息，则完成并关闭图形日志文件，并释放在主动捕获图形信息时使用的资源。

## <a name="syntax"></a>语法

```C++
~VsgDbg();
```

## <a name="see-also"></a>请参阅
- [VsgDbg::VsgDbg（构造函数）](vsgdbg-vsgdbg-constructor.md)