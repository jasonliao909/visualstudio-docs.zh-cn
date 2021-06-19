---
title: 修饰器的属性
description: 了解修饰器是图标、文本或展开/折叠 V 形，这些 V 形可以显示在关系图上的形状或连接器上。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, decorators
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2f3436bb800142e7c85594f4b05cef6fb45c4489
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390797"
---
# <a name="properties-of-decorators"></a>修饰器的属性
修饰器是图标、文本或展开/折叠 V 形，可以在关系图上的形状或连接器上显示。 下表显示了三种修饰器的属性。 某些属性仅在形状修饰器上显示，或仅在连接器修饰器上显示。

 有关详细信息，请参阅 [How to Define a Domain-Specific Language](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的信息，请参阅自定义和扩展Domain-Specific [语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

## <a name="expandcollapse-decorator"></a>展开/折叠修饰器

|属性|描述|默认|
|-|-|-|
|DisplayName|将在生成的设计器中显示的修饰器的名称。|展开"折叠修饰器"|
|名称|修饰器的名称。|ExpandCollapseDecorator|
|说明|与此修饰器关联的非正式说明。|\<none>|
|HorizontalOffset|相对于修饰器的默认位置的水平偏移量（以英寸为单位）。  (仅适用于形状.) |0|
|VerticalOffset|相对于修饰器的默认位置的垂直偏移量（以英寸为单位）。  (仅适用于形状.) |0|
|OffsetFromLine|修饰器与线条的偏移量（相对于其默认位置）（以英寸为单位）。  (仅在连接器上) |0|
|OffsetFromShape|修饰器与形状的偏移量（相对于其默认位置）（以英寸为单位）。  (仅在连接器上) |0|
|位置|修饰器的默认位置。|SourceTop|

## <a name="icon-decorator"></a>图标修饰器

|属性|描述|默认|
|-|-|-|
|DefaultIcon|要显示的图标或图像文件的路径。|\<none>|
|DisplayName|要显示在生成的设计器中的修饰器的名称。|图标修饰器|
|名称|修饰器的名称。|IconDecorator|
|说明|与修饰器关联的非正式注释。|\<none>|
|HorizontalOffset|相对于修饰器的默认位置的水平偏移量（以英寸为单位）。  (仅适用于形状.) |0|
|VerticalOffset|相对于修饰器的默认位置的垂直偏移量（以英寸为单位）。  (仅适用于形状.) |0|
|OffsetFromLine|修饰器与线条的偏移量（相对于其默认位置）（以英寸为单位）。  (仅在连接器上) |0|
|OffsetFromShape|修饰器与形状的偏移量（相对于其默认位置）（以英寸为单位）。  (仅在连接器上) |0|
|位置|修饰器的默认位置。|SourceTop|

## <a name="textdecorator"></a>TextDecorator

|属性|描述|默认|
|-|-|-|
|DefaultText|要显示的默认文本。|Label|
|DisplayName|要显示在生成的设计器中的修饰器的名称。|Label|
|FontSize|修饰器中显示的文本的字号。|8|
|FontStyle|修饰器中显示的文本的字体样式。|常规|
|名称|修饰器的名称。|Label|
|说明|与修饰器关联的非正式注释。|\<none>|
|HorizontalOffset|相对于修饰器的默认位置的水平偏移量（以英寸为单位）。  (仅适用于形状.) |0|
|VerticalOffset|相对于修饰器的默认位置的垂直偏移量（以英寸为单位）。  (仅适用于形状.) |0|
|OffsetFromLine|从行修饰器的偏移量（以英寸为单位），相对于其默认位置。 仅对连接器 (。 ) |0|
|OffsetFromShape|修饰器相对于其默认位置的偏移量（以英寸为单位）。 仅对连接器 (。 ) |0|
|位置|修饰器的默认位置。|Microsoft.visualstudio.modeling.diagrams.connectordecoratorposition.targetbottom|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))