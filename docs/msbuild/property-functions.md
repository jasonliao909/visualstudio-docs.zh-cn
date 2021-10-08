---
title: 属性函数 | Microsoft Docs
description: 了解如何使用属性函数，它们是对在 MSBuild 属性定义中出现的 .NET Framework 方法的调用。
ms.custom: SEO-VS-2020
ms.date: 02/21/2017
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, property functions
ms.assetid: 2253956e-3ae0-4bdc-9d3a-4881dfae4ddb
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: d45b3b46558abf4d16d651d97af1bc722e908a7f
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128429696"
---
# <a name="property-functions"></a>属性函数

属性函数是对在 MSBuild 属性定义中出现的 .NET Framework 方法的调用。 与任务不同，属性函数可在目标外部使用，并在任何目标运行之前进行计算。

可以在生成脚本中读取系统时间、比较字符串、匹配正则表达式及执行其他操作，而无需使用 MSBuild 任务。 MSBuild 将尝试将字符串转换为数字、将数字转换为字符串，并根据需要进行其他转换。

从属性函数返回的字符串值已转义[特殊字符](msbuild-special-characters.md)。 如果要将这些值视为如同直接置于项目文件中，请使用 `$([MSBuild]::Unescape())` 取消转义特殊字符。

.NET Framework 4 及更高版本中提供了属性函数。

## <a name="property-function-syntax"></a>属性函数语法

下面列出了三种属性函数；每种函数都有不同的语法：

- 字符串（实例）属性函数
- 静态属性函数
- MSBuild 属性函数

### <a name="string-property-functions"></a>字符串属性函数

所有生成属性值都只是字符串值。 可以使用字符串（实例）方法来操作任何属性值。 例如，可以使用以下代码，从表示完整路径的生成属性中提取驱动器名称（前三个字符）：

```
$(ProjectOutputFolder.Substring(0,3))
```

### <a name="static-property-functions"></a>静态属性函数

在生成脚本中，可以访问许多系统类的静态属性和方法。 要获取静态属性的值，请使用以下语法，其中 \<Class> 是系统类的名称，\<Property> 是属性的名称。

```
$([Class]::Property)
```

例如，可以使用以下代码将生成属性设置为当前日期和时间。

```xml
<Today>$([System.DateTime]::Now)</Today>
```

要调用静态方法，请使用以下语法，其中 \<Class> 是系统类的名称，\<Method> 是方法的名称，\<Parameters> 是方法的参数列表：

```
$([Class]::Method(Parameters))
```

例如，要将生成属性设置为新的 GUID，可以使用以下脚本：

```xml
<NewGuid>$([System.Guid]::NewGuid())</NewGuid>
```

在静态属性函数中，可以使用以下系统类的任何静态方法或属性：

- <xref:System.Byte?displayProperty=nameWithType>
- <xref:System.Char?displayProperty=nameWithType>
- <xref:System.Convert?displayProperty=nameWithType>
- <xref:System.DateTime?displayProperty=nameWithType>
- <xref:System.Decimal?displayProperty=nameWithType>
- <xref:System.Double?displayProperty=nameWithType>
- <xref:System.Enum?displayProperty=nameWithType>
- <xref:System.Guid?displayProperty=nameWithType>
- <xref:System.Int16?displayProperty=nameWithType>
- <xref:System.Int32?displayProperty=nameWithType>
- <xref:System.Int64?displayProperty=nameWithType>
- <xref:System.IO.Path?displayProperty=nameWithType>
- <xref:System.Math?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.OSPlatform?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.RuntimeInformation?displayProperty=nameWithType>
- <xref:System.UInt16?displayProperty=nameWithType>
- <xref:System.UInt32?displayProperty=nameWithType>
- <xref:System.UInt64?displayProperty=nameWithType>
- <xref:System.SByte?displayProperty=nameWithType>
- <xref:System.Single?displayProperty=nameWithType>
- <xref:System.String?displayProperty=nameWithType>
- <xref:System.StringComparer?displayProperty=nameWithType>
- <xref:System.TimeSpan?displayProperty=nameWithType>
- <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType>
- <xref:System.UriBuilder?displayProperty=nameWithType>
- <xref:System.Version?displayProperty=nameWithType>
- <xref:Microsoft.Build.Utilities.ToolLocationHelper?displayProperty=nameWithType>

