---
title: '&lt;publisherIdentity &gt; 元素 (ClickOnce部署) |Microsoft Docs'
description: publisherIdentity 元素包含有关对部署清单进行签名的发布服务器的信息。 已签名清单需要 元素。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- publisherIdentity Element [ClickOnce deployment manifest], introduction
- required element for signed manifests [ClickOnce], publisherIdentity Element
- publisherIdentity Element [ClickOnce deployment manifest], syntax, elements, and attributes
ms.assetid: 34c579db-d2f2-4b66-b9c8-47207f33d950
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: a0421172d9f97fde3fcf558214b7325152e3c15373a70d242f9b68c013a5cc42
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121343411"
---
# <a name="ltpublisheridentitygt-element-clickonce-deployment"></a>&lt;publisherIdentity &gt; 元素 (ClickOnce部署) 
包含有关为此部署清单签名的发布者的信息。

## <a name="syntax"></a>语法

```xml
<publisherIdentity
   name
   issuerKeyHash
/>
```

## <a name="elements-and-attributes"></a>元素和属性
 `publisherIdentity`已签名清单需要 元素。 下表显示了 元素支持 `publisherIdentity` 的属性。

|Attribute|说明|
|---------------|-----------------|
|`name`|必需。 描述发布此应用程序的一方的身份。|
|`issuerKeyHash`|必需。 包含证书颁发者公钥的 SHA-1 哈希。|

#### <a name="parameters"></a>Parameters

## <a name="property-valuereturn-value"></a>属性值/返回值

## <a name="exceptions"></a>例外

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求

## <a name="subhead"></a>副标题