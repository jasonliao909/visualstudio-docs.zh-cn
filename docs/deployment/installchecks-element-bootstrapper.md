---
title: '&lt;InstallChecks&gt; 元素（引导程序）| Microsoft Docs'
description: InstallChecks 元素支持在本地计算机上启动各种测试，以确保应用程序的所有必备组件已安装。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664132"
---
# <a name="ltinstallchecksgt-element-bootstrapper"></a>&lt;InstallChecks&gt; 元素（引导程序）
`InstallChecks` 元素支持在本地计算机上启动各种测试，以确保应用程序的所有相应必备组件已安装。

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
 此元素是 `InstallChecks` 元素的可选子元素。 对于 `AssemblyCheck` 的每个实例，引导程序将确保由元素标识的程序集存在于全局程序集缓存 (GAC) 中。 它不包含任何元素，但具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Property`|必需。 要存储结果的属性的名称。 可以从 `InstallConditions` 元素下的测试中引用此属性，该元素是 `Command` 元素的子元素。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|
|`Name`|必需。 要检查的程序集的完全限定名。|
|`PublicKeyToken`|必需。 与此强名称程序集关联的公钥的缩写形式。 存储在 GAC 中的所有程序集都必须具有名称、版本和公钥。|
|`Version`|必需。 该程序集的版本。<br /><br /> 版本号的格式为 \<*major version*>.\<*minor version*>.\<*build version*>.\<*revision version*>。|
|`Language`|可选。 本地化程序集的语言。 默认值为 `neutral`。|
|`ProcessorArchitecture`|可选。 此次安装所针对的计算机处理器。 默认值为 `msil`。|

## <a name="externalcheck"></a>ExternalCheck
 此元素是 `InstallChecks` 元素的可选子元素。 对于 `ExternalCheck` 的每个实例，引导程序将在单独的进程中执行命名的外部程序，并在 `Property` 指示的属性中存储其退出代码。 `ExternalCheck` 对于实现复杂的依赖项检查很有用，当检查组件是否存在的唯一方法是对其进行实例化时也很有用。

 `ExternalCheck` 不包含任何元素，但具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Property`|必需。 要存储结果的属性的名称。 可以从 `InstallConditions` 元素下的测试中引用此属性，该元素是 `Command` 元素的子元素。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|
|`PackageFile`|必需。 要执行的外部程序。 此程序必须是安装分发包的一部分。|
|`Arguments`|可选。 向 `PackageFile` 命名的可执行文件提供命令行参数。|

## <a name="filecheck"></a>FileCheck
 此元素是 `InstallChecks` 元素的可选子元素。 对于 `FileCheck` 的每个实例，引导程序将确定命名的文件是否存在，并返回该文件的版本号。 如果文件没有版本号，则引导程序会将 `Property` 命名的属性设置为 0。 如果该文件不存在，则 `Property` 不会设置为任何值。

 `FileCheck` 不包含任何元素，但具有以下属性。

| 属性 | 说明 |
|-----------------| - |
| `Property` | 必需。 要存储结果的属性的名称。 可以从 `InstallConditions` 元素下的测试中引用此属性，该元素是 `Command` 元素的子元素。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。 |
| `FileName` | 必需。 要查找的文件的名称。 |
| `SearchPath` | 必需。 要在其中查找文件的磁盘或文件夹。 如果分配了 `SpecialFolder`，则此路径必须是相对路径；否则，它必须是绝对路径。 |
| `SpecialFolder` | 可选。 对 Windows 或 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 具有特殊意义的文件夹。 默认值是将 `SearchPath` 解释为绝对路径。 有效值包括以下值：<br /><br /> `AppDataFolder`. 此 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的应用程序数据文件夹；特定于当前用户。<br /><br /> `CommonAppDataFolder`. 所有用户使用的应用程序数据文件夹。<br /><br /> `CommonFilesFolder`. 当前用户的 Common Files 文件夹。<br /><br /> `LocalDataAppFolder`. 非漫游应用程序的数据文件夹。<br /><br /> `ProgramFilesFolder`. 32 位应用程序的标准 Program Files 文件夹。<br /><br /> `StartUpFolder`. 包含系统启动时启动的所有应用程序的文件夹。<br /><br /> `SystemFolder`. 包含 32 位系统 DLL 的文件夹。<br /><br /> `WindowsFolder`. 包含 Windows 系统安装的文件夹。<br /><br /> `WindowsVolume`. 包含 Windows 系统安装的驱动器或分区。 |
| `SearchDepth` | 可选。 搜索命名文件的子文件夹的深度。 搜索采用深度优先搜索方式。 默认值为 0，这将搜索限制为由 `SpecialFolder` 和 SearchPath 指定的顶级文件夹。 |

