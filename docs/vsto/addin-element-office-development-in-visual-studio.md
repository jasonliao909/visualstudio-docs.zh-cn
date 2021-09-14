---
description: vstav3 命名空间的 addin 元素包含特定于使用 Microsoft Office VSTO 开发的外接程序和文档级自定义Visual Studio。
title: '&lt;addin &gt; 元素 (Office Visual Studio) '
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <addIn> element
- addin element
- <addin> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 63d5adb7d4fab31d7f4d24f40948d8e4acd26f10
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664766"
---
# <a name="ltaddingt-element-office-development-in-visual-studio"></a>&lt;addin &gt; 元素 (Office Visual Studio) 
  命名空间 **的 addin** 元素包含特定于使用 Microsoft Office VSTO 开发的外接程序和文档级自定义 `vstav3` Visual Studio。

## <a name="syntax"></a>语法

```xml
<addIn>
  <entryPointsCollection>
    <entryPoints>
      <entryPoint>
      </entryPoint>
    </entryPoints>
  </entryPointsCollection>
  <update></update>
  <postActions>
    <postAction>
      <postActionData>
      </postActionData>
    <postAction>
  </postActions>
  <application>
    <customization>
    </customization>
  </application
</addIn>
```

## <a name="elements-and-attributes"></a>元素和属性
 命名空间 **的 addin** `vstav3` 元素包含有关 Office 解决方案和 Microsoft Office 应用程序的信息。 此元素必须在以下命名空间中： `vstav3=urn:schemas-microsoft-com:vsta.v3`。 子元素也必须在此命名空间中。

 `addin` 元素没有属性。

 `addin` 元素具有以下子元素。

### <a name="entrypoints"></a>entryPoints
 必需。 **entryPoints** 元素在&#60;[中&#62;&#40;Office entryPoints Visual Studio&#41;。](../vsto/entrypoints-element-office-development-in-visual-studio.md)

### <a name="update"></a>update
 必需。 update 元素在&#60;&#62; [&#40;Office 中Visual Studio&#41;。 ](../vsto/update-element-office-development-in-visual-studio.md)

### <a name="postactions"></a>postActions
 可选。 **postActions** 元素在&#60;中&#62; [postActions &#40;Office元素Visual Studio&#41;。](../vsto/postactions-element-office-development-in-visual-studio.md)

### <a name="application"></a>application
 必需。 应用程序 **元素** 在&#60;[中&#62;&#40;Office元素Visual Studio&#41;。](../vsto/application-element-office-development-in-visual-studio.md)

## <a name="document-level-customization-example"></a>文档级自定义示例

### <a name="description"></a>说明
 下面的代码示例演示使用 部署的文档级 Office解决方案中的 **addin** 元素 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 。 此代码示例是应用程序清单中为解决方案 提供Office[的一部分](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstav3:addIn
  xmlns:vstav3="urn:schemas-microsoft-com:vsta.v3">
  <vstav3:entryPointsCollection>
    <vstav3:entryPoints>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.ThisWorkbook">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.Sheet1">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.Sheet2">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.Sheet3">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
    </vstav3:entryPoints>
  </vstav3:entryPointsCollection>
  <vstav3:update
    enabled="true">
    <vstav3:expiration
      maximumAge="7"
      unit="days" />
  </vstav3:update>
  <vstav3:application>
    <vstov4:customizations
      xmlns:vstov4="urn:schemas-microsoft-com:vsto.v4">
      <vstov4:customization>
        <vstov4:document
          solutionId="73e" />
      </vstov4:customization>
    </vstov4:customizations>
  </vstav3:application>
</vstav3:addIn>
```

## <a name="vsto-add-in-example"></a>VSTO外接程序示例

### <a name="description"></a>说明
 下面的代码示例演示使用 部署的应用程序级别 Office解决方案中的 **addin** 元素 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 。 此代码示例是应用程序清单中为解决方案 提供Office[的一部分](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstav3:addIn
  xmlns:vstav3="urn:schemas-microsoft-com:vsta.v3">
  <vstav3:entryPointsCollection>
    <vstav3:entryPoints>
      <vstav3:entryPoint
        class="ContosoOutlookAddIn.ThisAddIn">
        <assemblyIdentity
          name="ContosoOutlookAddIn"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
    </vstav3:entryPoints>
  </vstav3:entryPointsCollection>
  <vstav3:update
    enabled="true">
    <vstav3:expiration
      maximumAge="7"
      unit="days" />
  </vstav3:update>
  <vstav3:application>
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
  </vstav3:application>
</vstav3:addIn>
```

## <a name="see-also"></a>另请参阅

- [解决方案的应用程序Office清单](../vsto/application-manifests-for-office-solutions.md)
- [解决方案部署Office清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)
