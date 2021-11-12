---
title: '&lt;description&gt; 元素（ClickOnce 部署） | Microsoft Docs'
description: description 元素标识用于在控制面板中创建 shell 表示和“添加或删除程序”项的应用程序信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#description
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <description> element [ClickOnce deployment manifest]
ms.assetid: 18f6919e-a3ab-4942-a57d-167fabfac44e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: fabce5e8d6f7b6bf59f1a62346c8d9b5927e2cae
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665632"
---
# <a name="ltdescriptiongt-element-clickonce-deployment"></a>&lt;description&gt; 元素（ClickOnce 部署）
标识用于在控制面板中创建 shell 表示和“添加或删除程序”项的应用程序信息。

## <a name="syntax"></a>语法

```xml

      <description 
   publisher 
   product
   suiteName
   supportUrl
/>
```

## <a name="elements-and-attributes"></a>元素和属性
 `description` 元素是必需的，它位于 `urn:schemas-microsoft-com:asm.v1` 命名空间中。 它不包含任何子元素，但具有以下属性。

|属性|说明|
|---------------|-----------------|
|`publisher`|必需。 当部署针对安装进行了配置，它标识在 Windows“开始”菜单中的图标位置和控制面板中的“添加或删除程序”项处使用的公司名称 。|
|`product`|必需。 标识完整的产品名称。 用作在 Windows“开始”菜单中安装的图标的标题。|
|`suiteName`|可选。 标识 Windows“开始”菜单 `publisher` 文件夹中的子文件夹。|
|`supportUrl`|可选。 指定在控制面板的“添加或删除程序”项中显示的一个支持 URL。 当针对安装配置了部署时，还为 Windows“开始”菜单中的应用程序支持创建了此 URL 的快捷方式。|

## <a name="remarks"></a>备注
 所有部署配置中都需要 description 元素。

## <a name="example"></a>示例
 下面的代码示例演示了 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署清单中的 `description` 元素。 此代码示例摘自 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)中提供的一个更大的示例。

```xml
<description
  asmv2:publisher="My Company Name"
  asmv2:product="My Application"
  xmlns="urn:schemas-microsoft-com:asm.v1" />
```

## <a name="see-also"></a>另请参阅
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)