此外，还可以使用以下静态方法和属性：

- [System.Environment::CommandLine](xref:System.Environment.CommandLine*)
- [System.Environment::ExpandEnvironmentVariables](xref:System.Environment.ExpandEnvironmentVariables*)
- [System.Environment::GetEnvironmentVariable](xref:System.Environment.GetEnvironmentVariable*)
- [System.Environment::GetEnvironmentVariables](xref:System.Environment.GetEnvironmentVariables*)
- [System.Environment::GetFolderPath](xref:System.Environment.GetFolderPath*)
- [System.Environment::GetLogicalDrives](xref:System.Environment.GetLogicalDrives*)
- [System.IO.Directory::GetDirectories](xref:System.IO.Directory.GetDirectories*)
- [System.IO.Directory::GetFiles](xref:System.IO.Directory.GetFiles*)
- [System.IO.Directory::GetLastAccessTime](xref:System.IO.Directory.GetLastAccessTime*)
- [System.IO.Directory::GetLastWriteTime](xref:System.IO.Directory.GetLastWriteTime*)
- [System.IO.Directory::GetParent](xref:System.IO.Directory.GetParent*)
- [System.IO.File::Exists](xref:System.IO.File.Exists*)
- [System.IO.File::GetCreationTime](xref:System.IO.File.GetCreationTime*)
- [System.IO.File::GetAttributes](xref:System.IO.File.GetAttributes*)
- [System.IO.File::GetLastAccessTime](xref:System.IO.File.GetLastAccessTime*)
- [System.IO.File::GetLastWriteTime](xref:System.IO.File.GetLastWriteTime*)
- [System.IO.File::ReadAllText](xref:System.IO.File.ReadAllText*)

### <a name="calling-instance-methods-on-static-properties"></a>对静态属性调用实例方法

如果访问返回对象实例的静态属性，则可以调用该对象的实例方法。 要调用实例方法，请使用以下语法，其中 \<Class> 是系统类的名称，\<Property> 是属性的名称，\<Method> 是方法的名称，\<Parameters> 是方法的参数列表：

```
$([Class]::Property.Method(Parameters))
```

类的名称必须用命名空间加以完全限定。

例如，使用以下代码可以将生成属性设置为当天的日期：Today。

```xml
<Today>$([System.DateTime]::Now.ToString('yyyy.MM.dd'))</Today>
```

### <a name="msbuild-property-functions"></a>MSBuild 属性函数

可以访问生成中的许多静态方法，以提供算术、按位逻辑和转义字符支持。 可以使用以下语法访问这些方法，其中 \<Method> 是方法的名称，\<Parameters> 是方法的参数列表。

```
$([MSBuild]::Method(Parameters))
```

例如，要一起添加两个具有数字值的属性，请使用以下代码。

```
$([MSBuild]::Add($(NumberOne), $(NumberTwo)))
```

下面列出了 MSBuild 属性函数：

