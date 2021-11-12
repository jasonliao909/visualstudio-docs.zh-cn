---
title: '&lt;dependency&gt; 元素（ClickOnce 部署）| Microsoft Docs'
description: dependency 元素标识要安装的应用程序版本和应用程序清单的位置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#osVersionInfo
- urn:schemas-microsoft-com:asm.v2#os
- http://www.w3.org/2000/09/xmldsig#Transform
- urn:schemas-microsoft-com:asm.v2#dependency
- http://www.w3.org/2000/09/xmldsig#DigestValue
- urn:schemas-microsoft-com:asm.v2#assemblyIdentity
- http://www.w3.org/2000/09/xmldsig#DigestMethod
- http://www.w3.org/2000/09/xmldsig#Transforms
- urn:schemas-microsoft-com:asm.v2#hash
- urn:schemas-microsoft-com:asm.v2#dependentAssembly
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <dependency> element [ClickOnce deployment manifest]
ms.assetid: 9b4d2082-0347-4922-ac70-85f11b913039
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 27da36d933a3505163c36623b9eac8b51d0bbe86
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665649"
---
# <a name="ltdependencygt-element-clickonce-deployment"></a>&lt;dependency&gt; 元素（ClickOnce部署）
标识要安装的应用程序版本和应用程序清单的位置。

## <a name="syntax"></a>语法

```xml

      <dependency>
   <dependentAssembly
      preRequisite
      visible
      dependencyType
      codeBase
      size
   >
      <assemblyIdentity
         name
         version
         publicKeyToken
         processorArchitecture
         language
         type
      />
      <hash>
         <dsig:Transforms>
            <dsig:Transform
                Algorithm
            />
         </dsig:Transforms>
         <dsig:DigestMethod />
         <dsig:DigestValue>
         </dsig:DigestValue>
      </hash>

   </dependentAssembly>
</dependency>
```

## <a name="elements-and-attributes"></a>元素和属性
 `dependency` 元素是必需的。 没有属性。 一个部署清单可以有多个 `dependency` 元素。

 `dependency` 元素通常表示 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序中包含的程序集上主应用程序的依赖项。 如果 Main.exe 应用程序使用名为 DotNetAssembly.dll 的程序集，则必须在依赖项部分中列出该程序集。 不过，依赖项还可表示其他类型的依赖项，例如公共语言运行时的特定版本、全局程序集缓存中的程序集 (GAC) 或 COM 对象上的依赖项。 它是一种无接触部署技术，因此 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 无法发起这些类型的依赖项的下载和安装，但如果一个或多个指定的依赖项不存在，则它会阻止应用程序运行。

## <a name="dependentassembly"></a>dependentAssembly
 必需。 此元素包含 `assemblyIdentity` 元素。 下表显示了 `dependentAssembly` 支持的特性。

| 属性 | 说明 |
|------------------| - |
| `preRequisite` | 可选。 指定 GAC 中应该已存在此程序集。 有效值为 `true` 和 `false`。 如果 GAC 中不存在 `true` 和指定的程序集，则该应用程序无法运行。 |
| `visible` | 可选。 标识顶级应用程序标识，包括其依赖项。 供 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 内部使用，用于管理应用程序存储和激活。 |
| `dependencyType` | 必需。 此依赖项与应用程序之间的关系。 有效值是：<br /><br /> -   `install`. 组件表示与当前应用程序不同的安装。<br />-   `preRequisite`. 当前应用程序需要组件。 |
| `codebase` | 可选。 应用程序清单的完整路径。 |
| `size` | 可选。 应用程序清单的大小（以字节为单位）。 |

## <a name="assemblyidentity"></a>assemblyIdentity
 必需。 此元素是 `dependentAssembly` 元素的子元素。 `assemblyIdentity` 的内容必须与 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单中所述的内容相同。 下表显示了 `assemblyIdentity` 元素的特性。

