---
title: MarkProfile | Microsoft Docs
description: MarkProfile 方法可在 .vsp 文件中插入配置文件标记。 包含 MarkProfile 函数的线程的分析必须处于开启状态，才能插入标记。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MarkProfile
ms.assetid: 54dac8c8-c8ee-4023-af27-b25466e3a6ec
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: d8c1f089f96457c25bad703de40311000eaa65fb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122149671"
---
# <a name="markprofile"></a>MarkProfile
`MarkProfile` 方法可在 .vsp 文件中插入配置文件标记。 包含 `MarkProfile` 函数的线程的分析必须处于开启状态，才能插入标记。

## <a name="syntax"></a>语法

```cpp
PROFILE_COMMAND_STATUS PROFILERAPI MarkProfile( long lMarker );
```

#### <a name="parameters"></a>参数
 `lMarker`

 要插入的标记。 标记必须大于或等于零。

## <a name="property-valuereturn-value"></a>属性值/返回值
 函数通过使用 **PROFILE_COMMAND_STATUS** 枚举来指示成功或失败。 返回值可以是下列值之一：

|枚举器|描述|
|----------------|-----------------|
|MARK_ERROR_MARKER_RESERVED|参数小于或等于零。 这些值将保留。 不会记录标记和注释。|
|MARK_ERROR_MODE_NEVER|调用函数时，分析模式设置为“从不”。 不会记录标记和注释。|
|MARK_ERROR_MODE_OFF|调用函数时，分析模式设置为“关闭”。 不会记录标记和注释。|
|MARK_ERROR_NO_SUPPORT|此上下文中无标记支持。 不会记录标记和注释。|
|MARK_ERROR_OUTOFMEMORY|内存不可用来记录事件。 不会记录标记和注释。|
|MARK_TEXTTOOLONG|该字符串超过 256 个字符的最大限制。 注释字符串将截断，且会记录标记和注释。|
|MARK_OK|返回 MARK_OK 以指示成功。|

## <a name="remarks"></a>备注
 如果正在分析包含 MarkProfile 函数的线程，则每次运行代码时，都会向 .vsp 文件插入标记值。 可多次调用 MarkProfile。

 配置文件标记具有全局范围。 例如，在一个线程中插入的配置文件标记可用于标记 .vsp 文件中任何线程的数据段的开头或结尾。

 当使用 Mark 命令或 API 函数（CommentMarkAtProfile、CommentMarkProfile 或 MarkProfile）插入标记和注释时，包含标记配置文件函数的线程的分析状态必须为“开”。

> [!IMPORTANT]
> MarkProfile 方法仅能与检测分析一起使用。

## <a name="net-framework-equivalent"></a>.NET Framework 等效项
 Microsoft.VisualStudio.Profiler.dll

## <a name="function-information"></a>函数信息
 标头：在 VSPerf.h 中声明

 导入库：VSPerf.lib

## <a name="example"></a>示例
 下面的代码阐释了 MarkProfile 函数。

```cpp
void ExerciseMarkProfile()
{
    // Declare and initialize variables to pass to
    // MarkProfile.  The values of these parameters
    // are assigned based on the needs of the code;
    // and for the sake of simplicity in this example,
    // the variables are assigned arbitrary values.
    int markId = 03;

    // Declare enumeration to hold return value of
    // call to MarkProfile.
    PROFILE_COMMAND_STATUS markResult;

    // Variables used to print output.
    HRESULT hResult;
    TCHAR tchBuffer[256];

    markResult = MarkProfile(markId);

    // Format and print result.
    LPCTSTR pszFormat = TEXT("%s %d.\0");
    TCHAR* pszTxt = TEXT("MarkProfile returned");
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,
        pszTxt, markResult);

#ifdef DEBUG
    OutputDebugString(tchBuffer);
#endif
}
```

## <a name="see-also"></a>请参阅
- [Visual Studio 探查器 API 参考（本机）](../profiling/visual-studio-profiler-api-reference-native.md)
