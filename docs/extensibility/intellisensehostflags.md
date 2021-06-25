---
title: IntelliSenseHostFlags |Microsoft Docs
description: IntelliSenseHostFlags 枚举指定 IntelliSense 主机标志。 本文介绍枚举值。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IntellisenseHostFlags
helpviewer_keywords:
- IntelliSense, IntellisenseHostFlags enumeration
- IntellisenseHostFlags enumeration
ms.assetid: 0930640b-eb84-48ef-a8f7-d4268f55c99c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 33345f86c69d0faeaa5863534e21eca5ecc176cc
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902613"
---
# <a name="intellisensehostflags"></a>IntelliSenseHostFlags
指定 IntelliSense 主机标志。

## <a name="syntax"></a>语法

```cpp
enum IntellisenseHostFlags
{
    IHF_READONLYCONTEXT      = 0x00000001
    IHF_NOSEPARATESUBJECT    = 0x00000002
    IHF_SINGLELINESUBJECT    = 0x00000004
    IHF_FORCECOMMITTOCONTEXT = 0x00000008
    IHF_OVERTYPE             = 0x00000010
};
```

### <a name="parameters"></a>参数

|成员|描述|
|-------------|-----------------|
|`IHF_READONLYCONTEXT`|上下文缓冲区为只读。|
|`IHF_NOSEPARATESUBJECT`|无主题文本。 上下文缓冲区包含 IntelliSense-目标 (表示 `!IHF_READONLYCONTEXT`) 。|
|`IHF_SINGLELINESUBJECT`|主题文本不支持多行。|
|`IHF_FORCECOMMITTOCONTEXT`|与 `CanCommitIntoReadOnlyBuffer` 相同。|
|`IHF_OVERTYPE`|在主题或上下文) 中编辑 (应在改写模式下完成。|

## <a name="requirements"></a>要求
 SingleFileeditor .idl

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.TextManager.Interop>
