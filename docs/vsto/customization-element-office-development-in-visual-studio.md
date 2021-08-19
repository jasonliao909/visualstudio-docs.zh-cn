---
title: '&lt;&gt;Visual Studio 中 Office 开发的自定义元素 () '
description: 了解 vstov4 命名空间的自定义元素如何描述特定的 Office 解决方案。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <customization> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: b2795a4bcfe74bbebdf37c0f59eded6ae2d08cfe
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122053893"
---
# <a name="ltcustomizationgt-element-office-development-in-visual-studio"></a>&lt;&gt;Visual Studio 中 Office 开发的自定义元素 () 
  `customization` 命名空间的 `vstov4` 元素描述特定 Office 解决方案。 对于文档级自定义项和 VSTO 外接程序，子元素是不同的。

## <a name="syntax-for-document-level-customizations"></a>文档级自定义项的语法

```xml
<customization
  id
  <document
    solutionId
  />
</customization>
```

## <a name="syntax-for-vsto-add-ins"></a>VSTO 外接程序的语法

```xml
<customization
  id
  <appAddin
    application
    loadBehavior
    keyName>
  <friendlyName></friendlyName>
  <description></description>
  <formRegions></formRegions>
</customization>
```

## <a name="elements-and-attributes"></a>元素和属性
 `customization` 元素包含特定于自定义项的信息。 此元素必须在以下命名空间中： `vstov4=urn:schemas-microsoft-com:vsto.v4`。 每个 Office 解决方案都有一个 `customization` 元素。 例如，如果你在一个多项目部署中部署三个 Office 解决方案，则应用程序清单中有三个 `customization` 元素。

 程序集的子元素也必须在此命名空间中。

 `customization` 元素具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`id`|对于多项目部署是必需的。 `id` 元素唯一地标识 Office 解决方案。|

### <a name="document-level-customizations"></a>Document-Level 自定义
 `customization` 元素具有以下子元素。

#### <a name="document"></a>文档
 `document`命名空间中的元素 `vstov4` 在[&#60;文档&#62; 元素中定义 &#40;Office 在 Visual Studio&#41;中进行开发](../vsto/document-element-office-development-in-visual-studio.md)。

### <a name="vsto-add-ins"></a>VSTO 外接程序
 `customization` 元素具有以下子元素。

#### <a name="appaddin"></a>appAddin
 `appAddin`命名空间中的元素 `vstov4` 在[&#60;appAddin&#62; 元素中定义 &#40;Office 在 Visual Studio&#41;中进行开发](../vsto/appaddin-element-office-development-in-visual-studio.md)。

## <a name="example-of-a-document-level-customization"></a>文档级自定义项示例

### <a name="description"></a>说明
 下面的代码示例演示了文档级自定义项的 `customization` 元素。 此代码示例是[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

### <a name="code"></a>代码

```xml
<vstov4:customization>
  <vstov4:document
    solutionId="73e" />
</vstov4:customization>
```

## <a name="example-of-a-vsto-add-in"></a>VSTO 外接程序的示例

### <a name="description"></a>说明
 下面的代码示例演示了 `customization` VSTO 外接程序的元素。 这是一个包含窗体区域的 Outlook VSTO 外接程序。 此代码示例是[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

### <a name="code"></a>代码

```xml
<vstov4:customization>
  <vstov4:appAddIn
    application="Outlook"
    loadBehavior="3"
    keyName="ContosoOutlookAddIn">
    <vstov4:friendlyName>
      ContosoOutlookAddIn
    </vstov4:friendlyName>
    <vstov4:description>
      ContosoOutlookAddIn - Outlook VSTO Add-in
      created with Visual Studio Tools for Office
    </vstov4:description>
    <vstov4:formRegions>
      <vstov4:formRegion
          name="OutlookAddIn1.FormRegion1">
        <vstov4:messageClass name="IPM.Note" />
        <vstov4:messageClass name="IPM.Contact" />
        <vstov4:messageClass name="IPM.Appointment" />
      </vstov4:formRegion>
    </vstov4:formRegions>
  </vstov4:appAddIn>
</vstov4:customization>
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)