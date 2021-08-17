---
title: Bitmap 元素|Microsoft Docs
description: Bitmap 元素定义位图。 位图从资源或文件中加载。 本文包含一个示例。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Bitmaps
- Bitmaps element (VSCT XML schema)
ms.assetid: edcd7891-f4e7-416d-809d-5e2eed9f17e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 1fcf2b2eb60bfb99708d78424eaf4f084aca1c6d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122089766"
---
# <a name="bitmap-element"></a>Bitmap 元素
定义位图。 位图从资源或文件中加载。

## <a name="syntax"></a>语法

```
<Bitmap guid="guidImages" href="images\MyImage.bmp" usedList="bmp1, bmp2, bmp3" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|GUID|必需。 GUID/ID 命令标识符的 GUID。<br /><br /> 位图的 guid 属性不与任何 VSPackage 或其他命令组关联。  它应对于位图定义是唯一的，不应用于任何其他目的。|
|渣 油|GUID/ID 命令标识符的 ID。 resID 或 href 属性是必需的。<br /><br /> resID 属性是一个整数资源 ID，用于确定在命令表合并期间加载的位图条。  加载命令表时，资源 ID 指定的位图会从同一模块的资源加载。|
|usedList|如果存在 resID 属性，则是必需的。 选择位图条中的可用图像。|
|href|位图的路径。 resID 或 href 属性是必需的。<br /><br /> 将搜索包含路径，以查找嵌入在生成的二进制文件中的指示图像文件。  在命令表合并期间，将复制映像，并且无需额外的资源查找或加载。  如果 usedList 属性不存在，则条带中所有图像都可用。 **注意：** 图像可能以多种格式之一提供，其中包括.bmp、.png和 *.gif。* ** **  早期版本的编译器不支持具有 alpha 信息的 32 位位图图像，这些图像具有部分透明度信息。 这些版本的解决方法是使用.png *格式。*|
|条件|可选。 请参阅 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[Bitmaps 元素](../extensibility/bitmaps-element.md)|对位图元素进行分组。|

## <a name="example"></a>示例

```
<Bitmap guid="guidWidgetIcons" href="WidgetToolbarIcons_32.bmp" />
<Bitmap guid="guidWidgetIcons2" resID="IDBMP_WIDGETICONS"
  usedList="1, 2, 3, 4"/>
```

## <a name="see-also"></a>请参阅
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
