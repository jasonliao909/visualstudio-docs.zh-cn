---
title: '&lt;RelatedProducts &gt; 元素 (引导程序) |Microsoft Docs'
description: RelatedProducts 元素定义依赖于当前产品或包含在当前产品内的其他产品。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- MSBuild.GenerateBootstrapper.MissingDependency
- MSBuild.GenerateBootstrapper.DuplicateItems
- MSBuild.GenerateBootstrapper.IncludedProductIncluded
- MSBuild.GenerateBootstrapper.DependencyNotFound
- MSBuild.GenerateBootstrapper.PackageFileNotFound
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <RelatedProducts> element [bootstrapper]
ms.assetid: bf152712-4c1e-48bd-9b7f-311cf0fdb832
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: cb217da984fd23acdedc446724984d667e0006bf
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122120746"
---
# <a name="ltrelatedproductsgt-element-bootstrapper"></a>&lt;引导程序 &gt; (RelatedProducts) 
`RelatedProducts`元素定义依赖于当前产品或包含在当前产品中的其他产品。

## <a name="syntax"></a>语法

```xml
<RelatedProducts>
    <DependsOnProduct
        Code
    />
    <EitherProducts>
        <DependsOnProduct
            Code
        />
    </EitherProducts>
    <IncludesProduct
        Code
    />
</RelatedProducts>
```

## <a name="elements-and-attributes"></a>元素和属性
 `RelatedProducts`元素是 元素的 `Product` 子元素。 它没有任何属性。

## <a name="dependsonproduct"></a>DependsOnProduct
 元素表示当前产品依赖于命名产品，并且应在当前产品之前 `DependsOnProduct` 安装命名产品。 它是 元素的 `RelatedProducts` 子元素。 元素 `RelatedProducts` 可能具有一个或多个 `DependsOnProduct` 元素。

 `DependsOnProduct` 具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`Code`|包含的产品的代码名称，由 元素 `ProductCode` 的 属性 `Product` 指定。 有关详细信息，请参阅 [\<Product> 元素](../deployment/product-element-bootstrapper.md)。|

## <a name="eitherproducts"></a>EitherProducts
 `EitherProducts`元素定义零个或多个 `DependsOnProduct` 元素，并且没有属性。 必须在当前 `DependsOnProduct` 产品之前安装此集内至少一个 。 元素 `RelatedProducts` 可以具有零个或多个 `EitherProducts` 元素。

## <a name="includesproduct"></a>IncludesProduct
 `IncludesProduct`元素表示产品包含在当前安装中，不需要单独安装。 它是 元素的 `RelatedProducts` 子元素。 元素 `RelatedProducts` 可能具有一个或多个 `IncludesProduct` 元素。

 `IncludesProduct` 具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`Code`|包含的产品的代码名称，由 元素 `ProductCode` 的 属性 `Product` 指定。 有关详细信息，请参阅 [\<Product> 元素](../deployment/product-element-bootstrapper.md)。|

## <a name="example"></a>示例
 下面的代码示例指定 Microsoft Installer 随 .NET Framework一起安装，因此不需要单独安装。

```xml
<RelatedProducts>
    <IncludesProduct Code="Microsoft.Windows.Installer.2.0" />
</RelatedProducts>
```

## <a name="see-also"></a>请参阅
- [\<Product> 元素](../deployment/product-element-bootstrapper.md)