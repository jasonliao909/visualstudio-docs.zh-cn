---
title: CvCreateMarkerSeriesWithCodePageA 函数 | Microsoft Docs
description: 请参阅并发可视化工具 SDK 函数 CvCreateMarkerSeriesWithCodePageA（C 库）的参考信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmakers/CvCreateMarkerSeriesWithCodePageA
helpviewer_keywords:
- CvCreateMarkerSeriesWithCodePageA method
ms.assetid: 3d7ed601-2222-4be9-a557-f217db008753
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 187cc85b3bcdb552a491dd20e866a9f02e025fd2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122084527"
---
# <a name="cvcreatemarkerserieswithcodepagea-function"></a>CvCreateMarkerSeriesWithCodePageA 函数
为给定提供程序和指定代码页创建标记系列。 此函数可用于为标记 API ANSI 函数写出的文本显式指定代码页。 设置代码页对不同计算机使用不同的区域设置或语言来捕获然后分析跟踪非常有用。 默认情况下使用 GetACP() 函数返回的代码页。

## <a name="syntax"></a>语法

```C
HRESULT CvCreateMarkerSeriesWithCodePageA(
   _In_ PCV_PROVIDER pProvider,
   _In_ LPCSTR pSeriesName,
   _In_ UINT nTextCodePage,
   _Out_ PCV_MARKERSERIES* ppMarkerSeries
);
```

#### <a name="parameters"></a>参数
 `pProvider` 先前由 CvInitProvider 初始化的提供程序对象。 不能为 NULL。

 `pSeriesName` 标记系列名称。 不能为 NULL，但允许空字符串。

 `nTextCodePage` 有效的代码页。

 `ppMarkerSeries` 输出变量的地址，用于存储标记系列上下文。 不能为 NULL。

## <a name="return-value"></a>返回值
 成功创建标记系列时返回 S_OK，出现任何错误时返回错误代码。 使用 SUCCEEDED/FAILED 宏检查错误条件。

## <a name="requirements"></a>要求
 **Header:** cvmarkers.h

## <a name="see-also"></a>另请参阅
- [C++ 库参考](../profiling/cpp-library-reference.md)