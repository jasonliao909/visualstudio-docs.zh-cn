---
title: '&lt;assemblyIdentity &gt; 元素 (ClickOnce应用程序) |Microsoft Docs'
description: 程序集应用程序中需要 assemblyIdentity ClickOnce元素。 它不包含任何子元素，并且具有本文中所述的属性。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122090057"
---
# <a name="ltassemblyidentitygt-element-clickonce-application"></a>&lt;assemblyIdentity &gt; (ClickOnce应用程序) 
标识部署中部署 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 的应用程序。

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
 `assemblyIdentity` 元素是必需的。 它不包含子元素，并且具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`Name`|必需。 标识应用程序的名称。<br /><br /> 如果 `Name` 包含特殊字符（如单引号或双引号），则应用程序可能无法激活。|
|`Version`|必需。 采用以下格式指定应用程序的版本号： `major.minor.build.revision`|
|`publicKeyToken`|可选。 指定一个 16 个字符的十六进制字符串，该字符串表示对应用程序或程序集进行签名的公钥哈希值的最后 8 `SHA-1` 个字节。 用于对目录进行签名的公钥必须为 2048 位或更大。<br /><br /> 尽管建议对程序集进行签名，但可选，但此属性是必需的。 如果程序集未签名，应复制自签名程序集中的值或使用所有零的"虚拟"值。|
|`processorArchitecture`|必需。 指定处理器。 有效值适用于所有处理器、32 位 Windows、64 位 Windows 和 `msil` `x86` Intel `IA64` `Itanium` 64 位 Itanium 处理器。|
|`language`|必需。 标识两部分语言代码 (例如，) `en-US` 程序集的一部分。 此元素位于 `asmv2` 命名空间中。 如果未指定，则默认值为 `neutral` 。|

## <a name="examples"></a>示例

### <a name="description"></a>说明
 下面的代码示例演示了 `assemblyIdentity` 应用程序清单 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 中的元素。 此代码示例是应用程序清单 中提供的较大ClickOnce[的一部分](../deployment/clickonce-application-manifest.md)。

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

## <a name="see-also"></a>请参阅
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)
- [\<assemblyIdentity> 元素](../deployment/assemblyidentity-element-clickonce-deployment.md)