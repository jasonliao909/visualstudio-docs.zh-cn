---
title: 用于调试的 SDK 帮助程序 |Microsoft Docs
description: 了解用于实现 c + + 中的调试引擎、表达式计算器和符号提供程序的全局 helper 函数的函数和声明。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- dbgmetric.lib
- registry, Debugging SDK
- Debugging SDK, registry locations
- dbgmetric.h
- metrics [Debugging SDK]
ms.assetid: 80a52e93-4a04-4ab2-8adc-a7847c2dc20b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: fd85921256d8212a1d02d2d24277ff2ed71dde97
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103060"
---
# <a name="sdk-helpers-for-debugging"></a>用于调试的 SDK 帮助程序
这些函数和声明是用于实现 c + + 中的调试引擎、表达式计算器和符号提供程序的全局帮助器函数。

> [!NOTE]
> 目前没有这些函数和声明的托管版本。

## <a name="overview"></a>概述
 为了使调试引擎、表达式计算器和 Visual Studio 使用的符号提供程序，必须对它们进行注册。 这是通过设置注册表子项和条目来完成的，也称为 "设置度量值"。 以下全局函数旨在简化更新这些度量值的过程。 请参阅注册表位置部分，以了解这些函数更新的每个注册表子项的布局。

## <a name="general-metric-functions"></a>常规度量函数
 这些是调试引擎使用的常规功能。 稍后详细介绍了表达式计算器和符号提供程序的专用函数。

### <a name="getmetric-method"></a>GetMetric 方法
 从注册表检索指标值。

```cpp
HRESULT GetMetric(
   LPCWSTR pszMachine,
   LPCWSTR pszType,
   REFGUID guidSection,
   LPCWSTR pszMetric,
   DWORD * pdwValue,
   LPCWSTR pszAltRoot
);
```

|参数|说明|
|---------------|-----------------|
|pszMachine|中可能远程计算机的名称，其寄存器将写入 (`NULL` 表示本地计算机) 。|
|pszType|中度量值类型之一。|
|guidSection|中特定引擎、计算器、异常等的 GUID。这会为特定元素指定指标类型下的子节。|
|pszMetric|中要获取的指标。 这对应于特定的值名称。|
|pdwValue|中指标中值的存储位置。 有多种类型的 GetMetric 可以返回 DWORD (，如本示例所示) 、BSTR、GUID 或 Guid 数组。|
|pszAltRoot|中要使用的备用注册表根目录。 将设置为 `NULL` 以使用默认值。|

### <a name="setmetric-method"></a>SetMetric 方法
 在注册表中设置指定的指标值。

```cpp
HRESULT SetMetric(
         LPCWSTR pszType,
         REFGUID guidSection,
         LPCWSTR pszMetric,
   const DWORD   dwValue,
         bool    fUserSpecific,
         LPCWSTR pszAltRoot
);
```

|参数|说明|
|---------------|-----------------|
|pszType|中度量值类型之一。|
|guidSection|中特定引擎、计算器、异常等的 GUID。这会为特定元素指定指标类型下的子节。|
|pszMetric|中要获取的指标。 这对应于特定的值名称。|
|dwValue|中度量值中值的存储位置。 在此示例中，有几种类型的 SetMetric 可存储 DWORD () 、BSTR、GUID 或 Guid 数组。|
|fUserSpecific|中如果度量值是用户特定的，并且应该写入用户的 hive 而不是本地计算机 hive，则为 TRUE。|
|pszAltRoot|中要使用的备用注册表根目录。 将设置为 `NULL` 以使用默认值。|

### <a name="removemetric-method"></a>RemoveMetric 方法
 从注册表中删除指定的指标。

```cpp
HRESULT RemoveMetric(
   LPCWSTR pszType,
   REFGUID guidSection,
   LPCWSTR pszMetric,
   LPCWSTR pszAltRoot
);
```

