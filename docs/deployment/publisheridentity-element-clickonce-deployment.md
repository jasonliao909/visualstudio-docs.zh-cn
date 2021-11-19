---
title: '&lt;publisherIdentity&gt; 元素（ClickOnce 部署）| Microsoft Docs'
description: publisherIdentity 元素包含对部署清单进行签名的发布服务器的相关信息。 已签名清单需要此元素。
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
ms.openlocfilehash: 01f207d0430b17dddfdc955ae03e213fbcc2c415
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671810"
---
# <a name="ltpublisheridentitygt-element-clickonce-deployment"></a>&lt;publisherIdentity&gt; 元素（ClickOnce 部署）
包含有关为此部署清单签名的发布者的信息。

## <a name="syntax"></a>语法

```xml
<publisherIdentity
   name
   issuerKeyHash
/>
```

## <a name="elements-and-attributes"></a>元素和属性
 已签名清单需要 `publisherIdentity` 元素。 下表显示了 `publisherIdentity` 元素支持的属性。

|属性|说明|
|---------------|-----------------|
|`name`|必需。 描述发布此应用程序的一方的身份。|
|`issuerKeyHash`|必需。 包含证书颁发者公钥的 SHA-1 哈希。|

#### <a name="parameters"></a>参数

## <a name="property-valuereturn-value"></a>属性值/返回值

## <a name="exceptions"></a>例外

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求

## <a name="subhead"></a>副标题