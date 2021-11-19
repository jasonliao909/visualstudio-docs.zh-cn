---
title: '&lt;Commands&gt; 元素（引导程序）| Microsoft Docs'
description: Commands 元素在 InstallChecks 下的元素中实现测试，并在 ClickOnce 引导程序测试失败的情况下声明要安装的包。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <Commands> element [bootstrapper]
ms.assetid: e61d5787-fe1f-4ebf-b0cf-0d7909be7ffb
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: a343ae58306b85a7bd6dcb0332f1b69cbe5d04a7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665651"
---
# <a name="ltcommandsgt-element-bootstrapper"></a>&lt;Commands&gt; 元素（引导程序）
`Commands` 元素实现由 `InstallChecks` 元素下的元素描述的测试，并在测试失败的情况下声明 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 引导程序应安装的包。

## <a name="syntax"></a>语法

```xml
<Commands
    Reboot
>
    <Command
        PackageFile
        Arguments
        EstimatedInstallSeconds
        EstimatedDiskBytes
        EstimatedTempBytes
        Log
    >
        <InstallConditions>
            <BypassIf
                Property
                Compare
                Value
                Schedule
            />
            <FailIf
                Property
                Compare
                Value
                String
                Schedule
            />
        </InstallConditions>
        <ExitCodes>
            <ExitCode
                Value
                Result
                String
            />
        </ExitCodes>
    </Command>
</Commands>
```

## <a name="elements-and-attributes"></a>元素和属性
 `Commands` 元素是必需的。 元素具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Reboot`|可选。 确定在任何包返回重启退出代码时是否应重启系统。 以下列表显示了有效值：<br /><br /> `Defer`. 重启将推迟到将来的某个时间。<br /><br /> `Immediate`. 如果任何一个包返回了重启退出代码，则会立即重启。<br /><br /> `None`. 忽略任何重启请求。<br /><br /> 默认为 `Immediate`。|

## <a name="command"></a>命令
 `Command` 元素是 `Commands` 元素的一个子元素。 一个 `Commands` 元素可以包含一个或多个 `Command` 元素。 元素具有以下属性。

|属性|说明|
|---------------|-----------------|
|`PackageFile`|必需。 要安装的包的名称，应为由返回 false 的 `InstallConditions` 指定的一个或多个条件。 必须使用 `PackageFile` 元素在同一文件中定义包。|
|`Arguments`|可选。 要传递到包文件中的一组命令行参数。|
|`EstimatedInstallSeconds`|可选。 安装包所需的估计时间（以秒为单位）。 此值确定引导程序向用户显示的进度栏的大小。 默认值为 0，在这种情况下，未指定估计时间。|
|`EstimatedDiskBytes`|可选。 安装完成后包所占的估计磁盘空间量（以字节为单位）。 此值用于引导程序向用户显示硬盘空间要求。 默认值为 0，在这种情况下，引导程序不会显示任何硬盘空间要求。|
|`EstimatedTempBytes`|可选。 包所需的估计临时磁盘空间量（以字节为单位）。|
|`Log`|可选。 包生成的日志文件的路径（相对于包的根目录而言）。|

## <a name="installconditions"></a>InstallConditions
 `InstallConditions` 元素是 `Command` 元素的一个子元素。 每个 `Command` 元素最多只能有一个 `InstallConditions` 元素。 如果 `InstallConditions` 元素不存在，那么将始终运行由 `Condition` 指定的包。

## <a name="bypassif"></a>BypassIf
 `BypassIf` 元素是 `InstallConditions` 元素的子元素，描述不应执行命令的肯定条件。 每个 `InstallConditions` 元素可以包含零个或多个 `BypassIf` 元素。

 `BypassIf` 具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Property`|必需。 要测试的属性的名称。 此属性必须已在之前由 `InstallChecks` 元素的子元素所定义。 有关详细信息，请参阅 [\<InstallChecks> 元素](../deployment/installchecks-element-bootstrapper.md)。|
