---
title: CvWriteFlag 函数 | Microsoft Docs
description: 请参阅并发可视化工具 SDK 函数 CvWriteFlag（C 库）的参考信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkers/CvWriteFlagExVA
- cvmarkers/CvWriteFlagExW
- cvmarkers/CvWriteFlagExVW
- cvmarkers/CvWriteFlagExA
helpviewer_keywords:
- CvWriteFlagExW method
- CvWriteFlagExVA method
- CvWriteFlagExA method
- CvWriteFlagExVW method
ms.assetid: ee9da1e2-7b34-4cba-81e2-215d25d32e4d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 4722a70c1a298ce16e801a902648f810bb559cd6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122076719"
---
# <a name="cvwriteflag-function"></a>CvWriteFlag 函数
向并发可视化工具跟踪文件写入一个标志。

## <a name="syntax"></a>语法

```C
HRESULT CvWriteFlagExW(
    _In_reads_bytes_(16) PCV_MARKERSERIES pMarkerSeries,
    _In_ CV_IMPORTANCE level,
    _In_ int category,
    _In_ PCWSTR pMessage,
    ...
    );

HRESULT CvWriteFlagExA(
    _In_reads_bytes_(16) PCV_MARKERSERIES pMarkerSeries,
    _In_ CV_IMPORTANCE level,
    _In_ int category,
    _In_ PCSTR pMessage,
    ...
    );

HRESULT CvWriteFlagExVW(
    _In_reads_bytes_(16) PCV_MARKERSERIES pMarkerSeries,
    _In_ CV_IMPORTANCE level,
    _In_ int category,
    _In_ PCWSTR pMessage,
    _In_ va_list argList);

HRESULT CvWriteFlagExVA(
    _In_reads_bytes_(16) PCV_MARKERSERIES pMarkerSeries,
    _In_ CV_IMPORTANCE level,
    _In_ int category,
    _In_ PCSTR pMessage,
    _In_ va_list argList);
```

#### <a name="parameters"></a>参数
 `argList` 参数列表。

 `category` 类别。

 `level` 重要性级别。

 `pMarkerSeries` 有效标记系列上下文。 不能为 NULL。

 `pMessage` 消息格式字符串。 不能为 NULL。

## <a name="return-value"></a>返回值
 成功写入消息时返回 S_OK。 出现任何错误时返回错误代码。 使用 SUCCEEDED/FAILED 宏检查错误条件。

## <a name="requirements"></a>要求
 **Header:** cvmarkers.h

 **Unicode：** CvWriteFlagExW、CvWriteFlagExVW

 <strong>ANSI：</strong>CvWriteFlagExA、CvWriteFlagExVA

## <a name="see-also"></a>另请参阅
- [C++ 库参考](../profiling/cpp-library-reference.md)