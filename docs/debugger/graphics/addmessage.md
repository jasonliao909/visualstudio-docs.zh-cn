---
title: AddMessage | Microsoft Docs
description: 使用 VsgDbg 类的 AddMessage 方法将自定义消息添加到图形诊断提醒显示 (HUD)。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 102a0404-a00c-4566-93f3-01bc8df63280
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 98b37dd5df91bd4907869c36e40938a075d67396
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122138973"
---
# <a name="addmessage"></a>AddMessage
将自定义消息添加到图形诊断 HUD（提醒显示）  。

## <a name="syntax"></a>语法

```C++
void AddMessage(
  wchar_t const * szMessage
);
```

#### <a name="parameters"></a>参数
 `szMessage` 要添加到 HUD 的消息。

## <a name="remarks"></a>备注
 图像诊断 HUD 显示在正在图形诊断下运行的应用的左上角。 它显示有关此应用和图形信息捕获的信息以及通过调用此函数添加的消息。

 若要将消息添加到 HUD，不必主动捕获图形信息 - 也就是说，消息可通过 `VsgDbg` 类的实例添加，但首先不要调用 [Init](init.md) 成员函数。 消息只显示在 HUD 中，而不会记录在图形日志文件中。