|参数|说明|
|---------------|-----------------|
|pszType|中度量值类型之一。|
|guidSection|中特定引擎、计算器、异常等的 GUID。这会为特定元素指定指标类型下的子节。|
|pszMetric|中要删除的度量值。 这对应于特定的值名称。|
|pszAltRoot|中要使用的备用注册表根目录。 将设置为 `NULL` 以使用默认值。|

### <a name="enummetricsections-method"></a>EnumMetricSections 方法
 枚举注册表中的各种指标部分。

```cpp
HRESULT EnumMetricSections(
   LPCWSTR pszMachine,
   LPCWSTR pszType,
   GUID *  rgguidSections,
   DWORD * pdwSize,
   LPCWSTR pszAltRoot
);
```

|参数|说明|
|---------------|-----------------|
|pszMachine|中可能远程计算机的名称，其寄存器将写入 (`NULL` 表示本地计算机) 。|
|pszType|中度量值类型之一。|
|rgguidSections|[in，out]要填充的预先分配的 Guid 数组。|
|pdwSize|中可在数组中存储的最大 Guid 数目 `rgguidSections` 。|
|pszAltRoot|中要使用的备用注册表根目录。 将设置为 `NULL` 以使用默认值。|

## <a name="expression-evaluator-functions"></a>表达式计算器函数

|功能|说明|
|--------------|-----------------|
|GetEEMetric|从注册表检索指标值。|
|SetEEMetric|在注册表中设置指定的指标值。|
|RemoveEEMetric|从注册表中删除指定的指标。|
|GetEEMetricFile|获取指定指标中的文件名，并将其加载，并将文件内容作为字符串返回。|

## <a name="exception-functions"></a>异常函数

|功能|说明|
|--------------|-----------------|
|GetExceptionMetric|从注册表检索指标值。|
|SetExceptionMetric|在注册表中设置指定的指标值。|
|RemoveExceptionMetric|从注册表中删除指定的指标。|
|RemoveAllExceptionMetrics|从注册表中删除所有异常指标。|

## <a name="symbol-provider-functions"></a>符号提供程序函数

|功能|说明|
|--------------|-----------------|
|GetSPMetric|从注册表检索指标值。|
|SetSPMetric|在注册表中设置指定的指标值。|
|RemoveSPMetric|从注册表中删除指定的指标。|

## <a name="enumeration-functions"></a>枚举函数

|功能|说明|
|--------------|-----------------|
|EnumMetricSections|枚举指定指标类型的所有指标。|
|EnumDebugEngine|枚举已注册的调试引擎。|
|EnumEEs|枚举已注册的表达式计算器。|
|EnumExceptionMetrics|枚举所有异常指标。|

## <a name="metric-definitions"></a>指标定义
 这些定义可用于预定义的指标名称。 名称对应于各种注册表项和值名称，并且都定义为宽字符字符串：例如 `extern LPCWSTR metrictypeEngine` 。

|预定义指标类型|说明：的基本键 ...。|
|-----------------------------|---------------------------------------|
|metrictypeEngine|所有调试引擎指标。|
|metrictypePortSupplier|所有端口供应商指标。|
|metrictypeException|所有异常指标。|
|metricttypeEEExtension|所有表达式计算器扩展。|

