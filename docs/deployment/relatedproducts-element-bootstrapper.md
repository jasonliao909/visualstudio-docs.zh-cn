---
title: '&lt;RelatedProducts&gt; 元素（引导程序）| Microsoft Docs'
description: RelatedProducts 元素定义依赖于当前产品或包含在当前产品中的其他产品。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601004"
---
# <a name="ltrelatedproductsgt-element-bootstrapper"></a>&lt;RelatedProducts&gt; 元素（引导程序）
`RelatedProducts` 元素定义依赖于当前产品或包含在当前产品中的其他产品。

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
 `RelatedProducts` 元素是 `Product` 元素的一个子元素。 它没有属性。

## <a name="dependsonproduct"></a>DependsOnProduct
 `DependsOnProduct` 元素指示当前产品依赖于命名产品，并且命名产品应该在当前产品之前安装。 它是 `RelatedProducts` 元素的子元素。 一个 `RelatedProducts` 元素可能包含一个或多个 `DependsOnProduct` 元素。

 `DependsOnProduct` 具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Code`|包含的产品的代码名称，由 `Product` 元素的 `ProductCode` 属性指定。 有关详细信息，请参阅 [\<Product> 元素](../deployment/product-element-bootstrapper.md)。|

## <a name="eitherproducts"></a>EitherProducts
 `EitherProducts` 元素定义零个或多个 `DependsOnProduct` 元素，并且没有属性。 在安装当前产品之前，必须至少安装此集中的一个 `DependsOnProduct`。 一个 `RelatedProducts` 元素可以包含零个或多个 `EitherProducts` 元素。

## <a name="includesproduct"></a>IncludesProduct
 `IncludesProduct` 元素指示产品包含在当前安装中，无需单独安装。 它是 `RelatedProducts` 元素的子元素。 一个 `RelatedProducts` 元素可能包含一个或多个 `IncludesProduct` 元素。

 `IncludesProduct` 具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Code`|包含的产品的代码名称，由 `Product` 元素的 `ProductCode` 属性指定。 有关详细信息，请参阅 [\<Product> 元素](../deployment/product-element-bootstrapper.md)。|

## <a name="example"></a>示例
 下面的代码示例指定 Microsoft 安装程序与 .NET Framework 一起安装，因此不需要单独安装。

```xml
<RelatedProducts>
    <IncludesProduct Code="Microsoft.Windows.Installer.2.0" />
</RelatedProducts>
```

## <a name="see-also"></a>另请参阅
- [\<Product> 元素](../deployment/product-element-bootstrapper.md)