---
title: '&lt;自定义 &gt; 元素 (Office 开发 Visual Studio 中) '
description: 了解 vstov4 命名空间的 "自定义" 元素如何包含有关安装和加载每个 Office 解决方案的所有信息。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- <customizations> element
- customizations element
- application manifests [Office development in Visual Studio], <customizations> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: e9548c0cb730f9386a8a167e403161850a082e4a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122026520"
---
# <a name="ltcustomizationsgt-element-office-development-in-visual-studio"></a>&lt;自定义 &gt; 元素 (Office 开发 Visual Studio 中) 
  `customizations` 命名空间的 `vstov4` 元素包括有关安装和加载各个 Office 解决方案的所有信息。

## <a name="syntax-for-document-level-customizations"></a>文档级自定义项的语法

```xml
<customizations>
  <customization
    id
    <document
      solutionId
    />
  </customization>
</customizations>
```

## <a name="syntax-for-vsto-add-ins"></a>VSTO 外接程序的语法

```xml
<customizations>
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
</customizations>
```

## <a name="elements-and-attributes"></a>元素和属性
 `customizations` 元素包括有关各个 Office 解决方案的特定信息。 此元素必须在以下命名空间中： `vstov4=urn:schemas-microsoft-com:vsto.v4`。 程序集的子元素也必须在此命名空间中。

 `customizations` 元素没有属性。

 `customizations` 元素具有以下子元素。

### <a name="customization"></a>自定义
 必需。 `customization`命名空间中的元素 `vstov4` 在[&#60;自定义&#62; 元素中定义 &#40;Office 在 Visual Studio&#41;中进行开发](../vsto/customization-element-office-development-in-visual-studio.md)。

## <a name="example-of-a-document-level-customization"></a>文档级自定义项示例

### <a name="description"></a>说明
 下面的代码示例演示了文档级自定义项的 `customizations` 元素。

> [!NOTE]
> 此代码示例是[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

### <a name="code"></a>代码

```xml
<vstov4:customizations
  xmlns:vstov4="urn:schemas-microsoft-com:vsto.v4">
  <vstov4:customization>
    <vstov4:document
      solutionId="73e" />
  </vstov4:customization>
</vstov4:customizations>
```

## <a name="example-of-a-vsto-add-in"></a>VSTO 外接程序的示例

### <a name="description"></a>说明
 下面的代码示例演示了 `customizations` VSTO 外接程序的元素。 这是一个包含窗体区域的 Outlook VSTO 外接程序。 此代码示例是[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

### <a name="code"></a>代码

```xml
<vstov4:customizations
  xmlns:vstov4="urn:schemas-microsoft-com:vsto.v4">
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
</vstov4:customizations>
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)