|属性|说明|
|---------------|-----------------|
|`Name`|必需。 标识应用程序的名称。|
|`Version`|必需。 指定应用程序的版本号，格式如下：`major.minor.build.revision`|
|`publicKeyToken`|必需。 指定 16 个字符的十六进制字符串，该字符串表示应用程序或程序集签名时所用公钥的 SHA-1 哈希的最后 8 个字节。 用于签名的公钥必须为 2048 位或更大。|
|`processorArchitecture`|必需。 指定微处理器。 适用于 32 位 Windows 的有效值为 `x86`，适用于 64 位 Windows 的有效值为 `IA64`。|
|`Language`|可选。 标识程序集由两部分组成的语言代码。 例如，EN-US 表示英语(美国)。 默认为 `neutral`。 此元素位于 `asmv2` 命名空间中。|
|`type`|可选。 与 Windows 并行安装技术向后兼容。 唯一允许的值为 `win32`。|

## <a name="hash"></a>hash
 `hash` 元素是 `file` 元素的可选子元素。 `hash` 元素没有属性。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 在应用程序中使用所有文件的算法哈希作为安全检查，确保在部署后没有任何文件发生更改。 如果不包含 `hash` 元素，则不会执行此检查。 因此，建议不要省略 `hash` 元素。

## <a name="dsigtransforms"></a>dsig:Transforms
 `dsig:Transforms` 元素是 `hash` 元素的必需子元素。 `dsig:Transforms` 元素没有属性。

## <a name="dsigtransform"></a>dsig:Transform
 `dsig:Transform` 元素是 `dsig:Transforms` 元素的必需子元素。 下表显示了 `dsig:Transform` 元素的特性。

| 属性 | 说明 |
|-------------| - |
| `Algorithm` | 用于计算此文件的摘要的算法。 目前，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 唯一使用的值是 `urn:schemas-microsoft-com:HashTransforms.Identity`。 |

## <a name="dsigdigestmethod"></a>dsig:DigestMethod
 `dsig:DigestMethod` 元素是 `hash` 元素的必需子元素。 下表显示了 `dsig:DigestMethod` 元素的特性。

| 属性 | 说明 |
|-------------| - |
| `Algorithm` | 用于计算此文件的摘要的算法。 目前，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 唯一使用的值是 `http://www.w3.org/2000/09/xmldsig#sha1`。 |

## <a name="dsigdigestvalue"></a>dsig:DigestValue
 `dsig:DigestValue` 元素是 `hash` 元素的必需子元素。 `dsig:DigestValue` 元素没有属性。 它的文本值是指定文件计算得出的哈希。

## <a name="remarks"></a>备注
 部署清单通常具有单个 `assemblyIdentity` 元素，用于标识应用程序清单的名称和版本。

## <a name="example-1"></a>示例 1
 下面的代码示例演示了 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署清单中的 `dependency` 元素。

```xml
<!-- Identify the assembly dependencies -->
<dependency>
  <dependentAssembly dependencyType="install" allowDelayedBinding="true" codebase="MyApplication.exe" size="16384">
    <assemblyIdentity name="MyApplication" version="0.0.0.0" cultural="neutral" processorArchitecture="msil" />
    <hash>
      <dsig:Transforms>
        <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
      </dsig:Transforms>
      <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
       <dsig:DigestValue>YzXYZJAvj9pgAG3y8jXUjC7AtHg=</dsig:DigestValue>
    </hash>
  </dependentAssembly>
</dependency>
```

## <a name="example-2"></a>示例 2
 下面的代码示例指定对已在 GAC 中安装的程序集的依赖项。

```xml
<dependency>
  <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">
    <assemblyIdentity name="GACAssembly" version="1.0.0.0" language="neutral" processorArchitecture="msil" />
  </dependentAssembly>
</dependency>
```

## <a name="example-3"></a>示例 3
 下面的代码示例指定对特定版本的公共语言运行时的依赖项。

```xml
<dependency>
  <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">
    <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50215.0" />
  </dependentAssembly>
</dependency>
```

## <a name="example-4"></a>示例 4
 下面的代码示例指定操作系统依赖项。

```xml
<dependency>
   <dependentOS supportUrl="http://www.microsoft.com" description="Microsoft Windows Operating System">
      <osVersionInfo>
         <os majorVersion="4" minorVersion="10" />
      </osVersionInfo>
   </dependentOS>
</dependency>
```

## <a name="see-also"></a>另请参阅
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)
- [\<dependency> 元素](../deployment/dependency-element-clickonce-application.md)