|调试引擎属性|说明|
|-----------------------------|-----------------|
|metricAddressBP|设置为非零值表示支持地址断点。|
|metricAlwaysLoadLocal|设置为非零值，以便始终在本地加载调试引擎。|
|metricLoadInDebuggeeSession|未使用|
|metricLoadedByDebuggee|设置为非零值表示将始终使用或正在调试的程序加载调试引擎。|
|metricAttach|如果设置为非零，则表示支持对现有程序的附件。|
|metricCallStackBP|设置为非零值表示支持调用堆栈断点。|
|metricConditionalBP|设置为非零值表示支持条件断点的设置。|
|metricDataBP|设置为非零值，表示支持对数据更改进行断点设置。|
|metricDisassembly|设置为非零值表示支持拆装列表。|
|metricDumpWriting|设置为非零值，表示支持转储写入 (将内存转储到输出设备) 。|
|metricENC|设置为非零值表示支持 "编辑并继续"。 **注意：**  自定义调试引擎绝不应设置此设置，否则应始终将其设置为0。|
|metricExceptions|设置为非零值表示支持异常。|
|metricFunctionBP|如果设置为非零，则表示支持已命名的断点 (在) 指定某个函数名称时中断的断点。|
|metricHitCountBP|设置为非零值，以指示支持 "点击点" 断点 (仅在达到特定次数) 时触发的断点。|
|metricJITDebug|如果设置为非零，则表示支持实时调试 (调试程序在运行的进程) 中发生异常时启动。|
|metricMemory|未使用|
|metricPortSupplier|如果实现，则将此项设置为端口供应商的 CLSID。|
|metricRegisters|未使用|
|metricSetNextStatement|如果设置为非零，则表示支持设置下一个语句 (这将跳过中间语句的执行) 。|
|metricSuspendThread|设置为非零值以指示支持挂起线程执行。|
|metricWarnIfNoSymbols|如果设置为非零，则指示在没有符号时应通知用户。|
|metricProgramProvider|将此设置为程序提供程序的 CLSID。|
|metricAlwaysLoadProgramProviderLocal|将此值设置为非零值，以指示应始终在本地加载程序提供程序。|
|metricEngineCanWatchProcess|将此值设置为非零值，以指示调试引擎将监视进程事件而不是程序提供程序。|
|metricRemoteDebugging|将此值设置为非零表示支持远程调试。|
|metricEncUseNativeBuilder|将此值设置为非零值，表示 "编辑并继续" 管理器应该使用调试引擎的 encbuild.dll 来生成以进行 "编辑并继续"。 **注意：**  自定义调试引擎绝不应设置此设置，否则应始终将其设置为0。|
|metricLoadUnderWOW64|将此项设置为非零值，指示调试引擎应在调试64位进程时在 WOW 下的调试对象进程中加载;否则，将在 Visual Studio 进程中加载调试引擎， (在 WOW64) 下运行。|
|metricLoadProgramProviderUnderWOW64|将此项设置为非零值，表示当调试 WOW 下的64位进程时，应在调试对象进程中加载程序提供程序。否则，它将加载到 Visual Studio 进程中。|
|metricStopOnExceptionCrossingManagedBoundary|将此值设置为非零值，以指示当跨托管/非托管代码边界引发未经处理的异常时，进程应停止。|
|metricAutoSelectPriority|将此项设置为自动选择调试引擎的优先级 (较高的值等于较高的优先级) 。|
|metricAutoSelectIncompatibleList|包含条目的注册表项，这些条目指定在自动选择中要忽略的调试引擎的 GUID。 这些条目是一个数字 (0、1、2 等) GUID 表示为字符串。|
|metricIncompatibleList|包含条目的注册表项，这些项指定与此调试引擎不兼容的调试引擎的 GUID。|
|metricDisableJITOptimization|将此选项设置为"非零"，以指示应在调试 (禁用托管代码) 实时优化。|

|表达式计算程序属性|说明|
|-------------------------------------|-----------------|
|metricEngine|这保存支持指定表达式计算程序调试引擎的数量。|
|metricPreloadModules|将此选项设置为非零值，以指示在针对程序启动表达式计算程序时，应预加载模块。|
|metricThisObjectName|将此选项设置为"this"对象名称。|

|表达式计算程序扩展属性|说明|
| - |-----------------|
|metricExtensionDll|支持此扩展的 dll 的名称。|
|metricExtensionRegistersSupported|支持的寄存器列表。|
|metricExtensionRegistersEntryPoint|用于访问寄存器的入口点。|
|metricExtensionTypesSupported|支持的类型列表。|
|metricExtensionTypesEntryPoint|用于访问类型的入口点。|

