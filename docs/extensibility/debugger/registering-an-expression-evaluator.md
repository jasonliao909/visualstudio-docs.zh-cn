---
title: 注册表达式计算|Microsoft Docs
description: 了解表达式计算程序如何将自身注册为类工厂，同时Windows COM 环境和Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluators, registering
ms.assetid: 236be234-e05f-4ad8-9200-24ce51768ecf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: b61f14810834e8d019811f2385b1596d2afde911825d03d81bdf233630be56dd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121276147"
---
# <a name="register-an-expression-evaluator"></a>注册表达式计算程序
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表达式计算 (企业版) 必须同时使用 COM 环境和 Windows 将自身注册为Visual Studio。 企业版设置为 DLL，以便注入调试引擎 (DE) 地址空间或 Visual Studio 地址空间，具体取决于实例化 企业版 的实体。

## <a name="managed-code-expression-evaluator"></a>托管代码表达式评估程序
 托管代码企业版作为类库实现，该类库是一个 DLL，它向 COM 环境注册自身，通常通过调用 VSIP 程序启动 *，regpkg.exe。* 为 COM 环境编写注册表项的实际过程会自动处理。

 主类的一个方法标记为 ，指示在向 COM 注册 DLL 时 <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> 将调用方法。 此注册方法（通常称为 ）执行向 Visual Studio `RegisterClass` 注册 DLL 的任务。 使用 `UnregisterClass` (标记的相应 <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute>) ，撤消 `RegisterClass` 卸载 DLL 时 的效果。
对于以非托管代码编写的企业版注册表项相同;唯一的区别是，没有帮助程序函数（例如 `SetEEMetric` ）来执行工作。 下面是注册和注销过程的示例。

### <a name="example"></a>示例
 以下函数演示托管代码如何企业版注册和注销自身Visual Studio。

```csharp
namespace EEMC
{
    [GuidAttribute("462D4A3D-B257-4AEE-97CD-5918C7531757")]
    public class EEMCClass : IDebugExpressionEvaluator
    {
        #region Register and unregister.
        private static Guid guidMycLang = new Guid("462D4A3E-B257-4AEE-97CD-5918C7531757");
        private static string languageName = "MyC";
        private static string eeName = "MyC Expression Evaluator";

        private static Guid guidMicrosoftVendor = new Guid("994B45C4-E6E9-11D2-903F-00C04FA302A1");
        private static Guid guidCOMPlusOnlyEng = new Guid("449EC4CC-30D2-4032-9256-EE18EB41B62B");
        private static Guid guidCOMPlusNativeEng = new Guid("92EF0900-2251-11D2-B72E-0000F87572EF");

        /// <summary>
        /// Register the expression evaluator.
        /// Set "project properties/configuration properties/build/register for COM interop" to true.
        /// </summary>
         [ComRegisterFunctionAttribute]
        public static void RegisterClass(Type t)
        {
            // Get Visual Studio version (set by regpkg.exe)
            string hive = Environment.GetEnvironmentVariable("EnvSdk_RegKey");
            string s = @"SOFTWARE\Microsoft\VisualStudio\"
                        + hive
                        + @"\AD7Metrics\ExpressionEvaluator";

            RegistryKey rk = Registry.LocalMachine.CreateSubKey(s);
            if (rk == null)  return;

            rk = rk.CreateSubKey(guidMycLang.ToString("B"));
            rk = rk.CreateSubKey(guidMicrosoftVendor.ToString("B"));
            rk.SetValue("CLSID", t.GUID.ToString("B"));
            rk.SetValue("Language", languageName);
            rk.SetValue("Name", eeName);

            rk = rk.CreateSubKey("Engine");
            rk.SetValue("0", guidCOMPlusOnlyEng.ToString("B"));
            rk.SetValue("1", guidCOMPlusNativeEng.ToString("B"));
        }
        /// <summary>
        /// Unregister the expression evaluator.
        /// </summary>
         [ComUnregisterFunctionAttribute]
        public static void UnregisterClass(Type t)
        {
            // Get Visual Studio version (set by regpkg.exe)
            string hive = Environment.GetEnvironmentVariable("EnvSdk_RegKey");
            string s = @"SOFTWARE\Microsoft\VisualStudio\"
                        + hive
                        + @"\AD7Metrics\ExpressionEvaluator\"
                        + guidMycLang.ToString("B");
            RegistryKey key = Registry.LocalMachine.OpenSubKey(s);
            if (key != null)
            {
                key.Close();
                Registry.LocalMachine.DeleteSubKeyTree(s);
            }
        }
    }
}
```