|函数签名|描述|
|------------------------|-----------------|
|double Add(双精度型值 a, 双精度型值 b)|将两个双精度型值相加。|
|long Add(长型值 a, 长型值 b)|将两个长型值相加。|
|double Subtract(双精度型值 a, 双精度型值 b)|将两个双精度型值相减。|
|long Subtract(长型值 a, 长型值 b)|将两个长型值相减。|
|double Multiply(双精度型值 a, 双精度型值 b)|将两个双精度型值相乘。|
|long Multiply(长型值 a, 长型值 b)|将两个长型值相乘。|
|double Divide(双精度型值 a, 双精度型值 b)|将两个双精度型值相除。|
|long Divide(长型值 a, 长型值 b)|将两个长型值相除。|
|double Modulo(双精度型值 a, 双精度型值 b)|对两个双精度型值取模。|
|long Modulo(长型值 a, 长型值 b)|对两个长型值取模。|
|string Escape(未转义字符串)|根据 MSBuild 转义规则对字符串进行转义。|
|string Unescape(已转义字符串)|根据 MSBuild 转义规则取消对字符串进行转义。|
|int BitwiseOr(第一个整型值, 第二个整型值)|对第一个值和第二个值执行按位 `OR`（第一个值 &#124; 第二个值）。|
|int BitwiseAnd(第一个整型值, 第二个整型值)|对第一个值和第二个值执行按位 `AND`（第一个值 & 第二个值）。|
|int BitwiseXor(第一个整型值, 第二个整型值)|对第一个值和第二个值执行按位 `XOR`（第一个值 ^ 第二个值）。|
|int BitwiseNot(第一个整型值)|执行按位 `NOT`（~第一个值）。|
|bool IsOsPlatform(string platformString)|指定当前 OS 平台是否为 `platformString`。 `platformString` 必须属于 <xref:System.Runtime.InteropServices.OSPlatform>。|
|bool IsOSUnixLike()|如果当前 OS 是 Unix 系统，则为 True。|
|string NormalizePath(params string[] path)|获取指定路径的规范化完整路径，并确保其包含当前操作系统的正确目录分隔符。|
|string NormalizeDirectory(params string[] path)|获取指定目录的规范化完整路径，确保其包含当前操作系统的正确目录分隔符，并确保其具有尾部反斜杠。|
|string EnsureTrailingSlash(string path)|如果给定路径没有尾部反斜杠，请添加一个。 如果路径为空字符串，请勿其进行修改。|
|string GetPathOfFileAbove(string file, string startingDirectory)|在当前生成文件位置上级的目录结构中搜索并返回文件的完整路径，如果指定，则基于 `startingDirectory`。|
|GetDirectoryNameOfFileAbove(string startingDirectory, string fileName)|在指定目录或该目录上级的目录结构位置中查找并返回文件目录。|
|string MakeRelative(string basePath, string path)|将 `path` 关联到 `basePath`。 `basePath` 必须是绝对目录。 如果无法关联 `path`，则会返回逐字字符串。 类似于 `Uri.MakeRelativeUri`。|
|string ValueOrDefault(string conditionValue, string defaultValue)|仅当“conditionValue”为空时在参数“defaultValue”中返回字符串，否则返回值 conditionValue。|

## <a name="nested-property-functions"></a>嵌套的属性函数

可将属性函数组合在一起，组成更复杂的函数，如下例所示。

```
$([MSBuild]::BitwiseAnd(32, $([System.IO.File]::GetAttributes(tempFile))))
```

此示例返回由路径 <xref:System.IO.FileAttributes> 所指定文件的 `Archive``tempFile` 位（32 或 0）的值。 请注意，枚举的数据值不能以名称形式显示在属性函数内。 必须改用数字值 (32)。

元数据也可以出现在嵌套的属性函数中。 有关详细信息，请参阅[批处理](../msbuild/msbuild-batching.md)。

## <a name="msbuild-doestaskhostexist"></a>MSBuild DoesTaskHostExist

MSBuild 中的 `DoesTaskHostExist` 属性函数将返回当前是否针对特定运行时和体系结构值安装了任务宿主。

此属性函数具有以下语法：

```
$([MSBuild]::DoesTaskHostExist(string theRuntime, string theArchitecture))
```

## <a name="msbuild-ensuretrailingslash"></a>MSBuild EnsureTrailingSlash

如果尚不存在尾部反斜杠，MSBuild 中的 `EnsureTrailingSlash` 属性函数将添加一条。

此属性函数具有以下语法：

```
$([MSBuild]::EnsureTrailingSlash('$(PathProperty)'))
```