|`Compare`|必需。 要执行的比较的类型。 以下列表显示了有效值：<br /><br /> `ValueEqualTo`, `ValueNotEqualTo`, `ValueGreaterThan`, `ValueGreaterThanOrEqualTo`, `ValueLessThan`, `ValueLessThanOrEqualTo`, `VersionEqualTo`, `VersionNotEqualTo`, `VersionGreaterThan`, `VersionGreaterThanOrEqualTo`, `VersionLessThan`, `VersionLessThanOrEqualTo`, `ValueExists`, `ValueNotExists`|
|`Value`|必需。 要与属性进行比较的值。|
|`Schedule`|可选。 定义何时应计算此规则的 `Schedule` 标记的名称。|

## <a name="failif"></a>FailIf
 `FailIf` 元素是 `InstallConditions` 元素的子元素，描述应停止执行安装的肯定条件。 每个 `InstallConditions` 元素可以包含零个或多个 `FailIf` 元素。

 `FailIf` 具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Property`|必需。 要测试的属性的名称。 此属性必须已在之前由 `InstallChecks` 元素的子元素所定义。 有关详细信息，请参阅 [\<InstallChecks> 元素](../deployment/installchecks-element-bootstrapper.md)。|
|`Compare`|必需。 要执行的比较的类型。 以下列表显示了有效值：<br /><br /> `ValueEqualTo`, `ValueNotEqualTo`, `ValueGreaterThan`, `ValueGreaterThanOrEqualTo`, `ValueLessThan`, `ValueLessThanOrEqualTo`, `VersionEqualTo`, `VersionNotEqualTo`, `VersionGreaterThan`, `VersionGreaterThanOrEqualTo`, `VersionLessThan`, `VersionLessThanOrEqualTo`, `ValueExists`, `ValueNotExists`|
|`Value`|必需。 要与属性进行比较的值。|
|`String`|可选。 失败时要显示给用户的文本。|
|`Schedule`|可选。 定义何时应计算此规则的 `Schedule` 标记的名称。|

## <a name="exitcodes"></a>ExitCodes
 `ExitCodes` 元素是 `Command` 元素的一个子元素。 `ExitCodes` 元素包含一个或多个 `ExitCode` 元素，此元素确定安装应执行的操作以响应包中的退出代码。 `Command` 元素下可以有一个可选的 `ExitCode` 元素。 `ExitCodes` 没有属性。

## <a name="exitcode"></a>ExitCode
 `ExitCode` 元素是 `ExitCodes` 元素的一个子元素。 `ExitCode` 元素确定安装应执行的操作以响应包中的退出代码。 `ExitCode` 不包含任何子元素，但具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Value`|必需。 此 `ExitCode` 元素应用到的退出代码值。|
|`Result`|必需。 安装应如何对此退出代码做出反应。 以下列表显示了有效值：<br /><br /> `Success`. 将包标记为已成功安装。<br /><br /> `SuccessReboot`. 将包标记为已成功安装，并指示系统重启。<br /><br /> `Fail`. 将包标记为失败。<br /><br /> `FailReboot`. 将包标记为失败，并指示系统重启。|
|`String`|可选。 应对此退出代码要向用户显示的值。|
|`FormatMessageFromSystem`|可选。 确定是使用与退出代码相对应的系统提供的错误消息，还是使用 `String` 中提供的值。 有效值包括 `true`：表示使用系统提供的错误；`false`：表示使用 `String` 提供的字符串。 默认为 `false`。 如果此属性为 `false`，但未设置 `String`，则会使用系统提供的错误。|

## <a name="example"></a>示例
 下面的代码示例定义了用于安装 .NET Framework 2.0 的命令。

