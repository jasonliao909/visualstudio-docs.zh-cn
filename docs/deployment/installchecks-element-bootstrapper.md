---
title: '&lt;&gt; (引导程序) 的 InstallChecks 元素 |Microsoft Docs'
description: InstallChecks 元素支持在本地计算机上启动各种测试，以确保已安装应用程序的所有先决条件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <InstallChecks> element [bootstrapper]
ms.assetid: ad329c87-b0ad-4304-84de-ae9496514c42
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 0f2487489d75ca4ce7275153fd754b6fac7ebf5e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122051568"
---
# <a name="ltinstallchecksgt-element-bootstrapper"></a>&lt;InstallChecks &gt; 元素 (引导程序) 
`InstallChecks`元素支持对本地计算机启动各种测试，以确保已安装应用程序的所有适当的先决条件。

## <a name="syntax"></a>语法

```xml
<InstallChecks>
    <AssemblyCheck
        Property
        Name
        PublicKeyToken
        Version
        Language
        ProcessorArchitecture
    />
    <RegistryCheck
        Property
        Key
        Value
    />
    <ExternalCheck
        PackageFile
        Property
        Arguments
    />
    <FileCheck
        Property
        FileName
        SearchPath
        SpecialFolder
        SearchDepth
    />
    <MsiProductCheck
        Property
        Product
        Feature
    />
    <RegistryFileCheck
        Property
        Key
        Value
        FileName
        SearchDepth
    />
</InstallChecks>
```

## <a name="assemblycheck"></a>AssemblyCheck
 此元素是的可选子元素 `InstallChecks` 。 对于每个实例 `AssemblyCheck` ，引导程序将确保由元素标识的程序集存在于全局程序集缓存中 (GAC) 。 它不包含任何元素，并且具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`Property`|必需。 要存储结果的属性的名称。 可以从元素下的测试中引用此属性 `InstallConditions` ，该元素是元素的子元素 `Command` 。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|
|`Name`|必需。 要检查的程序集的完全限定名称。|
|`PublicKeyToken`|必需。 与此强名称程序集关联的公钥的缩写形式。 GAC 中存储的所有程序集都必须具有名称、版本和公钥。|
|`Version`|必需。 该程序集的版本。<br /><br /> 版本号的格式为 \<*major version*> ... \<*minor version*> \<*build version*> \<*revision version*> 。|
|`Language`|可选。 本地化程序集的语言。 默认值为 `neutral`。|
|`ProcessorArchitecture`|可选。 此安装所针对的计算机处理器。 默认值为 `msil`。|

## <a name="externalcheck"></a>ExternalCheck
 此元素是的可选子元素 `InstallChecks` 。 对于每个实例 `ExternalCheck` ，引导程序将在单独的进程中执行命名的外部程序，并在指示的属性中存储其退出代码 `Property` 。 `ExternalCheck` 对于实现复杂的依赖项检查非常有用，或者当检查组件是否存在的唯一方法是对其进行实例化时。

 `ExternalCheck` 不包含任何元素，并且具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`Property`|必需。 要存储结果的属性的名称。 可以从元素下的测试中引用此属性 `InstallConditions` ，该元素是元素的子元素 `Command` 。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|
|`PackageFile`|必需。 要执行的外部程序。 此程序必须是安装分发包的一部分。|
|`Arguments`|可选。 向名为的可执行文件提供命令行参数 `PackageFile` 。|

## <a name="filecheck"></a>FileCheck
 此元素是的可选子元素 `InstallChecks` 。 对于每个实例 `FileCheck` ，引导程序将确定指定的文件是否存在，并返回该文件的版本号。 如果文件没有版本号，则引导程序会将名为的属性设置 `Property` 为0。 如果该文件不存在， `Property` 则不会将设置为任何值。

 `FileCheck` 不包含任何元素，并且具有以下属性。

| Attribute | 说明 |
|-----------------| - |
| `Property` | 必需。 要存储结果的属性的名称。 可以从元素下的测试中引用此属性 `InstallConditions` ，该元素是元素的子元素 `Command` 。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。 |
| `FileName` | 必需。 要查找的文件的名称。 |
| `SearchPath` | 必需。 要在其中查找文件的磁盘或文件夹。 如果分配了，则此路径必须是相对路径 `SpecialFolder` ; 否则，它必须是绝对路径。 |
| `SpecialFolder` | 可选。 具有对 Windows 或的特殊意义的文件夹 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 默认值是解释 `SearchPath` 为绝对路径。 有效值包括以下值：<br /><br /> `AppDataFolder`. 此应用程序的应用程序数据文件夹 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ; 特定于当前用户。<br /><br /> `CommonAppDataFolder`. 所有用户使用的应用程序数据文件夹。<br /><br /> `CommonFilesFolder`. 当前用户的 "公共文件" 文件夹。<br /><br /> `LocalDataAppFolder`. 非漫游应用程序的数据文件夹。<br /><br /> `ProgramFilesFolder`. 32位应用程序的标准 Program Files 文件夹。<br /><br /> `StartUpFolder`. 包含系统启动时启动的所有应用程序的文件夹。<br /><br /> `SystemFolder`. 包含32位系统 Dll 的文件夹。<br /><br /> `WindowsFolder`. 包含 Windows 系统安装的文件夹。<br /><br /> `WindowsVolume`. 包含 Windows 系统安装的驱动器或分区。 |
| `SearchDepth` | 可选。 在其中搜索指定文件的子文件夹的深度。 搜索深度优先。 默认值为0，该值将搜索限制为由和 SearchPath 指定的顶层文件夹 `SpecialFolder` 。  |