## <a name="unmanaged-code-expression-evaluator"></a>非托管代码表达式计算程序
 该企业版 DLL 实现 函数，以向 COM 环境注册自身 `DllRegisterServer` 以及Visual Studio。

> [!NOTE]
> 可以在文件 *dllentry.cpp* 中查找 MyCEE 代码示例注册表代码，该文件位于 ENVSDK\MyCPkgs\MyCEE 下的 VSIP 安装中。

### <a name="dll-server-process"></a>DLL 服务器进程
 在注册企业版时，DLL 服务器：

1. 根据常规 COM 约定 `CLSID` 注册其类工厂。

2. 调用帮助程序函数 `SetEEMetric` 以注册Visual Studio企业版下表中所示的一些指标。 如下所示 `SetEEMetric` 指定的函数和指标是 *dbgmetric.lib 库的一* 部分。 有关详细信息 [，请参阅用于调试的 SDK](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) 帮助程序。

    |指标|说明|
    |------------|-----------------|
    |`metricCLSID`|`CLSID`企业版类工厂的|
    |`metricName`|以可企业版字符串形式显示的名称|
    |`metricLanguage`|用于评估企业版语言的名称|
    |`metricEngine`|`GUID`调试引擎的 (DE) 可处理此企业版|

    > [!NOTE]
    > `metricLanguage``GUID`按名称标识语言，但选择该语言的 `guidLang` 是 `SetEEMetric` 的参数。 当编译器生成调试信息文件时，它应编写适当的 ，以便 DE 知道企业版 `guidLang` 版本。 DE 通常会请求此语言的符号提供程序 `GUID` ，该提供程序存储在调试信息文件中。

3. 通过创建Visual Studio X.Y 下的HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio注册到 Visual Studio，其中 \\ *X.Y* 是要注册的 Visual Studio版本。 

### <a name="example"></a>示例
 以下函数演示 C++ 中的非托管 (如何使用) 企业版 注册和注销自身Visual Studio。

```cpp
/*---------------------------------------------------------
  Registration
-----------------------------------------------------------*/
#ifndef LREGKEY_VISUALSTUDIOROOT
    #define LREGKEY_VISUALSTUDIOROOT L"Software\\Microsoft\\VisualStudio\\8.0"
#endif

static HRESULT RegisterMetric( bool registerIt )
{
    // check where we should register
    const ULONG cchBuffer = _MAX_PATH;
    WCHAR wszRegistrationRoot[cchBuffer];
    DWORD cchFreeBuffer = cchBuffer - 1;
    wcscpy(wszRegistrationRoot, LREGKEY_VISUALSTUDIOROOT_NOVERSION);
    wcscat(wszRegistrationRoot, L"\\");

    // this is Environment SDK specific
    // we check for  EnvSdk_RegKey environment variable to
    // determine where to register
    DWORD cchDefRegRoot = lstrlenW(LREGKEY_VISUALSTUDIOROOT_NOVERSION) + 1;
    cchFreeBuffer = cchFreeBuffer - cchDefRegRoot;
    DWORD cchEnvVarRead = GetEnvironmentVariableW(
        /* LPCTSTR */ L"EnvSdk_RegKey", // environment variable name
        /* LPTSTR  */ &wszRegistrationRoot[cchDefRegRoot],// buffer for variable value
        /* DWORD   */ cchFreeBuffer);// size of buffer
    if (cchEnvVarRead >= cchFreeBuffer)
        return E_UNEXPECTED;
    // If the environment variable does not exist then we must use
    // LREGKEY_VISUALSTUDIOROOT which has the version number.
    if (0 == cchEnvVarRead)
        wcscpy(wszRegistrationRoot, LREGKEY_VISUALSTUDIOROOT);

    if (registerIt)
    {
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricCLSID,
                    CLSID_MycEE,
                    wszRegistrationRoot );
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricName,
                    GetString(IDS_INFO_MYCDESCRIPTION),
                    wszRegistrationRoot );
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricLanguage, L"MyC",
                    wszRegistrationRoot);

        GUID engineGuids[2];
        engineGuids[0] = guidCOMPlusOnlyEng;
        engineGuids[1] = guidCOMPlusNativeEng;
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricEngine,
                    engineGuids,
                    2,
                    wszRegistrationRoot);
    }
    else
    {
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricCLSID,
                        wszRegistrationRoot);
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricName,
                        wszRegistrationRoot );
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricLanguage,
                        wszRegistrationRoot );
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricEngine,
                        wszRegistrationRoot );
    }

    return S_OK;
}
```

## <a name="see-also"></a>另请参阅
- [编写 CLR 表达式计算程序](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [用于调试的 SDK 帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
