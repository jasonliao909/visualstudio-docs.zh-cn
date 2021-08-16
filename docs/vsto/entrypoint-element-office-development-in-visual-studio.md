---
description: vstav3 命名空间的每个入口点元素都标识应在安装此 ClickOnce 应用程序时运行的自定义程序集。
title: '&lt;&gt;Visual Studio 中 Office 开发 (入口点元素) '
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <entryPoint> element
- <entryPoint> element
- entryPoint element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: ff0f3313da0479c7ec6a8dda0c2bc609e6f7b4a357821b9acf988e7ff599112a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121424341"
---
# <a name="ltentrypointgt-element-office-development-in-visual-studio"></a>&lt;&gt;Visual Studio 中 Office 开发 (入口点元素) 
  `entryPoint` 命名空间中的每个 `vstav3` 元素都标识应在安装此 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 应用程序时运行的自定义程序集。

## <a name="syntax"></a>语法

```xml
<entryPoint class>
    <assemblyIdentity />
</entryPoint>
```

## <a name="elements-and-attributes"></a>元素和属性
 `entryPoint` 元素是必需的，它位于 `vstav3` 命名空间中。

 每个 `entryPoint` 元素都只能包含一个自定义程序集。 应用程序清单中可以定义多个 `entryPoint` 元素。

 `entryPoint` 元素具有以下属性。

|属性|说明|
|---------------|-----------------|
|`class`|必需。 标识要执行的自定义程序集。 此属性的语法是 *NamespaceName.ClassName*。|

 `entryPoint` 具有以下元素。

### <a name="assemblyidentity"></a>assemblyIdentity
 必需。 `assemblyIdentity` 命名空间中的 `vstav3` 元素引用 `assemblyIdentity` 应用程序清单中的现有 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 元素。

 `assemblyIdentity`及其特性的角色是在[&#60;assemblyIdentity&#62; 元素 &#40;ClickOnce 应用程序&#41;](../deployment/assemblyidentity-element-clickonce-application.md)中定义的。

## <a name="document-level-customization-example"></a>文档级自定义项示例

### <a name="description"></a>说明
 下面的代码示例演示文档级 Office 解决方案的应用程序清单中的 `entryPoint` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例是[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

### <a name="code"></a>代码

```xml
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
```

## <a name="vsto-add-in-example"></a>VSTO外接程序示例

### <a name="description"></a>说明
 下面的代码示例演示应用程序级 Office 解决方案的应用程序清单中的 `entryPoint` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例是[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

### <a name="code"></a>代码

```xml
<vstav3:entryPoint
  class="ContosoOutlookAddIn.ThisAddIn">
  <assemblyIdentity
    name="ContosoOutlookAddIn"
    version="1.0.0.0"
    language="neutral"
    processorArchitecture="msil" />
</vstav3:entryPoint>
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