|端口供应商属性|说明|
|------------------------------|-----------------|
|metricPortPickerCLSID|端口选取器 CLSID (一个对话框，用户可以使用该对话框选择端口并添加用于调试) 。|
|metricDisallowUserEnteredPorts|如果无法将用户输入的端口添加到端口供应商 (则非零值，这使得端口选取器对话框实质上是只读) 。|
|metricPidBase|分配进程 ID 时端口供应商使用的基本进程 ID。|

|预定义的 SP 存储类型|说明|
|-------------------------------|-----------------|
|storetypeFile|符号存储在单独的文件中。|
|storetypeMetadata|符号作为元数据存储在程序集中。|

|其他属性|说明|
|------------------------------|-----------------|
|metricShowNonUserCode|将此选项设置为"非零"可显示非使用代码。|
|metricJustMyCodeStepping|将此选项设置为非零，以指示单步执行只能在用户代码中进行。|
|metricCLSID|特定指标类型的对象的 CLSID。|
|metricName|特定指标类型的对象的用户友好名称。|
|metricLanguage|语言名称。|

## <a name="registry-locations"></a>注册表位置
 指标从注册表读取并写入注册表，特别是子 `VisualStudio` 项中的指标。

> [!NOTE]
> 大多数情况下，指标将写入到HKEY_LOCAL_MACHINE键。 但是，有时HKEY_CURRENT_USER将成为目标密钥。 Dbgmetric.lib 处理这两个键。 获取指标时，它会先搜索HKEY_CURRENT_USER，然后搜索HKEY_LOCAL_MACHINE。 设置指标时，参数指定要使用哪个顶级键。

 *[注册表项]*\

 `Software`\

 `Microsoft`\

 `VisualStudio`\

 *[版本根]*\

 *[指标根]*\

 *[指标类型]*\

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|占位符|说明|
|-----------------|-----------------|
|*[注册表项]*|`HKEY_CURRENT_USER` 或 `HKEY_LOCAL_MACHINE`。|
|*[版本根]*|的 Visual Studio (，例如 、 或 `7.0` `7.1` `8.0`) 。 但是，也可使用 **/rootuffix** 开关修改此根 **devenv.exe。** 对于 VSIP，此修饰符通常为 **Exp**，因此版本根为 8.0Exp。|
|*[指标根]*|这是 或 ，具体取决于是否使用 `AD7Metrics` `AD7Metrics(Debug)` dbgmetric.lib 的调试版本。 **注意：**  无论是否使用 dbgmetric.lib，如果调试版本和发布版本之间存在差异，则必须在注册表中反映，则应遵循此命名约定。|
|*[指标类型]*|要写入的指标类型 `Engine` `ExpressionEvaluator` `SymbolProvider` ：、、 等。这些均在 dbgmetric.h 中定义为 `metricTypeXXXX` ， `XXXX` 其中 是特定的类型名称。|
|*[指标]*|要为其分配值以设置指标的条目的名称。 指标的实际组织取决于指标类型。|
|*[指标值]*|分配给指标的值。 值的类型应具有 (字符串、数字等) 取决于指标。|

> [!NOTE]
> 所有 GUID 都以 格式存储 `{GUID}` 。 例如 `{123D150B-FA18-461C-B218-45B3E4589F9B}`。