## <a name="msbuild-getdirectorynameoffileabove"></a>MSBuild GetDirectoryNameOfFileAbove

MSBuild `GetDirectoryNameOfFileAbove` 属性函数向上搜索包含指定文件的目录，从指定目录开始（包括指定目录）。 如果找到文件，它将返回包含该文件的最近目录的完整路径，否则返回空字符串。

此属性函数具有以下语法：

```
$([MSBuild]::GetDirectoryNameOfFileAbove(string startingDirectory, string fileName))
```

此示例演示了如何在当前文件夹中或更高一级中导入最近的 EnlistmentInfo.props 文件（仅当找到匹配项时）：

```xml
<Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), EnlistmentInfo.props))\EnlistmentInfo.props" Condition=" '$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), EnlistmentInfo.props))' != '' " />
```

请注意，此示例可以通过使用 `GetPathOfFileAbove` 函数来更简洁地编写：

```xml
<Import Project="$([MSBuild]::GetPathOfFileAbove(EnlistmentInfo.props))" Condition=" '$([MSBuild]::GetPathOfFileAbove(EnlistmentInfo.props))' != '' " />
```

## <a name="msbuild-getpathoffileabove"></a>MSBuild GetPathOfFileAbove

MSBuild `GetPathOfFileAbove` 属性函数向上搜索包含指定文件的目录，从指定目录开始（包括指定目录）。 如果找到文件，它将返回最近匹配文件的完整路径，否则返回空字符串。

此属性函数具有以下语法：

```
$([MSBuild]::GetDirectoryNameOfFileAbove(string file, [string startingDirectory]))
```

其中，`file` 是要搜索的文件的名称，`startingDirectory` 是开始搜索的可选目录。 默认情况下，搜索将在当前文件自身的目录中开始。
 
此示例演示如何在当前目录中或更高一级中导入名为“dir.props”的文件（仅当找到匹配项时）：

```xml
<Import Project="$([MSBuild]::GetPathOfFileAbove(dir.props))" Condition=" '$([MSBuild]::GetPathOfFileAbove(dir.props))' != '' " />
```

这在功能上等效于

```xml
<Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), dir.props))\dir.props" Condition=" '$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), dir.props))' != '' " />
```

但是，有时需要在父目录中开始搜索，以避免与当前文件匹配。 此示例演示 Directory.Build.props 文件如何在严格意义上更高级别的树中导入最近的 Directory.Build.props 文件，而不会以递归方式将自己导入 ：

```xml
<Import Project="$([MSBuild]::GetPathOfFileAbove('Directory.Build.props', '$(MSBuildThisFileDirectory)../'))" />
```

这在功能上等效于

```xml
<Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove('$(MSBuildThisFileDirectory)../', 'Directory.Build.props'))/Directory.Build.props" />
```

## <a name="msbuild-getregistryvalue"></a>MSBuild GetRegistryValue

MSBuild `GetRegistryValue` 属性函数返回注册表项的值。 此函数采用两个参数（项名称和值名称），并从注册表中返回值。 如果未指定值名称，则返回默认值。

下面的示例演示如何使用此函数：

```
$([MSBuild]::GetRegistryValue(`HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Debugger`, ``))                                  // default value
$([MSBuild]::GetRegistryValue(`HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Debugger`, `SymbolCacheDir`))
$([MSBuild]::GetRegistryValue(`HKEY_LOCAL_MACHINE\SOFTWARE\(SampleName)`, `(SampleValue)`))             // parens in name and value
```

## <a name="msbuild-getregistryvaluefromview"></a>MSBuild GetRegistryValueFromView

MSBuild `GetRegistryValueFromView` 属性函数在给定了注册表项、值以及一个或多个经过排序的注册表视图的情况下，获取系统注册表数据。 该属性函数将按顺序在每个注册表视图中搜索注册表项和值，直至找到它们。

该属性函数的语法是：

```
[MSBuild]::GetRegistryValueFromView(string keyName, string valueName, object defaultValue, params object[] views)
```

