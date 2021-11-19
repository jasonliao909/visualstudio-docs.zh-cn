---
title: '&lt;assemblyIdentity&gt; 元素（ClickOnce 应用程序）| Microsoft Docs'
description: assemblyIdentity 元素在 ClickOnce 应用程序中是必需的。 它不包含任何子元素，但包含本文中所述的属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#assemblyIdentity
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assemblyIdentity> element [ClickOnce application manifest]
ms.assetid: f48e9531-efac-4d11-8166-f63a5ece1ac5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: c70873e347999b7e7a8503febf78771ceeaad0d3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665169"
---
# <a name="ltassemblyidentitygt-element-clickonce-application"></a>&lt;assemblyIdentity&gt; 元素（ClickOnce 应用程序）
标识 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署中部署的应用程序。

## <a name="syntax"></a>语法

```xml

      <assemblyIdentity
   name
   version
   publicKeyToken
   processorArchitecture
   language
/>
```

## <a name="elements-and-attributes"></a>元素和属性
 `assemblyIdentity` 元素是必需的。 它不包含任何子元素，但具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Name`|必需。 标识应用程序的名称。<br /><br /> 如果 `Name` 包含特殊字符（如单引号或双引号），则应用程序可能无法激活。|
|`Version`|必需。 按以下格式指定应用程序的版本号：`major.minor.build.revision`|
|`publicKeyToken`|可选。 指定一个 16 个字符的十六进制字符串，该字符串表示应用程序或程序集签名时所用公钥的 `SHA-1` 哈希值的最后 8 个字节。 用于目录签名的公钥必须是 2048 位或更高。<br /><br /> 尽管建议对程序集签名，但这是可选的，但此属性是必需的。 如果未为对程序集进行签名，则应从自签名的程序集复制一个值，或使用全部为零的“虚拟”值。|
|`processorArchitecture`|必需。 指定处理器。 有效值为适用于所有处理器的 `msil`，适用于 32 位 Windows 的 `x86`，适用于 64 位 Windows 的 `IA64`，以及适用于 Intel 64 位 Itanium 处理器的 `Itanium`。|
|`language`|必需。 标识程序集由两部分组成的语言代码（例如 `en-US`）。 此元素位于 `asmv2` 命名空间中。 如果未指定，则默认值为 `neutral`。|

## <a name="examples"></a>示例

### <a name="description"></a>说明
 下面的代码示例演示了 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单中的 `assemblyIdentity` 元素。 此代码示例摘自 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)中提供的一个更大的示例。

### <a name="code"></a>代码

```xml
<asmv1:assemblyIdentity
  name="My Application Deployment.exe"
  version="1.0.0.0"
  publicKeyToken="43cb1e8e7a352766"
  language="neutral"
  processorArchitecture="x86"
  type="win32" />
```

## <a name="see-also"></a>另请参阅
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
- [\<assemblyIdentity> 元素](../deployment/assemblyidentity-element-clickonce-deployment.md)