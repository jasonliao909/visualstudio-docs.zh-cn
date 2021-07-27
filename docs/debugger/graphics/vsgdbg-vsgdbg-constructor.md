---
description: 构造 VsgDbg 类的实例（准备或不准备图形诊断的应用内组件）来根据指定的布尔型参数主动捕获并记录图形信息（默认情况下）。
title: VsgDbg::VsgDbg（构造函数）| Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 670651e6-5e79-4845-b0c2-671beb7055a8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e3693301aef27e01f2d12fa954f94fcc55fb8dea
ms.sourcegitcommit: aeed3eb503d0b282537b073ebae8c028c4fef750
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2021
ms.locfileid: "114232422"
---
# <a name="vsgdbgvsgdbg-constructor"></a>VsgDbg::VsgDbg（构造函数）
构造 `VsgDbg` 类的实例（准备或不准备图形诊断的应用内组件）来根据指定的布尔型参数主动捕获并记录图形信息（默认情况下）。

## <a name="syntax"></a>语法

```C++
VsgDbg(
  bDefaultInit
);
```

#### <a name="parameters"></a>参数
 `bDefaultInit` 如果指定图形诊断的应用内组件准备主动捕获并记录图形信息，则为 `true`；如果指定应用此时不应准备主动捕获并记录图形信息，则为 `false`。

## <a name="remarks"></a>备注
 如果在 `bDefaultInit` 设置为 `true` 的情况下调用构造函数，则图形日志文件的文件名由在将 `vsgcapture.h` 包括在应用中之前定义 `DONT_SAVE_VSGLOG_TO_TEMP` 和 `VSG_DEFAULT_RUN_FILENAME` 预处理器符号的方式确定。

 如果在 `bDefaultInit` 设置为 `false` 的情况下调用构造函数，则图形诊断的应用内组件可准备以通过调用 `Init` 函数主动捕获图形信息并在稍后记录该信息。

## <a name="see-also"></a>请参阅
- [VsgDbg::~VsgDbg（析构函数）](vsgdbg-tilde-vsgdbg-destructor.md)
- [Init](init.md)
- [DONT_SAVE_VSGLOG_TO_TEMP](dont-save-vsglog-to-temp.md)
- [VSG_DEFAULT_RUN_FILENAME](vsg-default-run-filename.md)
