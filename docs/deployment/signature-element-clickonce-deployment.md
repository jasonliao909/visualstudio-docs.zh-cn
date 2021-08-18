---
title: '&lt;Signature &gt; 元素 (ClickOnce部署) |Microsoft Docs'
description: Signature 元素包含对此部署清单进行数字签名所必需的信息。 为部署清单签名是可选的，但建议这样做。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <Signature> element [ClickOnce deployment manifest]
ms.assetid: c99b07ad-e8ba-43f2-b0d6-3745e7a7c8b3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 8312a9660ca621857b835f43f9e43a173c93240e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122035600"
---
# <a name="ltsignaturegt-element-clickonce-deployment"></a>&lt;部署 &gt; (ClickOnce签名) 
包含对此部署清单进行数字签名所需的信息。

## <a name="syntax"></a>语法

```xml

<Signature> 
   XML signature information 
</Signature>
```

## <a name="remarks"></a>备注
 使用信封签名对部署清单进行签名是可选的，但建议这样做。 有关对 XML 文件进行签名的信息，请参阅 万维网联合会 建议，"XML 签名语法和处理"，如 中所述 [http://www.w3.org/TR/xmldsig-core/](https://www.w3.org/TR/xmldsig-core/) 。

 如果要对清单进行签名，则必须为所有文件提供哈希。 无法对包含未哈希的文件的清单进行签名，因为用户无法验证未哈希文件的内容。

## <a name="example"></a>示例
 下面的代码示例演示部署 `Signature` 中使用的部署清单中的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 元素。

```xml
<Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
  <SignedInfo>
    <CanonicalizationMethod Algorithm=
           "http://www.w3.org/TR/2001/REC-xml-c14n-20010315" />
    <SignatureMethod Algorithm=
           "http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
    <Reference URI="">
      <Transforms>
        <Transform Algorithm=
           "http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
      </Transforms>
      <DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
      <DigestValue>d2z5AE...</DigestValue>
    </Reference>
  </SignedInfo>
  <SignatureValue>
4PHj6SaopoLp...
  </SignatureValue>
  <KeyInfo>
    <X509Data>
      <X509Certificate>
MIIHnTCCBoWgAwIBAgIKJY9+nwAHAAB...
      </X509Certificate>
    </X509Data>
  </KeyInfo>
</Signature>
```

## <a name="see-also"></a>请参阅
- [ClickOnce部署清单](../deployment/clickonce-deployment-manifest.md)
