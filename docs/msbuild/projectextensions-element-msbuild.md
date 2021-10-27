---
title: ProjectExtensions 元素 (MSBuild) | Microsoft Docs
description: 了解 MSBuildProjectExtensions 元素，它允许 MSBuild 项目文件包含非 MSBuild 信息。
ms.custom: SEO-VS-2020
ms.date: 03/13/2017
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ProjectExtensions
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <ProjectExtensions> element [MSBuild]
- ProjectExtensions element [MSBuild]
ms.assetid: f95f312f-ff92-41eb-9469-ad99e236a307
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 0fbf7760af7275172bc57ce0aac097e70182b4f5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640601"
---
# <a name="projectextensions-element-msbuild"></a>ProjectExtensions 元素 (MSBuild)

允许 MSBuild 项目文件包含非 MSBuild 信息。 `ProjectExtensions` 元素中的所有内容都将被 MSBuild 忽略。

 \<Project> \<ProjectExtensions>

## <a name="syntax"></a>语法

```xml
<ProjectExtensions>
    Non-MSBuild information to include in file.
</ProjectExtensions>
```

## <a name="attributes-and-elements"></a>特性和元素

 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

 无

### <a name="child-elements"></a>子元素

 无

### <a name="parent-elements"></a>父元素

| 元素 | 描述 |
| - | - |
| [Project](../msbuild/project-element-msbuild.md) | MSBuild 项目文件必需的根元素。 |

## <a name="remarks"></a>备注

 MSBuild 项目中可能只会用到一个 `ProjectExtensions` 元素。

## <a name="example"></a>示例

 以下示例显示了存储在 `ProjectExtensions` 元素中的集成开发环境的信息。

```xml
<ProjectExtensions>
    <VSIDE>
        <External>
            <!--
            Raw XML passed to the IDE by an external source
            -->
        </External>
    </VSIDE>
</ProjectExtensions>
```

## <a name="see-also"></a>请参阅

- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
- [MSBuild](../msbuild/msbuild.md)
