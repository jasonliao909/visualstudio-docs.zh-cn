---
title: CV_CPU_TYPE_e | Microsoft Docs
description: 获取有关 CV_CPU_TYPE_e 枚举类型的参考信息，该类型指定调试接口访问 SDK 中的目标处理器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CV_CPU_TYPE_e enumeration
ms.assetid: df470a7e-1d04-448e-b920-c731189514fa
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 7cf2450701ed3543b7bd210a268875ef7e4b04b1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832390"
---
# <a name="cv_cpu_type_e"></a>CV_CPU_TYPE_e
指定目标处理器。

> [!NOTE]
> 处理器是在 `CV_CFL_*` 前缀后的枚举元素中标识的。

## <a name="syntax"></a>语法

```C++
typedef enum CV_CPU_TYPE_e {
    CV_CFL_8080         = 0x00,
    CV_CFL_8086         = 0x01,
    CV_CFL_80286        = 0x02,
    CV_CFL_80386        = 0x03,
    CV_CFL_80486        = 0x04,
    CV_CFL_PENTIUM      = 0x05,
    CV_CFL_PENTIUMII    = 0x06,
    CV_CFL_PENTIUMPRO   = CV_CFL_PENTIUMII,
    CV_CFL_PENTIUMIII   = 0x07,
    CV_CFL_MIPS         = 0x10,
    CV_CFL_MIPSR4000    = CV_CFL_MIPS,
    CV_CFL_MIPS16       = 0x11,
    CV_CFL_MIPS32       = 0x12,
    CV_CFL_MIPS64       = 0x13,
    CV_CFL_MIPSI        = 0x14,
    CV_CFL_MIPSII       = 0x15,
    CV_CFL_MIPSIII      = 0x16,
    CV_CFL_MIPSIV       = 0x17,
    CV_CFL_MIPSV        = 0x18,
    CV_CFL_M68000       = 0x20,
    CV_CFL_M68010       = 0x21,
    CV_CFL_M68020       = 0x22,
    CV_CFL_M68030       = 0x23,
    CV_CFL_M68040       = 0x24,
    CV_CFL_ALPHA        = 0x30,
    CV_CFL_ALPHA_21064  = 0x30,
    CV_CFL_ALPHA_21164  = 0x31,
    CV_CFL_ALPHA_21164A = 0x32,
    CV_CFL_ALPHA_21264  = 0x33,
    CV_CFL_ALPHA_21364  = 0x34,
    CV_CFL_PPC601       = 0x40,
    CV_CFL_PPC603       = 0x41,
    CV_CFL_PPC604       = 0x42,
    CV_CFL_PPC620       = 0x43,
    CV_CFL_PPCFP        = 0x44,
    CV_CFL_SH3          = 0x50,
    CV_CFL_SH3E         = 0x51,
    CV_CFL_SH3DSP       = 0x52,
    CV_CFL_SH4          = 0x53,
    CV_CFL_SHMEDIA      = 0x54,
    CV_CFL_ARM3         = 0x60,
    CV_CFL_ARM4         = 0x61,
    CV_CFL_ARM4T        = 0x62,
    CV_CFL_ARM5         = 0x63,
    CV_CFL_ARM5T        = 0x64,
    CV_CFL_ARM6         = 0x65,
    CV_CFL_ARM_XMAC     = 0x66,
    CV_CFL_ARM_WMMX     = 0x67,
    CV_CFL_OMNI         = 0x70,
    CV_CFL_IA64         = 0x80,
    CV_CFL_IA64_1       = 0x80,
    CV_CFL_IA64_2       = 0x81,
    CV_CFL_CEE          = 0x90,
    CV_CFL_AM33         = 0xA0,
    CV_CFL_M32R         = 0xB0,
    CV_CFL_TRICORE      = 0xC0,
    CV_CFL_X64          = 0xD0,
    CV_CFL_AMD64        = CV_CFL_X64,
    CV_CFL_EBC          = 0xE0,
    CV_CFL_THUMB        = 0xF0
    CV_CFL_ARMNT        = 0xF4,
    CV_CFL_ARM64        = 0xF6,
    CV_CFL_D3D11_SHADER = 0x100,
} CV_CPU_TYPE_e;
```

## <a name="remarks"></a>备注
此枚举中的值是通过调用 [IDiaSymbol::get_platform](../../debugger/debug-interface-access/idiasymbol-get-platform.md) 方法返回的。

## <a name="requirements"></a>要求
标头：cvconst.h

## <a name="see-also"></a>另请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_platform](../../debugger/debug-interface-access/idiasymbol-get-platform.md)
