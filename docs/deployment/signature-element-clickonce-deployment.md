---
title: '&lt;Signature&gt; 元素（ClickOnce 部署）| Microsoft Docs'
description: Signature 元素包含对此部署清单进行数字签名所需的信息。 对部署清单进行签名的操作是可选的，但建议这样做。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665460"
---
# <a name="ltsignaturegt-element-clickonce-deployment"></a>&lt;Signature&gt; 元素（ClickOnce部署）
包含对此部署清单进行数字签名所需的信息。

## <a name="syntax"></a>语法

```xml

<Signature> 
   XML signature information 
</Signature>
```

## <a name="remarks"></a>备注
 使用信封签名对部署清单进行签名的操作是可选的，但建议这样做。 有关对 XML 文件进行签名的详细信息，请参阅万维网联合会建议，即 [http://www.w3.org/TR/xmldsig-core/](https://www.w3.org/TR/xmldsig-core/) 中所述的“XML 签名语法和处理”。

 如果要对清单进行签名，必须为所有文件提供哈希。 不能对包含未进行哈希处理的文件的清单进行签名，因为用户无法验证未经过哈希处理的文件的内容。

## <a name="example"></a>示例
 下面的代码示例演示了 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署中使用的部署清单中的 `Signature` 元素。

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

## <a name="see-also"></a>另请参阅
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)
