---
title: '&lt;assembly&gt; 元素（ClickOnce 应用程序）| Microsoft Docs'
description: assembly 元素是根元素，是 ClickOnce 应用程序中必需的。 其第一个包含的元素必须是 assemblyIdentity 元素。
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
- <assembly> element [ClickOnce application manifest]
ms.assetid: 51410569-10f9-4c0a-96b5-d39185edbefc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: cc8fb424c3a6232f27737521604247cf55ebc20e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665172"
---
# <a name="ltassemblygt-element-clickonce-application"></a>&lt;assembly&gt; 元素（ClickOnce 应用程序）
应用程序清单的顶级元素。

## <a name="syntax"></a>语法

```xml

      <assembly
   manifestVersion
/>
```

## <a name="elements-and-attributes"></a>元素和属性
 `assembly` 元素为根元素，并且是必需的。 其第一个包含的元素必须是 `assemblyIdentity` 元素。 清单元素必须在以下命名空间之一中：

 `urn:schemas-microsoft-com:asm.v1`

 `urn:schemas-microsoft-com:asm.v2`

 `http://www.w3.org/2000/09/xmldsig#`

 assembly 的子元素还必须通过继承或标记存在于这些命名空间中。

 `assembly` 元素具有以下属性。

|属性|说明|
|---------------|-----------------|
|`manifestVersion`|必需。 `manifestVersion` 特性必须设置为 `1.0`。|

## <a name="example"></a>示例
 下面的代码示例展示 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的清单中的 `assembly` 元素。 此代码示例摘自 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)中提供的一个更大的示例。

```xml
<asmv1:assembly
  xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd"
  manifestVersion="1.0"
  xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"
  xmlns:dsig=http://www.w3.org/2000/09/xmldsig#
  xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2"
  xmlns="urn:schemas-microsoft-com:asm.v2"
  xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
  xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"
  xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance
  xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1">
```

## <a name="see-also"></a>另请参阅
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
- [\<assembly> 元素](../deployment/assembly-element-clickonce-deployment.md)