## <a name="msiproductcheck"></a>MsiProductCheck
 此元素是 `InstallChecks` 元素的可选子元素。 对于 `MsiProductCheck` 的每个实例，引导程序将进行检查，以确定指定的 Microsoft Windows Installer 安装是否一直运行直至完毕。 根据安装的产品的状态设置属性值。 正值表示已安装该产品，0 或 -1 表示未安装该产品。 （有关详细信息，请参阅 Windows Installer SDK 函数 MsiQueryFeatureState。）。 如果未在计算机上安装 Windows Installer，则不设置 `Property`。

 `MsiProductCheck` 不包含任何元素，但具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Property`|必需。 要存储结果的属性的名称。 可以从 `InstallConditions` 元素下的测试中引用此属性，该元素是 `Command` 元素的子元素。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|
|`Product`|必需。 已安装产品的 GUID。|
|`Feature`|可选。 已安装应用程序的特定功能的 GUID。|

## <a name="registrycheck"></a>RegistryCheck
 此元素是 `InstallChecks` 元素的可选子元素。 对于 `RegistryCheck` 的每个实例，引导程序将进行检查以确定指定的注册表项是否存在，或其是否具有指示的值。

 `RegistryCheck` 不包含任何元素，但具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Property`|必需。 要存储结果的属性的名称。 可以从 `InstallConditions` 元素下的测试中引用此属性，该元素是 `Command` 元素的子元素。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|
|`Key`|必需。 注册表项的名称。|
|`Value`|可选。 要检索的注册表值的名称。 默认返回默认值的文本。 `Value` 必须是字符串或 DWORD。|

## <a name="registryfilecheck"></a>RegistryFileCheck
 此元素是 `InstallChecks` 元素的可选子元素。 对于 `RegistryFileCheck` 的每个实例，引导程序检索指定文件的版本，首先尝试从指定的注册表项中检索文件路径。 如果要在注册表中指定为值的目录中查找文件，这特别有用。

 `RegistryFileCheck` 不包含任何元素，但具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Property`|必需。 要存储结果的属性的名称。 可以从 `InstallConditions` 元素下的测试中引用此属性，该元素是 `Command` 元素的子元素。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|
|`Key`|必需。 注册表项的名称。 除非设置了 `File` 属性，否则其值将解释为文件路径。 如果此项不存在，则不设置 `Property`。|
|`Value`|可选。 要检索的注册表值的名称。 默认返回默认值的文本。 `Value` 值必须是字符串。|
|`FileName`|可选。 文件的名称。 如果指定，则假定从注册表项获取的值是目录路径，并且此文件名将追加到该路径中。 如果未指定，则假定从注册表返回的值是文件的完整路径。|
|`SearchDepth`|可选。 搜索命名文件的子文件夹的深度。 搜索采用深度优先搜索方式。 默认值为 0，这将搜索限制为由注册表项的值指定的顶级文件夹。|

## <a name="remarks"></a>备注
 虽然 `InstallChecks` 下的元素定义了要运行的测试，但不会执行这些测试。 若要执行测试，必须在 `Commands` 元素下创建 `Command` 元素。

## <a name="example"></a>示例
 下面的代码示例演示了 `InstallChecks` 元素，它在产品文件中用于 .NET Framework。

```xml
<InstallChecks>
    <ExternalCheck Property="DotNetInstalled" PackageFile="dotnetchk.exe" />
    <RegistryCheck Property="IEVersion" Key="HKLM\Software\Microsoft\Internet Explorer" Value="Version" />
</InstallChecks>
```

## <a name="installconditions"></a>InstallConditions
 计算 `InstallChecks` 时，它们会生成属性。 然后，`InstallConditions` 使用这些属性来确定包是应安装、绕过还是失败。 下表列出 `InstallConditions`：

|条件|说明|
|-|-|
|`FailIf`|如果 `FailIf` 条件的计算结果为 true，包将失败。 并且将不计算其余条件。|
|`BypassIf`|如果 `BypassIf` 条件的计算结果为 true，包将绕过。 并且将不计算其余条件。|

## <a name="predefined-properties"></a>预定义属性
 下表列出了 `BypassIf` 和 `FailIf` 元素：

|属性|注释|可能的值|
|--------------|-----------|---------------------|
|`Version9X`|Windows 9X 操作系统的版本号。|4.10 = Windows 98|
|`VersionNT`|基于 Windows NT 的操作系统的版本号。|Major.Minor.ServicePack<br /><br /> 5.0 = Windows 2000<br /><br /> 5.1.0 = Windows XP<br /><br /> 5.1.2 = Windows XP Professional SP2<br /><br /> 5.2.0 = Windows Server 2003|
|`VersionNT64`|基于 Windows NT 的 64 位操作系统的版本号。|与前面所述相同。|
|`VersionMsi`|Windows Installer 服务的版本号。|2.0 = Windows Installer 2.0|
|`AdminUser`|指定用户是否具有基于 Windows NT 的操作系统的管理员特权。|0 = 不具有管理员特权<br /><br /> 1 = 管理员特权|

 例如，若要阻止在运行 Windows 95 的计算机上安装，请使用如下所示的代码：

```xml
    <!-- Block install on Windows 95 -->
    <FailIf Property="Version9X" Compare="VersionLessThan" Value="4.10" String="InvalidPlatform"/>
```

 若要跳过运行安装检查，如果满足 FailIf 或 BypassIf 条件，则使用 BeforeInstallChecks 属性。  例如：

```xml
    <!-- Block install and do not evaluate install checks if user does not have admin privileges -->
    <FailIf Property="AdminUser" Compare="ValueEqualTo" Value="false" String="AdminRequired" BeforeInstallChecks="true"/>
```

>[!NOTE]
>从 Visual Studio 2019 Update 9 版本开始支持 `BeforeInstallChecks` 属性。

## <a name="see-also"></a>另请参阅
- [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)
- [产品和包架构引用](../deployment/product-and-package-schema-reference.md)