```xml
<Commands Reboot="Immediate">
    <Command PackageFile="instmsia.exe"
             Arguments= ' /q /c:"msiinst /delayrebootq"'
             EstimatedInstallSeconds="20" >
        <InstallConditions>
           <BypassIf Property="VersionNT" Compare="ValueExists"/>
             BypassIf Property="VersionMsi" Compare="VersionGreaterThanOrEqualTo" Value="2.0"/>
        </InstallConditions>
        <ExitCodes>
            <ExitCode Value="0" Result="SuccessReboot"/>
            <ExitCode Value="1641" Result="SuccessReboot"/>
            <ExitCode Value="3010" Result="SuccessReboot"/>
            <DefaultExitCode Result="Fail" FormatMessageFromSystem="true" String="GeneralFailure" />
        </ExitCodes>
    </Command>
    <Command PackageFile="WindowsInstaller-KB884016-v2-x86.exe"
             Arguments= '/quiet /norestart'
             EstimatedInstallSeconds="20" >
      <InstallConditions>
          <BypassIf Property="Version9x" Compare="ValueExists"/>
          <BypassIf Property="VersionNT" Compare="VersionLessThan" Value="5.0.3"/>
          <BypassIf Property="VersionMsi" Compare="VersionGreaterThanOrEqualTo" Value="3.0"/>
          <FailIf Property="AdminUser" Compare="ValueEqualTo" Value="false" String="AdminRequired"/>
      </InstallConditions>
      <ExitCodes>
          <ExitCode Value="0" Result="Success"/>
          <ExitCode Value="1641" Result="SuccessReboot"/>
          <ExitCode Value="3010" Result="SuccessReboot"/>
          <DefaultExitCode Result="Fail" FormatMessageFromSystem="true" String="GeneralFailure" />
      </ExitCodes>
    </Command>
    <Command PackageFile="dotnetfx.exe"
         Arguments=' /q:a /c:"install /q /l"'
         EstimatedInstalledBytes="21000000"
         EstimatedInstallSeconds="300">

        <!-- These checks determine whether the package is to be installed -->
        <InstallConditions>
            <!-- Either of these properties indicates the .NET Framework is already installed -->
            <BypassIf Property="DotNetInstalled" Compare="ValueNotEqualTo" Value="0"/>

            <!-- Block install if user does not have adminpermissions -->
            <FailIf Property="AdminUser" Compare="ValueEqualTo" Value="false" String="AdminRequired"/>

            <!-- Block install on Windows 95 -->
            <FailIf Property="Version9X" Compare="VersionLessThan" Value="4.10" String="InvalidPlatformWin9x"/>

            <!-- Block install on Windows 2000 SP 2 or less -->
            <FailIf Property="VersionNT" Compare="VersionLessThan" Value="5.0.3" String="InvalidPlatformWinNT"/>

            <!-- Block install if Internet Explorer 5.01 or later is not present -->
            <FailIf Property="IEVersion" Compare="ValueNotExists" String="InvalidPlatformIE" />
            <FailIf Property="IEVersion" Compare="VersionLessThan" Value="5.01" String="InvalidPlatformIE" />

            <!-- Block install if the operating system does not support x86 -->
            <FailIf Property="ProcessorArchitecture" Compare="ValueNotEqualTo" Value="Intel" String="InvalidPlatformArchitecture" />
       </InstallConditions>

        <ExitCodes>
            <ExitCode Value="0" Result="Success"/>
            <ExitCode Value="3010" Result="SuccessReboot"/>
            <ExitCode Value="4097" Result="Fail" String="AdminRequired"/>
            <ExitCode Value="4098" Result="Fail" String="WindowsInstallerComponentFailure"/>
            <ExitCode Value="4099" Result="Fail" String="WindowsInstallerImproperInstall"/>
            <ExitCode Value="4101" Result="Fail" String="AnotherInstanceRunning"/>
            <ExitCode Value="4102" Result="Fail" String="OpenDatabaseFailure"/>
            <ExitCode Value="4113" Result="Fail" String="BetaNDPFailure"/>
            <DefaultExitCode Result="Fail" FormatMessageFromSystem="true" String="GeneralFailure" />
        </ExitCodes>

    </Command>
</Commands>
```

## <a name="see-also"></a>另请参阅
- [产品和包架构引用](../deployment/product-and-package-schema-reference.md)
- [\<InstallChecks> 元素](../deployment/installchecks-element-bootstrapper.md)