Windows 64 位操作系统维护一个 HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node 注册表项，它表示 32 位应用程序的 HKEY_LOCAL_MACHINE\SOFTWARE 注册表视图。

默认情况下，在 WOW64 上运行的 32 位应用程序将访问 32 位注册表视图，而 64 位应用程序将访问 64 位注册表视图。

以下这些注册表视图是可用的：

|注册表视图|定义|
|-------------------|----------------|
|RegistryView.Registry32|32 位应用程序注册表视图。|
|RegistryView.Registry64|64 位应用程序注册表视图。|
|RegistryView.Default|与应用程序正在其中运行的进程匹配的注册表视图。|

下面是一个示例。

 ```
$([MSBuild]::GetRegistryValueFromView('HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SDKs\Silverlight\v3.0\ReferenceAssemblies', 'SLRuntimeInstallPath', null, RegistryView.Registry64, RegistryView.Registry32))
```

首先在 64 位注册表视图中查找，然后在 32 位注册表视图中查找，以获取 ReferenceAssemblies 项的 SLRuntimeInstallPath 数据。

## <a name="msbuild-makerelative"></a>MSBuild MakeRelative

MSBuild `MakeRelative` 属性函数将返回第二条路径的相对路径（相对于第一条路径）。 每条路径可以是文件或文件夹。

此属性函数具有以下语法：

```
$([MSBuild]::MakeRelative($(FileOrFolderPath1), $(FileOrFolderPath2)))
```

下面的代码是此语法的示例。

```xml
<PropertyGroup>
    <Path1>c:\users\</Path1>
    <Path2>c:\users\username\</Path2>
</PropertyGroup>

<Target Name = "Go">
    <Message Text ="$([MSBuild]::MakeRelative($(Path1), $(Path2)))" />
    <Message Text ="$([MSBuild]::MakeRelative($(Path2), $(Path1)))" />
</Target>

<!--
Output:
   username\
   ..\
-->
```

## <a name="msbuild-valueordefault"></a>MSBuild ValueOrDefault

MSBuild `ValueOrDefault` 属性函数将返回第一个参数，除非它为 null 或空。 如果第一个参数为 null 或空，则该函数将返回第二个参数。

下面的示例演示如何使用此函数。

```xml
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
        <Value1>$([MSBuild]::ValueOrDefault('$(UndefinedValue)', 'a'))</Value1>
        <Value2>$([MSBuild]::ValueOrDefault('b', '$(Value1)'))</Value2>
    </PropertyGroup>

    <Target Name="MyTarget">
        <Message Text="Value1 = $(Value1)" />
        <Message Text="Value2 = $(Value2)" />
    </Target>
</Project>

<!--
Output:
  Value1 = a
  Value2 = b
-->
```

<a name="TargetFramework"></a>

## <a name="msbuild-targetframework-and-targetplatform-functions"></a>MSBuild TargetFramework 和 TargetPlatform 函数

MSBuild 16.7 及更高版本定义了几个用于处理 [TargetFramework 和 TargetPlatform 属性](msbuild-target-framework-and-target-platform.md)的函数。

|函数签名|描述|
|------------------------|-----------------|
|GetTargetFrameworkIdentifier(string targetFramework)|从 TargetFramework 分析 TargetFrameworkIdentifier。|
|GetTargetFrameworkVersion(string targetFramework)|从 TargetFramework 分析 TargetFrameworkVersion。|
|GetTargetPlatformIdentifier(string targetFramework)|从 TargetFramework 分析 TargetPlatformIdentifier。|
|GetTargetPlatformVersion(string targetFramework)|从 TargetFramework 分析 TargetPlatformVersion。|
|IsTargetFrameworkCompatible(string targetFrameworkTarget, string targetFrameworkCandidate)|如果候选目标框架与此目标框架兼容，则返回“True”，否则返回 false。|

下面的示例演示如何使用这些函数。 

