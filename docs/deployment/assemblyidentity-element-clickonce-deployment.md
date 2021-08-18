---
title: '&lt;assemblyIdentity &gt; 元素 (ClickOnce部署) |Microsoft Docs'
description: 程序集部署中需要 assemblyIdentity ClickOnce元素。 它不包含任何子元素，并且具有本文中所述的属性。
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
- <assemblyIdentity> element [ClickOnce deployment manifest]
ms.assetid: f4a3bb83-c800-47d0-9905-9a5ae2486838
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: e4633b5ed024b1e43134b33827a5614bfa5f8d17
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122146493"
---
# <a name="ltassemblyidentitygt-element-clickonce-deployment"></a>&lt;assemblyIdentity &gt; 元素 (ClickOnce部署) 
标识应用程序的主 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 程序集。

## <a name="syntax"></a>语法

```xml

      <assemblyIdentity  
   name 
   version
   publicKeyToken
   processorArchitecture
    type
/>
```

## <a name="elements-and-attributes"></a>元素和属性
 `assemblyIdentity` 元素是必需的。 它不包含子元素，并且具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`name`|必需。 标识部署的可读名称，以便提供信息。<br /><br /> 如果 `name` 包含特殊字符（如单引号或双引号），则应用程序可能无法激活。|
|`version`|必需。 指定程序集的版本号，格式如下 `major.minor.build.revision` ：。<br /><br /> 此值必须在更新的清单中递增，以触发应用程序更新。|
|`publicKeyToken`|必需。 指定一个 16 个字符的十六进制字符串，该字符串表示部署清单签名时所基于的公钥的 SHA-1 哈希值的最后 8 个字节。 用于签名的公钥必须为 2048 位或更大。<br /><br /> 尽管建议对程序集进行签名，但可选，但此属性是必需的。 如果程序集未签名，应复制自签名程序集中的值或使用所有零的"虚拟"值。|
|`processorArchitecture`|必需。 指定处理器。 有效值适用于所有处理器、32 位 Windows、64 位 Windows 和 `msil` `x86` Intel `IA64` `Itanium` 64 位 Itanium 处理器。|
|`type`|必需。 为了与Windows并行安装技术兼容。 唯一允许的值为 `win32` 。|

## <a name="remarks"></a>备注

## <a name="example"></a>示例
 下面的代码示例演示了 `assemblyIdentity` 部署清单中的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 元素。 此代码示例是为部署清单主题提供的较大ClickOnce[的一](../deployment/clickonce-deployment-manifest.md)部分。

```xml
<!-- Identify the deployment. -->
<assemblyIdentity
  name="My Application Deployment.app"
  version="1.0.0.0"
  publicKeyToken="43cb1e8e7a352766"
  language="neutral"
  processorArchitecture="x86"
  xmlns="urn:schemas-microsoft-com:asm.v1" />
```

## <a name="see-also"></a>请参阅
- [ClickOnce部署清单](../deployment/clickonce-deployment-manifest.md)
- [\<assemblyIdentity> 元素](../deployment/assemblyidentity-element-clickonce-application.md)