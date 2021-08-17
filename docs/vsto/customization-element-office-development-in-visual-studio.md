---
title: '&lt;自定义 &gt; 元素 (Office开发Visual Studio) '
description: 了解 vstov4 命名空间的 customization 元素如何描述特定的Office解决方案。
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
ms.openlocfilehash: 2a2744e82fc1012e40257cb23371584eb7792aea9b24562ff1de9e66acbee1a9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394779"
---
# <a name="ltcustomizationgt-element-office-development-in-visual-studio"></a>&lt;自定义 &gt; 元素 (Office开发Visual Studio) 
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

|属性|说明|
|---------------|-----------------|
|`id`|对于多项目部署是必需的。 `id` 元素唯一地标识 Office 解决方案。|

### <a name="document-level-customizations"></a>Document-Level自定义项
 `customization` 元素具有以下子元素。

#### <a name="document"></a>文档
 命名空间中的 元素在&#60;文档中 `document` `vstov4` [&#62;&#40;Office开发Visual Studio&#41;。 ](../vsto/document-element-office-development-in-visual-studio.md)

### <a name="vsto-add-ins"></a>VSTO 外接程序
 `customization` 元素具有以下子元素。

#### <a name="appaddin"></a>appAddin
 命名空间 `appAddin` 中的 元素在&#60;`vstov4` appAddin&#62; 元素&#40;Office[中Visual Studio&#41;。 ](../vsto/appaddin-element-office-development-in-visual-studio.md)

## <a name="example-of-a-document-level-customization"></a>文档级自定义项的示例

### <a name="description"></a>说明
 下面的代码示例演示了文档级自定义项的 `customization` 元素。 此代码示例是应用程序清单中为解决方案 提供Office[的一部分](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstov4:customization>
  <vstov4:document
    solutionId="73e" />
</vstov4:customization>
```

## <a name="example-of-a-vsto-add-in"></a>外接程序VSTO示例

### <a name="description"></a>说明
 下面的代码示例演示了 `customization` VSTO 外接程序的 元素。 这是一个包含窗体区域的 Outlook VSTO 外接程序。 此代码示例是应用程序清单中为解决方案 提供Office[的一部分](../vsto/application-manifests-for-office-solutions.md)。

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

- [解决方案的应用程序Office清单](../vsto/application-manifests-for-office-solutions.md)
- [解决方案部署Office清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)