```xml
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
        <Value1>$([MSBuild]::GetTargetFrameworkIdentifier('net5.0-windows7.0'))</Value1>
        <Value2>$([MSBuild]::GetTargetFrameworkVersion('net5.0-windows7.0'))</Value2>
        <Value3>$([MSBuild]::GetTargetPlatformIdentifier('net5.0-windows7.0'))</Value3>
        <Value4>$([MSBuild]::GetTargetPlatformVersion('net5.0-windows7.0'))</Value4>
        <Value5>$([MSBuild]::IsTargetFrameworkCompatible('net5.0-windows', 'net5.0'))</Value5>
    </PropertyGroup>

    <Target Name="MyTarget">
        <Message Text="Value1 = $(Value1)" />
        <Message Text="Value2 = $(Value2)" />
        <Message Text="Value3 = $(Value3)" />
        <Message Text="Value4 = $(Value4)" />
        <Message Text="Value5 = $(Value5)" />
    </Target>
</Project>
```

```output
Value1 = .NETCoreApp
Value2 = 5.0
Value3 = windows
Value4 = 7.0
Value5 = True
```

## <a name="msbuild-version-comparison-functions"></a>MSBuild 版本比较函数

MSBuild 16.5 及更高版本定义了若干函数，用于比较表示版本的字符串。

> [!Note]
> 条件中的比较运算符[可以比较可分析为 `System.Version` 对象](msbuild-conditions.md#comparing-versions) 的字符串，但比较可能会产生意外结果。 首选属性函数。

|函数签名|描述|
|------------------------|-----------------|
|VersionEquals(string a, string b)|如果版本 `a` 和 `b` 等效，则根据以下规则返回 `true`。|
|VersionGreaterThan(string a, string b)|如果版本 `a` 大于 `b`，则根据以下规则返回 `true`。|
|VersionGreaterThanOrEquals(string a, string b)|如果版本 `a` 大于或等于 `b`，则根据以下规则返回 `true`。|
|VersionLessThan(string a, string b)|如果版本 `a` 小于 `b`，则根据以下规则返回 `true`。|
|VersionLessThanOrEquals(string a, string b)|如果版本 `a` 小于或等于 `b`，则根据以下规则返回 `true`。|
|VersionNotEquals(string a, string b)|如果版本 `a` 和 `b` 等效，则根据以下规则返回 `false`。|

在这些方法中，版本的分析类似于 <xref:System.Version?displayProperty=fullName>，但以下情况例外：

* 忽略前导 `v` 或 `V`，以便可以与 `$(TargetFrameworkVersion)` 进行比较。

* 从第一个“-”或“+”到版本字符串末尾的所有内容都将被忽略。 虽然顺序与 SemVer 不同，但允许传递语义版本 (SemVer)。 相反，预发布说明符和生成元数据没有任何排序权重。 例如，若要打开 `>= x.y` 的功能并使其在 `x.y.z-pre` 上启动，这很有用。

* 未指定部分与零值部分相同。 (`x == x.0 == x.0.0 == x.0.0.0`).

* 整数组件中不允许含有空格。

* 仅主版本有效（`3` 等于 `3.0.0.0`）

* `+` 不允许作为整数组件中的正号（它被视为 SemVer 元数据并被忽略）

> [!TIP]
> 要比较 [TargetFramework 属性](msbuild-target-framework-and-target-platform.md)，通常应使用 [IsTargetFrameworkCompatible](#TargetFramework)，而不是提取和比较版本。 这允许比较在 `TargetFrameworkIdentifier` 和版本中不同的 `TargetFramework`。

## <a name="msbuild-condition-functions"></a>MSBuild 条件函数

函数 `Exists` 和 `HasTrailingSlash` 不是属性函数。 它们可与 `Condition` 属性一起使用。 请参阅 [MSBuild 条件](msbuild-conditions.md)。

## <a name="see-also"></a>请参阅

- [MSBuild 属性](../msbuild/msbuild-properties.md)

- [MSBuild 概述](../msbuild/msbuild.md)
