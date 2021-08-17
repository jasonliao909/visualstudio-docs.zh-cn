---
title: '&lt;appAddin &gt; 元素 (Office开发Visual Studio) '
description: 了解 vstov4 命名空间的 appAddin 元素如何存储外接程序VSTO自定义特定信息。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <appAddin> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 3e8a6ee4a422c156bfb81108c830f917e5ee8020
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122047252"
---
# <a name="ltappaddingt-element-office-development-in-visual-studio"></a>&lt;appAddin &gt; 元素 (Office开发Visual Studio) 
  命名空间 **的 appAddin** `vstov4` 元素存储外接程序的VSTO特定信息。

## <a name="syntax"></a>语法

```xml
<appAddin
  application
  loadBehavior
  keyName>
  <friendlyName>
  <description>
  <formRegions></formRegions>
</appAddin>
```

## <a name="elements-and-attributes"></a>元素和属性
 **appAddin** 元素是必需的，并且位于 `vstov4` 命名空间中。 应用程序清单中仅定义了一个 **appAddin** 元素。

 **appAddin** 元素具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|**应用程序**|必需。 标识 Microsoft Office 应用程序。 值可以是以下值之一：Excel、InfoPath、Outlook、PowerPoint、Project、Visio 或 Word。|
|**loadBehavior**|可选。 默认情况下，通过将此值设置为 来启用 **loadBehavior。** 为进行调试，可以通过将此值设置为 2 来禁用 VSTO 外接程序。 有关详细信息，请参阅标题为 LoadBehavior Values in [Registryntries](../vsto/registry-entries-for-vsto-add-ins.md)for VSTO 外接程序 的表。|
|**keyName**|必需。 此值是该应用程序将用于加载 VSTO 外接程序的注册表项名称。 有关详细信息，请参阅外接程序 的[VSTO项](../vsto/registry-entries-for-vsto-add-ins.md)。|

 **appAddin** 元素具有以下子元素。

### <a name="friendlyname"></a>friendlyName
 可选。 **friendlyName** 元素在&#60;中&#62; [friendlyName &#40;Office元素Visual Studio&#41;。](../vsto/friendlyname-element-office-development-in-visual-studio.md)

### <a name="description"></a>description
 可选。 description 元素在&#60;&#62;[开发&#40;Office说明Visual Studio&#41;。 ](../vsto/description-element-office-development-in-visual-studio.md)

### <a name="formregions"></a>formRegions
 仅为包含窗体区域的 Outlook VSTO 外接程序所需。 **formRegions** 元素在&#60;[&#62; &#40;Office 开发中的 formRegions Visual Studio&#41;中进行了Visual Studio&#41;。](../vsto/formregions-element-office-development-in-visual-studio.md)

## <a name="vsto-add-in-example"></a>VSTO外接程序示例

### <a name="description"></a>说明
 下面的代码示例演示了使用 部署Outlook解决方案中的 **appAddin** 元素 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 。 此代码示例是应用程序清单中为解决方案 提供Office[的一部分](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
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
```

## <a name="see-also"></a>请参阅

- [解决方案的应用程序Office清单](../vsto/application-manifests-for-office-solutions.md)
- [解决方案部署Office清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)