## <a name="msiproductcheck"></a>MsiProductCheck
 此元素是的可选子元素 `InstallChecks` 。 对于每个实例 `MsiProductCheck` ，引导程序将进行检查，以确定指定的 Microsoft Windows Installer 安装是否已运行完毕。 根据安装的产品的状态设置属性值。 正值表示已安装产品，0或-1 表示未安装该产品。  (有关详细信息，请参阅 Windows Installer SDK 函数 MsiQueryFeatureState。 ) 。 如果未在计算机上安装 Windows Installer， `Property` 则不设置。

 `MsiProductCheck` 不包含任何元素，并且具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`Property`|必需。 要存储结果的属性的名称。 可以从元素下的测试中引用此属性 `InstallConditions` ，该元素是元素的子元素 `Command` 。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|
|`Product`|必需。 已安装产品的 GUID。|
|`Feature`|可选。 已安装应用程序的特定功能的 GUID。|

## <a name="registrycheck"></a>RegistryCheck
 此元素是的可选子元素 `InstallChecks` 。 对于每个实例 `RegistryCheck` ，引导程序将进行检查以确定指定的注册表项是否存在，或其是否具有指示的值。

 `RegistryCheck` 不包含任何元素，并且具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`Property`|必需。 要存储结果的属性的名称。 可以从 元素（元素的子元素）下面的测试 `InstallConditions` 引用 `Command` 此属性。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|
|`Key`|必需。 注册表项的名称。|
|`Value`|可选。 要检索的注册表值的名称。 默认值是返回默认值的文本。 `Value` 必须是字符串或 DWORD。|

## <a name="registryfilecheck"></a>RegistryFileCheck
 此元素是 的可选子元素 `InstallChecks` 。 对于每个 实例，引导程序将检索指定文件的版本，首先尝试从指定的注册表项中检索 `RegistryFileCheck` 文件的路径。 如果要在注册表中指定为值的目录中查找文件，这特别有用。

 `RegistryFileCheck` 不包含任何元素，并且具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`Property`|必需。 要存储结果的属性的名称。 可以从 元素（元素的子元素）下面的测试 `InstallConditions` 引用 `Command` 此属性。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|
|`Key`|必需。 注册表项的名称。 除非设置了 属性，否则其值将解释为 `File` 文件的路径。 如果此键不存在， `Property` 则不设置 。|
|`Value`|可选。 要检索的注册表值的名称。 默认值是返回默认值的文本。 `Value` 必须是字符串。|
|`FileName`|可选。 文件的名称。 如果指定，则假定从注册表项获取的值是目录路径，并且此名称将追加到该路径中。 如果未指定，则假定从注册表返回的值是文件的完整路径。|
|`SearchDepth`|可选。 在子文件夹中搜索命名文件的深度。 搜索是深度第一。 默认值为 0，将搜索限制为由注册表项的值指定的顶级文件夹。|

## <a name="remarks"></a>备注
 虽然下面的元素 `InstallChecks` 定义要运行的测试，但不会执行它们。 若要执行测试，必须在 `Command` 元素下创建 `Commands` 元素。

## <a name="example"></a>示例
 下面的代码示例演示 了 `InstallChecks` 元素，因为它在 .NET Framework 的产品文件中使用。

```xml
<InstallChecks>
    <ExternalCheck Property="DotNetInstalled" PackageFile="dotnetchk.exe" />
    <RegistryCheck Property="IEVersion" Key="HKLM\Software\Microsoft\Internet Explorer" Value="Version" />
</InstallChecks>
```

## <a name="installconditions"></a>InstallConditions
 计算 `InstallChecks` 时，它们生成属性。 然后，使用 属性来确定包是应安装、 `InstallConditions` 绕过还是失败。 下表列出了 `InstallConditions` ：

|条件|说明|
|-|-|
|`FailIf`|如果任何 `FailIf` 条件计算结果为 true，则包将失败。 不会计算其余条件。|
|`BypassIf`|如果 `BypassIf` 任何条件计算结果为 true，将绕过包。 不会计算其余条件。|

## <a name="predefined-properties"></a>预定义属性
 下表列出了 和 `BypassIf` `FailIf` 元素：

|属性|注释|可能的值|
|--------------|-----------|---------------------|
|`Version9X`|9X 操作系统Windows版本号。|4.10 = Windows 98|
|`VersionNT`|基于 Windows NT操作系统的版本号。|Major.Minor.ServicePack<br /><br /> 5.0 = Windows 2000<br /><br /> 5.1.0 = Windows XP<br /><br /> 5.1.2 = Windows XP Professional SP2<br /><br /> 5.2.0 = Windows Server 2003|
|`VersionNT64`|基于操作系统的 64 位Windows NT版本号。|与前面所述相同。|
|`VersionMsi`|安装程序服务的Windows版本号。|2.0 = Windows安装程序 2.0|
|`AdminUser`|指定用户是否具有基于 Windows NT操作系统的管理员权限。|0 = 无管理员特权<br /><br /> 1 = 管理员特权|

 例如，若要阻止在运行 Windows 95 的计算机上安装，请使用如下所示的代码：

```xml
    <!-- Block install on Windows 95 -->
    <FailIf Property="Version9X" Compare="VersionLessThan" Value="4.10" String="InvalidPlatform"/>
```

 若要跳过运行安装检查，如果满足 FailIf 或 BypassIf 条件，请使用 BeforeInstallChecks 属性。  例如：

```xml
    <!-- Block install and do not evaluate install checks if user does not have admin privileges -->
    <FailIf Property="AdminUser" Compare="ValueEqualTo" Value="false" String="AdminRequired" BeforeInstallChecks="true"/>
```

>[!NOTE]
>从 `BeforeInstallChecks` 2019 Update 9 Visual Studio开始支持 属性。

## <a name="see-also"></a>请参阅
- [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)
- [产品和包架构参考](../deployment/product-and-package-schema-reference.md)