### <a name="debug-engines"></a>调试引擎
 以下是注册表中调试引擎指标的组织。 `Engine` 是调试引擎的指标类型名称，对应于上述注册表子树中的 *[* 指标类型]。

 `Engine`\

 *[引擎 guid]*\

 `CLSID` = *[class guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 `PortSupplier`\

 `0` = *[端口供应商 guid]*

 `1` = *[端口供应商 guid]*

|占位符|说明|
|-----------------|-----------------|
|*[引擎 guid]*|调试引擎的 GUID。|
|*[class guid]*|实现此调试引擎的 类的 GUID。|
|*[端口供应商 guid]*|端口供应商的 GUID（如果有）。 许多调试引擎使用默认端口供应商，因此不指定自己的供应商。 在这种情况下，子项 `PortSupplier` 将不存在。|

### <a name="port-suppliers"></a>端口提供程序
 以下是注册表中端口供应商指标的组织。 `PortSupplier` 是端口供应商的指标类型名称，对应于 *[指标类型]*。

 `PortSupplier`\

 *[端口供应商 guid]*\

 `CLSID` = *[class guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|占位符|说明|
|-----------------|-----------------|
|*[端口供应商 guid]*|端口供应商的 GUID|
|*[class guid]*|实现此端口供应商的类的 GUID|

### <a name="symbol-providers"></a>符号提供程序
 以下是注册表中符号供应商指标的组织。 `SymbolProvider` 是符号提供程序的指标类型名称，对应于 *[指标类型]*。

 `SymbolProvider`\

 *[符号提供程序 guid]*\

 `file`\

 `CLSID` = *[class guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 `metadata`\

 `CLSID` = *[class guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|占位符|说明|
|-----------------|-----------------|
|*[符号提供程序 guid]*|符号提供程序的 GUID|
|*[class guid]*|实现此符号提供程序的类的 GUID|

### <a name="expression-evaluators"></a>表达式评估器
 以下是注册表中表达式评估器指标的组织。 `ExpressionEvaluator` 是表达式评估器的指标类型名称，对应于 *[指标类型]*。

> [!NOTE]
> 的指标类型未在 dbgmetric.h 中定义，因为假定表达式评估程序的所有指标更改都将经历相应的表达式评估程序指标函数 (子项的布局有点复杂，因此详细信息隐藏在 `ExpressionEvaluator` `ExpressionEvaluator` dbgmetric.lib) 中。

 `ExpressionEvaluator`\

 *[语言 guid]*\

 *[供应商 guid]*\

 `CLSID` = *[class guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 `Engine`\

 `0` = *[调试引擎 guid]*

 `1` = *[调试引擎 guid]*

|占位符|说明|
|-----------------|-----------------|
|*[语言 guid]*|语言的 GUID|
|*[供应商 guid]*|供应商的 GUID|
|*[class guid]*|实现此表达式计算程序类的 GUID|
|*[调试引擎 guid]*|此表达式计算程序用于的调试引擎的 GUID|

### <a name="expression-evaluator-extensions"></a>表达式计算程序扩展
 以下是注册表中表达式评估程序扩展指标的组织。 `EEExtensions` 是表达式计算程序扩展的指标类型名称，对应于 *[指标类型]*。

 `EEExtensions`\

 *[扩展 guid]*\

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|占位符|说明|
|-----------------|-----------------|
|*[扩展 guid]*|表达式计算程序扩展的 GUID|

### <a name="exceptions"></a>例外
 以下是注册表中异常指标的组织。 `Exception` 是异常的指标类型名称，对应于 *[指标类型]*。

 `Exception`\

 *[调试引擎 guid]*\

 *[异常类型]*\

 *[exception]*\

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 *[exception]*\

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|占位符|说明|
|-----------------|-----------------|
|*[调试引擎 guid]*|支持异常的调试引擎的 GUID。|
|*[异常类型]*|用于标识可处理的异常类的子项的常规标题。 典型名称包括 **C++** 异常 **、Win32 异常**、 **公共语言运行时异常** 和 **本机Run-Time检查**。 这些名称还用于标识用户的特定异常类。|
|*[exception]*|异常的名称：例如，_com_error **或 Control-Break**。  这些名称还用于标识用户的特定异常。|

## <a name="requirements"></a>要求
 默认情况下，这些文件位于 SDK 安装目录中 ([!INCLUDE[vs_dev10_ext](../../../extensibility/debugger/reference/includes/vs_dev10_ext_md.md)] *[drive]* \Program Files\Microsoft Visual Studio 2010 SDK \\) 。

 标头：includes\dbgmetric.h

 库：libs\ad2de.lib、libs\dbgmetric.lib

## <a name="see-also"></a>请参阅
- [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
