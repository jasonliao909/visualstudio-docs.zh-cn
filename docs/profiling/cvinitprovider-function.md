---
title: CvInitProvider 函数 | Microsoft Docs
description: 请参阅并发可视化工具 SDK 函数 CvInitProvider（C 库）的参考信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkers/CvInitProvider
helpviewer_keywords:
- CvInitProvider method
ms.assetid: ba1863ad-e35f-4d34-a2f2-5e68957d1915
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0d1b41d9d62bbf5a159ec3a9d60f4e2edf5cc115
ms.sourcegitcommit: d13f7050c873b6284911d1f4acf07cfd29360183
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2021
ms.locfileid: "98686501"
---
# <a name="cvinitprovider-function"></a>CvInitProvider 函数
初始化标记提供程序。 必须在任何其他并发可视化工具 SDK 函数之前调用。

## <a name="syntax"></a>语法

```C
HRESULT CvInitProvider(
   _In_ const GUID* pGuid,
   _Out_ PCV_PROVIDER* ppProvider
);
```

#### <a name="parameters"></a>参数
 `pGuid` 提供程序 guid。 不能为 NULL。

 `ppProvider` 输出变量的地址，用于存储提供程序上下文。 不能为 NULL。

## <a name="return-value"></a>返回值
 成功初始化提供程序时返回 S_OK，出现任何错误时返回错误代码。 使用 SUCCEEDED/FAILED 宏检查错误条件。

## <a name="requirements"></a>要求
 **Header:** cvmarkers.h

## <a name="see-also"></a>另请参阅
- [C++ 库参考](../profiling/cpp-library-reference.md)