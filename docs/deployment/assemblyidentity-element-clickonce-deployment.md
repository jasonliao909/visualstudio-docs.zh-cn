---
title: '&lt;assemblyIdentity&gt; 元素（ClickOnce 部署）| Microsoft Docs'
description: assemblyIdentity 元素在 ClickOnce 部署中是必需的。 它不包含任何子元素，但包含本文中所述的属性。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665167"
---
# <a name="ltassemblyidentitygt-element-clickonce-deployment"></a>&lt;assemblyIdentity&gt; 元素（ClickOnce 部署）
标识 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的主程序集。

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
 `assemblyIdentity` 元素是必需的。 它不包含任何子元素，但具有以下属性。

|属性|说明|
|---------------|-----------------|
|`name`|必需。 标识出于信息目的的部署的人类可读名称。<br /><br /> 如果 `name` 包含特殊字符（如单引号或双引号），则应用程序可能无法激活。|
|`version`|必需。 指定程序集的版本号，格式如下：`major.minor.build.revision`。<br /><br /> 此值必须在更新的清单中递增才能触发应用程序更新。|
|`publicKeyToken`|必需。 指定 16 个字符的十六进制字符串，该字符串表示对部署清单签名时所用公钥的 SHA-1 哈希值的最后 8 个字节。 用于签名的公钥必须为 2048 位或更大。<br /><br /> 尽管建议对程序集签名，但这是可选的，但此属性是必需的。 如果未为对程序集进行签名，则应从自签名的程序集复制一个值，或使用全部为零的“虚拟”值。|
|`processorArchitecture`|必需。 指定处理器。 有效值为适用于所有处理器的 `msil`，适用于 32 位 Windows 的 `x86`，适用于 64 位 Windows 的 `IA64`，以及适用于 Intel 64 位 Itanium 处理器的 `Itanium`。|
|`type`|必需。 与 Windows 并行安装技术兼容。 唯一允许的值为 `win32`。|

## <a name="remarks"></a>备注

## <a name="example"></a>示例
 下面的代码示例演示了 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署清单中的 `assemblyIdentity` 元素。 此代码示例摘自 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)中提供的一个更大的示例。

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

## <a name="see-also"></a>另请参阅
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)
- [\<assemblyIdentity> 元素](../deployment/assemblyidentity-element-clickonce-application.md)