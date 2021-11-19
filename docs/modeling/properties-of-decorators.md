---
title: 修饰器的属性
description: 了解修饰器是可以在图表上的形状或连接器上显示的图标、文本或展开/折叠 V 形。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, decorators
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: bfbec75b8190b56900a7a994ac12022af1133ac0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663928"
---
# <a name="properties-of-decorators"></a>修饰器的属性
修饰器是可以在图表上的形状或连接器上显示的图标、文本或展开/折叠 V 形。 下表显示了三种修饰器的属性。 某些属性仅在形状修饰器上显示，或仅在连接器修饰器上显示。

 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

## <a name="expandcollapse-decorator"></a>展开/折叠修饰器

|属性|说明|默认|
|-|-|-|
|DisplayName|将在生成的设计器中显示的修饰器的名称。|展开折叠修饰器|
|名称|修饰器的名称。|ExpandCollapseDecorator|
|备注|与此修饰器相关联的非正式说明。|\<none>|
|HorizontalOffset|相对于修饰器默认位置的水平偏移（以英寸为单位）。 （仅在形状上。）|0|
|VerticalOffset|相对于修饰器默认位置的垂直偏移（以英寸为单位）。 （仅在形状上。）|0|
|OffsetFromLine|修饰器从该行相对于其默认位置的偏移（以英寸为单位）。 （仅在连接器上。）|0|
|OffsetFromShape|修饰器从该形状相对于其默认位置的偏移（以英寸为单位）。 （仅在连接器上。）|0|
|位置|修饰器的默认位置。|SourceTop|

## <a name="icon-decorator"></a>图标修饰器

|属性|说明|默认|
|-|-|-|
|DefaultIcon|要显示的图标或图像文件的路径。|\<none>|
|DisplayName|将在生成的设计器中显示的修饰器的名称。|图标修饰器|
|名称|修饰器的名称。|IconDecorator|
|备注|与此修饰器相关联的非正式说明。|\<none>|
|HorizontalOffset|相对于修饰器默认位置的水平偏移（以英寸为单位）。 （仅在形状上。）|0|
|VerticalOffset|相对于修饰器默认位置的垂直偏移（以英寸为单位）。 （仅在形状上。）|0|
|OffsetFromLine|修饰器从该行相对于其默认位置的偏移（以英寸为单位）。 （仅在连接器上。）|0|
|OffsetFromShape|修饰器从该形状相对于其默认位置的偏移（以英寸为单位）。 （仅在连接器上。）|0|
|位置|修饰器的默认位置。|SourceTop|

## <a name="textdecorator"></a>TextDecorator

|属性|说明|默认|
|-|-|-|
|DefaultText|要显示的默认文本。|标签|
|DisplayName|将在生成的设计器中显示的修饰器的名称。|标签|
|FontSize|修饰器中所显示文本的字体大小。|8|
|FontStyle|修饰器中所显示文本的字体样式。|定期|
|名称|修饰器的名称。|标签|
|备注|与此修饰器相关联的非正式说明。|\<none>|
|HorizontalOffset|相对于修饰器默认位置的水平偏移（以英寸为单位）。 （仅在形状上。）|0|
|VerticalOffset|相对于修饰器默认位置的垂直偏移（以英寸为单位）。 （仅在形状上。）|0|
|OffsetFromLine|修饰器从该行相对于其默认位置的偏移（以英寸为单位）。 （仅在连接器上。）|0|
|OffsetFromShape|修饰器从该形状相对于其默认位置的偏移（以英寸为单位）。 （仅在连接器上。）|0|
|位置|修饰器的默认位置。|TargetBottom|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))