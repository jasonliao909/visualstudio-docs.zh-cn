---
title: CaptureCurrentFrame | Microsoft Docs
description: 使用 VsgDbg 类的 CaptureCurrentFrame 方法将当前帧的剩余部分捕获到图形日志文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 4509311d-6fe2-4b65-9b4a-ff0522585d6a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 94c55a34ee71f8002d31613d64ff978f0a546b72
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99874543"
---
# <a name="capturecurrentframe"></a>CaptureCurrentFrame
将当前帧的剩余部分捕获到图形日志文件。

## <a name="syntax"></a>语法

```C++
void CaptureCurrentFrame();
```

## <a name="remarks"></a>备注
 如果另一个捕获当前正在进行中（例如，通过 `BeginCapture` 函数启动的捕获），则将完成该捕获并将其记录到图形日志以作为不同的帧。 紧跟着，图形诊断开始捕获当前帧的剩余部分，此部分也记录为不同的帧。 通过调用 present 来标记当前帧的结尾。

 若要捕获帧，必须准备应用以捕获并记录图形信息 - 也就是说，必须在调用 `CaptureCurrentFrame` 之前已通过 `VsgDbg` 类的实例调用 [Init](init.md)。

## <a name="see-also"></a>请参阅
- [Init](init.md)
- [BeginCapture](begincapture.md)