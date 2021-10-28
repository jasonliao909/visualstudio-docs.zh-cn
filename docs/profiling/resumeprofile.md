---
title: ResumeProfile | Microsoft Docs
description: 了解 ResumeProfile 方法如何递减指定分析级别的挂起/继续计数器的值。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ResumeProfile
ms.assetid: 876f145b-ec07-4240-ade6-4f6e44baadce
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: d52e2dccda89829d05bac6e17f5fc0dcdc70cc62
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736851"
---
# <a name="resumeprofile"></a>ResumeProfile
`ResumeProfile` 方法递减指定分析级别的挂起/继续计数器的值。

## <a name="syntax"></a>语法

```cpp
PROFILE_COMMAND_STATUS PROFILERAPI ResumeProfile(
                       PROFILE_CONTROL_LEVEL Level,
                       unsigned int dwId);
```

#### <a name="parameters"></a>参数
 `Level`

 指示性能数据集合可应用到的分析级别。 以下 PROFILE_CONTROL_LEVEL 枚举器可用于指示性能数据集合可应用到的三个级别之一：

|枚举器|描述|
|----------------|-----------------|
|PROFILE_GLOBALLEVEL|全局级别设置影响分析运行中的所有进程和线程。|
|PROFILE_PROCESSLEVEL|进程级别设置影响指定进程包含的所有线程。|
|PROFILE_THREADLEVEL|线程分析级别设置影响指定的线程。|

 `dwId`

 系统生成的进程或线程标识符。

## <a name="property-valuereturn-value"></a>属性值/返回值
 函数通过使用 **PROFILE_COMMAND_STATUS** 枚举来指示成功或失败。 返回值可以是下列值之一：

|枚举器|描述|
|----------------|-----------------|
|PROFILE_ERROR_ID_NOEXIST|分析元素 ID 不存在。|
|PROFILE_ERROR_LEVEL_NOEXIST|指定的分析级别不存在。|
|PROFILE_ERROR_MODE_NEVER|调用函数时，分析模式设置为“从不”。|
|PROFILE_ERROR_NOT_YET_IMPLEMENTED|分析函数调用、分析级别或者调用和级别的组合尚未实现。|
|PROFILE_OK|调用成功。|

## <a name="remarks"></a>备注
 挂起/继续计数器的初始值是 0。 每次调用 SuspendProfile 都会将挂起/继续计数加 1；每次调用 ResumeProfile 则会减 1。

 当挂起/继续计数大于 0 时，该级别的挂起/继续状态为 OFF。 当该计数小于或等于 0 时，挂起/继续状态为 ON。

 当启动/停止状态和挂起/继续状态都为 ON 时，该级别的分析状态为 ON。 对于要分析的线程，该线程的全局、进程和线程级别状态都必须为 ON。

## <a name="net-framework-equivalent"></a>.NET Framework 等效项
 Microsoft.VisualStudio.Profiler.dll

## <a name="function-information"></a>函数信息
 标头：在 VSPerf.h 中声明

 导入库：VSPerf.lib

## <a name="example"></a>示例
 下面的示例演示 ResumeProfile 函数。 该示例假定已对由 [PROFILE_CURRENTID](../profiling/profile-currentid.md) 标识的同一线程或进程调用了 SuspendProfile 方法。

```cpp
void ExerciseResumeProfile()
{
    // The initial value of the Suspend/Resume counter is 0.
    // Each call to SuspendProfile adds 1 to the Suspend/Resume
    // count; each call to ResumeProfile subtracts 1.

    // Variables used to print output.
    HRESULT hResult;
    TCHAR tchBuffer[256];

    // Declare enumeration to hold result of call to ResumeProfile
    PROFILE_COMMAND_STATUS profileResult;

    profileResult = ResumeProfile(
        PROFILE_GLOBALLEVEL,
        PROFILE_CURRENTID);

    // Format and print result.
    LPCTSTR pszFormat = TEXT("%s %d.\0");
    TCHAR* pszTxt = TEXT("ResumeProfile returned");
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,
        pszTxt, profileResult);

#ifdef DEBUG
    OutputDebugString(tchBuffer);
#endif
}
```

## <a name="see-also"></a>请参阅
- [Visual Studio 探查器 API 参考（本机）](../profiling/visual-studio-profiler-api-reference-native.md)
