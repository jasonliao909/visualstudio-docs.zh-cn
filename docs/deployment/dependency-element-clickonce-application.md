---
title: '&lt;dependency &gt; Element (ClickOnce Application) |Microsoft Docs'
description: 依赖项元素标识应用程序所需的平台或程序集依赖项。
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
- manifests [ClickOnce], dependency element
- <dependency> element [ClickOnce application manifest]
ms.assetid: 09d6a1e0-60f8-4fbd-843b-8e49ee3115a3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 6dc3d0ad29597e801f4f28cc2b80335cab7240b1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122160876"
---
# <a name="ltdependencygt-element-clickonce-application"></a>&lt;应用程序 &gt; (ClickOnce依赖项) 
标识应用程序所需的平台或程序集依赖项。

## <a name="syntax"></a>语法

```xml

      <dependency>
   <dependentOS
      supportURL
      description
   >
      <osVersionInfo>
         <os
            majorVersion
            minorVersion
            buildNumber
            servicePackMajor
            servicePackMinor
            productType
            suiteType
         />
      </osVersionInfo>
   </dependentOS>
   <dependentAssembly
      dependencyType
      allowDelayedBinding
      group
      codeBase
      size
   >
      <assemblyIdentity
         name
         version
         processorArchitecture
         language
      >
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

      </assemblyIdentity>
   </dependentAssembly>
</dependency>
```

## <a name="elements-and-attributes"></a>元素和属性
 `dependency` 元素是必需的。 同一应用程序清单中 `dependency` 可能有多个 实例。

 `dependency`元素没有属性，并且包含以下子元素。

### <a name="dependentos"></a>dependentOS
 可选。 包含 `osVersionInfo` 元素。 和 元素是互斥的：一个或另一个元素必须存在， `dependentOS` `dependentAssembly` `dependency` 但不能同时存在两者。

 `dependentOS` 支持以下属性。

|Attribute|说明|
|---------------|-----------------|
|`supportUrl`|可选。 指定相关平台的支持 URL。 如果找到所需的平台，则向用户显示此 URL。|
|`description`|可选。 以可读的形式描述 元素描述 `dependentOS` 的操作系统。|

### <a name="osversioninfo"></a>osVersionInfo
 必需。 此元素是 `dependentOS` 元素的子元素，并且包含 `os` 元素。 此元素没有属性。

### <a name="os"></a>os
 必需。 此元素是 `osVersionInfo` 元素的子元素。 此元素具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`majorVersion`|必需。 指定 OS 的主要版本号。|
|`minorVersion`|必需。 指定 OS 的次版本号。|
|`buildNumber`|必需。 指定 OS 的生成号。|
|`servicePackMajor`|必需。 指定 OS 的 Service Pack 主编号。|
|`servicePackMinor`|可选。 指定 OS 的 Service Pack 次要编号。|
|`productType`|可选。 标识产品类型值。 有效值为 `server`、`workstation` 和 `domainController`。 例如，对于 Windows 2000 Professional，此属性值为 `workstation` 。|
|`suiteType`|可选。 标识系统上可用的产品套件或系统的配置类型。 有效值为 `backoffice`、`blade`、`datacenter`、`enterprise`、`home`、`professional`、`smallbusiness`、`smallbusinessRestricted` 和 `terminal`。 例如，对于 Windows 2000 Professional，此属性值为 `professional` 。|

### <a name="dependentassembly"></a>dependentAssembly
 可选。 包含 `assemblyIdentity` 元素。 和 元素是互斥的：一个或另一个元素必须存在， `dependentOS` `dependentAssembly` `dependency` 但不能同时存在两者。

 `dependentAssembly` 具有以下属性。

