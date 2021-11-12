---
title: '&lt;fileAssociation&gt; 元素（ClickOnce 应用程序） | Microsoft Docs'
description: fileAssociation 元素标识要与应用程序关联的文件扩展名。 fileAssociation 元素是可选的。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <fileAssociation> element [ClickOnce application manifest]
- manifests [ClickOnce], fileAssociation element
ms.assetid: 8f951b4f-54f9-412e-a9e5-af4e379fcf08
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: a17f239b7abaf981416b86ec785cb7a4d7e95e8a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665629"
---
# <a name="ltfileassociationgt-element-clickonce-application"></a>&lt;fileAssociation&gt; 元素（ClickOnce 应用程序）
标识要与应用程序关联的文件扩展名。

## <a name="syntax"></a>语法

```xml
<fileAssociation
    xmlns="urn:schemas-microsoft-com:clickonce.v1"
    extension
    description
    progid
    defaultIcon
/>
```

## <a name="elements-and-attributes"></a>元素和属性
 `fileAssociation` 元素是可选的。 元素具有以下属性。

|属性|说明|
|---------------|-----------------|
|`extension`|必需。 要与应用程序关联的文件扩展名。|
|`description`|必需。 对 shell 使用的文件类型的说明。|
|`progid`|必需。 唯一标识文件类型的名称。|
|`defaultIcon`|必需。 指定要用于具有此扩展名的文件的图标。 必须使用包含此元素的 [\<assembly> 元素](../deployment/assembly-element-clickonce-application.md)中的 [\<file> 元素](../deployment/file-element-clickonce-application.md)指定图标文件。|

## <a name="remarks"></a>备注
 此元素必须包含对“urn:schemas-microsoft-com:clickonce.v1”的 XML 命名空间引用。 如果使用了 `<fileAssociation>` 元素，它必须位于其父元素 [\<assembly> 元素](../deployment/assembly-element-clickonce-application.md) 中的 `<application>` 元素之后。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 不会覆盖现有文件关联。 但 ClickOnce 应用程序只能替代当前用户的文件扩展名。 卸载 ClickOnce 的应用程序后，ClickOnce 会删除该用户的文件关联，每台计算机的关联会再次变为活动状态。

## <a name="example"></a>示例
 下面的代码示例演示使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署的文本编辑器应用程序的应用程序清单中的 `fileAssociation` 元素。 此代码示例还包括 `defaultIcon` 属性所需的 [\<file> 元素](../deployment/file-element-clickonce-application.md)。

```xml
<file name="text.ico" size="4286">
  <hash>
    <dsig:Transforms>
      <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
    </dsig:Transforms>
    <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
    <dsig:DigestValue>0joAqhmfeBb93ZneZv/oTMP2brY=</dsig:DigestValue>
  </hash>
</file>
<file name="writing.ico" size="9662">
  <hash>
    <dsig:Transforms>
      <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
    </dsig:Transforms>
    <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
    <dsig:DigestValue>2cL2U7cm13nG40v9MQdxYKazIwI=</dsig:DigestValue>
  </hash>
</file>
<fileAssociation xmlns="urn:schemas-microsoft-com:clickonce.v1" extension=".text" description="Text  Document (ClickOnce)" progid="Text.Document" defaultIcon="text.ico" />
<fileAssociation xmlns="urn:schemas-microsoft-com:clickonce.v1" extension=".writing" description="Writings (ClickOnce)" progid="Writing.Document" defaultIcon="writing.ico" />
```

## <a name="see-also"></a>另请参阅
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)