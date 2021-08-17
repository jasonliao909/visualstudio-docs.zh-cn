---
title: '&lt;assembly &gt; Element (ClickOnce Deployment) |Microsoft Docs'
description: 程序集元素是根元素，在部署ClickOnce必需。 其第一个包含的元素必须是 assemblyIdentity 元素。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#assembly
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assembly> element [ClickOnce deployment manifest]
ms.assetid: b8e3362a-f821-4696-b98d-571d4bbfe431
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 54affc5f75a17fe93beac0ee62207f6c25a1c448
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122074028"
---
# <a name="ltassemblygt-element-clickonce-deployment"></a>&lt;assembly &gt; 元素 (ClickOnce部署) 
部署清单的顶级元素。

## <a name="syntax"></a>语法

```xml

      <assembly  
   manifestVersion
/>
```

## <a name="elements-and-attributes"></a>元素和属性
 `assembly`元素是根元素，是必需的。 其第一个包含的元素必须是 `assemblyIdentity` 元素。 清单元素必须具有以下命名空间 `urn:schemas-microsoft-com:asm.v1` ：、 `urn:schemas-microsoft-com:asm.v2` 和 `http://www.w3.org/2000/09/xmldsig#` 。 程序集的子元素还必须通过继承或标记来在这些命名空间中。

 `assembly` 元素具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`manifestVersion`|必需。 此属性必须设置为 `1.0` 。|

## <a name="example"></a>示例
 下面的代码示例演示了使用 部署的应用程序 `assembly` 的部署清单中的元素 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 此代码示例是为部署清单主题提供的ClickOnce[示例的一](../deployment/clickonce-deployment-manifest.md)部分。

```xml
<asmv1:assembly
  xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd"
  manifestVersion="1.0"
  xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"
  xmlns:dsig=http://www.w3.org/2000/09/xmldsig#
  xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1"
  xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2"
  xmlns="urn:schemas-microsoft-com:asm.v2"
  xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
  xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"
  xmlns:xrml="urn:mpeg:mpeg21:2003:01-REL-R-NS"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
```

## <a name="see-also"></a>请参阅
- [ClickOnce部署清单](../deployment/clickonce-deployment-manifest.md)
- [\<assembly> 元素](../deployment/assembly-element-clickonce-application.md)