| Attribute | 说明 |
|-----------------------| - |
| `dependencyType` | 必需。 指定依赖项类型。 有效值为 `preprequisite` 和 `install`。 `install`程序集作为应用程序的一部分 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 安装。 程序集 `prerequisite` 必须存在于全局程序集缓存中 (GAC) 才能 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 安装应用程序。 |
| `allowDelayedBinding` | 必需。 指定是否可以以编程方式运行时加载程序集。 |
| `group` | 可选。 如果 `dependencyType` 属性设置为 `install` ，则指定仅按需安装的命名程序集组。 有关详细信息，请参见[演练：在设计器中使用 ClickOnce 部署 API 按需下载程序集](../deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer.md)。<br /><br /> 如果 设置为 `framework` 且 `dependencyType` 属性设置为 `prerequisite` ，则指定程序集作为该程序集的一.NET Framework。 在 .NET Framework 4 和更高版本) 时，不会检查此程序集的全局 (GAC 缓存。 |
| `codeBase` | 当 特性 `dependencyType` 设置为 时是必需的 `install` 。 依赖程序集的路径。 可以是绝对路径，或者是相对于清单基本代码的路径。 此路径必须是有效的 URI，程序集清单才能有效。 |
| `size` | 当 特性 `dependencyType` 设置为 时是必需的 `install` 。 依赖程序集的大小（以字节为单位）。 |

### <a name="assemblyidentity"></a>assemblyIdentity
 必需。 此元素是 `dependentAssembly` 元素的子元素，并且包含下列元素。

|Attribute|说明|
|---------------|-----------------|
|`name`|必需。 标识应用程序的名称。|
|`version`|必需。 采用以下格式指定应用程序的版本号： `major.minor.build.revision`|
|`publicKeyToken`|可选。 指定一个 16 个字符的十六进制字符串，该字符串表示对应用程序或程序集进行签名的公钥哈希值的最后 8 `SHA-1` 个字节。 用于对目录进行签名的公钥必须是 2048 位或更多位。|
|`processorArchitecture`|可选。 指定处理器。 有效值适用于 `x86` 32 位Windows `I64` 64 位Windows。|
|`language`|可选。 标识程序集的两部分语言代码，如 EN-US。|

### <a name="hash"></a>hash
 `hash`元素是 元素的可选 `assemblyIdentity` 子元素。 `hash` 元素没有属性。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用应用程序中所有文件的算法哈希作为安全检查，以确保部署后未更改任何文件。 如果未 `hash` 包含 元素，则不执行此检查。 因此，不建议省略 `hash` 元素。

### <a name="dsigtransforms"></a>dsig:Transforms
 `dsig:Transforms`元素是 元素的必需 `hash` 子元素。 `dsig:Transforms` 元素没有属性。

### <a name="dsigtransform"></a>dsig:Transform
 `dsig:Transform`元素是 元素的必需 `dsig:Transforms` 子元素。 `dsig:Transform` 元素具有以下属性。

| Attribute | 说明 |
|-------------| - |
| `Algorithm` | 用于计算此文件摘要的算法。 当前使用的唯一值为 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `urn:schemas-microsoft-com:HashTransforms.Identity` 。 |

### <a name="dsigdigestmethod"></a>dsig:DigestMethod
 `dsig:DigestMethod`元素是 元素的必需 `hash` 子元素。 `dsig:DigestMethod` 元素具有以下属性。

| Attribute | 说明 |
|-------------| - |
| `Algorithm` | 用于计算此文件摘要的算法。 当前使用的唯一值为 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `http://www.w3.org/2000/09/xmldsig#sha1` 。 |

### <a name="dsigdigestvalue"></a>dsig:DigestValue
 `dsig:DigestValue`元素是 元素的必需 `hash` 子元素。 `dsig:DigestValue` 元素没有属性。 其文本值为指定文件的计算哈希。

## <a name="remarks"></a>备注
 应用程序使用的所有程序集都必须具有相应的 `dependency` 元素。 依赖程序集不包括必须预装在全局程序集缓存中作为平台程序集的程序集。

## <a name="example"></a>示例
 下面的代码示例演示 `dependency` 了应用程序清单 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 中的元素。 此代码示例是为应用程序清单主题提供的ClickOnce[示例的一](../deployment/clickonce-application-manifest.md)部分。

```xml
<dependency>
  <dependentOS>
    <osVersionInfo>
      <os
        majorVersion="4"
        minorVersion="10"
        buildNumber="0"
        servicePackMajor="0" />
    </osVersionInfo>
  </dependentOS>
</dependency>
<dependency>
  <dependentAssembly
    dependencyType="preRequisite"
    allowDelayedBinding="true">
    <assemblyIdentity
      name="Microsoft.Windows.CommonLanguageRuntime"
      version="4.0.20506.0" />
  </dependentAssembly>
</dependency>

<dependency>
  <dependentAssembly
    dependencyType="install"
    allowDelayedBinding="true"
    codebase="MyApplication.exe"
    size="4096">
    <assemblyIdentity
      name="MyApplication"
      version="1.0.0.0"
      language="neutral"
      processorArchitecture="x86" />
    <hash>
      <dsig:Transforms>
        <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
      </dsig:Transforms>
      <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
      <dsig:DigestValue>DpTW7RzS9IeT/RBSLj54vfTEzNg=</dsig:DigestValue>
    </hash>
  </dependentAssembly>
</dependency>
```

## <a name="see-also"></a>请参阅
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)
- [\<dependency> 元素](../deployment/dependency-element-clickonce-deployment.md)