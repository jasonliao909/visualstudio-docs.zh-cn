---
title: VSIX 颜色编译器|Microsoft Docs
description: 了解扩展Visual Studio编译器工具，该工具是一个控制台应用程序，用于将主题Visual Studio中的颜色覆盖到 .pkgdef 文件中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 99395da7-ec34-491d-9baa-0590d23283ce
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 1c724dae82bb8f7f05c83c96d1c331d72eac0abd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600843"
---
# <a name="vsix-color-compiler"></a>VSIX 颜色编译器
Visual Studio扩展颜色编译器工具是一个控制台应用程序，它采用表示现有 Visual Studio 主题颜色的 .xml 文件，并覆盖它到 .pkgdef 文件，以便可以在 Visual Studio 中Visual Studio。 由于比较不同文件之间的差异.xml，此工具可用于管理源代码管理中的自定义颜色。 还可以将该文件挂钩到生成环境中，以便生成的输出是有效的 .pkgdef 文件。

 **主题 XML 架构**

 文件的完整.xml如下所示：

```xml
<Themes>
      <!—one or Theme elements -->
      <Theme>
        <!-- one or more Category elements -->
        <Category>
          <!-- one or more Color elements -->
          <Color>
            <!-- zero or one Background element -->
            <Background />
            <!-- zero or one Foreground element -->
            <Foreground />
          </Color>
        </Category>
      </Theme>
</Themes>
```

 **主题**

 \<Theme>元素定义整个主题。 主题必须至少包含一 \<Category> 个元素。 主题元素的定义如下所示：

```xml
<Theme Name="name" GUID="guid">
      <!-- one or more Category elements -->
</Theme>
```

|**Attribute**|**定义**|
|-|-|
|名称|[必需]主题的名称|
|GUID|[必需]主题的 GUID (必须与 GUID 格式设置) |

 为主题创建自定义颜色Visual Studio，需要为以下主题定义这些颜色。 如果特定主题不存在颜色，则Visual Studio浅色主题中加载缺失的颜色。

|**主题名称**|**主题 GUID**|
|-|-|
|亮|{de3dbbcd-f642-433c-8353-8f1df4370aba}|
|暗|{1ded0138-47ce-435e-84ef-9ec1f439b749}|
|蓝色|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|
|高对比度|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|

 **类别**

 \<Category>元素定义主题中的颜色集合。 类别名称提供逻辑分组，应尽量缩小定义范围。 类别必须至少包含一 \<Color> 个元素。 类别元素的定义如下：

```xml
<Category Name="name" GUID="guid">
      <!-- one or more Color elements -->
 </Category>
```

|**Attribute**|**定义**|
|-|-|
|名称|[必需]类别的名称|
|GUID|[必需]类别的 GUID (必须与 GUID 格式设置) |

 **颜色**

 \<Color>元素定义 UI 的组件或状态的颜色。 颜色的首选命名方案是 [UI 类型] [状态]。 请勿使用单词"color"，因为它是冗余的。 颜色应清楚地指示要应用颜色的元素类型和情况或"状态"。 颜色不得为空，并且必须包含 和 元素的一个或两 \<Background> \<Foreground> 个。 颜色元素的定义如下所示：

```xml
<Color Name="name">
        <Background /> <!-- zero or one Background element -->
        <Foreground /> <!-- zero or one Foreground element -->
 </Color>
```

|**Attribute**|**定义**|
|-|-|
|名称|[必需]颜色的名称|

 **背景和/或前景**

 和 元素定义 UI 元素的背景或前景 \<Background> \<Foreground> 的颜色值和类型。 这些元素没有子元素。

```xml
<Background Type="type" Source="int" />
<Foreground Type="type" Source="int" />
```

|**Attribute**|**定义**|
|-|-|
|类型|[必需]颜色的类型。 该参数可以是下列值之一：<br /><br /> *CT_INVALID：* 颜色无效或未设置。<br /><br /> *CT_RAW：* 原始 ARGB 值。<br /><br /> *CT_COLORINDEX：* 请勿使用。<br /><br /> *CT_SYSCOLOR：* SysColor Windows系统颜色。<br /><br /> *CT_VSCOLOR：* 一Visual Studio颜色__VSSYSCOLOREX。<br /><br /> *CT_AUTOMATIC：* 自动颜色。<br /><br /> *CT_TRACK_FOREGROUND：* 请勿使用。<br /><br /> *CT_TRACK_BACKGROUND：* 请勿使用。|
|源|[必需]以十六进制表示的颜色的值|

 Type 属性中的架构支持__VSCOLORTYPE枚举支持的所有值。 但是，我们建议你仅使用 CT_RAW CT_SYSCOLOR。

 **一起**

 这是有效主题文件的简单.xml示例：

```xml
<Themes>
  <Theme Name="Light" GUID="{de3dbbcd-f642-433c-8353-8f1df4370aba}">
    <Category Name="MyCategory" GUID="{0A96238B-70CE-4479-9170-EECEAA3FCD58}">
      <Color Name="MyActiveBorder">
        <Background Type="CT_RAW" Source="FFCCCEDB" />
      </Color>
    </Category>
  </Theme>
</Themes>
```

## <a name="how-to-use-the-tool"></a>如何使用工具
 **语法**

 VsixColorCompiler \<XML file> \<PkgDef file>\<Optional Args>

 **参数**

|**交换机名称**|**说明**|**必需或可选**|
|-|-|-|
|未命名 (.xml文件) |这是第一个未命名的参数，是要转换的 XML 文件的路径。|必需|
|未命名 (.pkgdef) |这是第二个未命名的参数，是生成的 .pkgdef 文件的输出路径。<br /><br /> 默认值 \<XML Filename> ：.pkgdef|可选|
|/noLogo|设置此标志会阻止打印产品和版权信息。|可选|
|/?|打印出"帮助信息"。|可选|
|/help|打印出"帮助信息"。|可选|

 **示例**

- VsixColorCompiler D:\xml\colors.xml D：\pkgdef\colors.pkgdef

- VsixColorCompiler D:\xml\colors.xml /noLogo

## <a name="notes"></a>说明

- 此工具需要安装最新版本的 VC++ 运行时。

- 仅支持单个文件。 不支持通过文件夹路径进行的大容量转换。

- 可在中找到该工具 `<VS Install Path>\VSSDK\VisualStudioIntegration\Tools\Bin\`

## <a name="sample-output"></a>示例输出
 该工具生成的 .pkgdef 文件将类似于以下项：

```
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\Environment]
"Data"=hex:3a,00,00,00,0b,00,00,00,01,00,00,00,c3,d9,4e,62,fd,bd,fa,41,96,c3,7c,82,4e,a3,2e,3d,01,00,00,00,0c,00,00,00,41,63,74,69,76,65,42,6f,72,64,65,72,01,cc,ce,db,ff,01,33,31,24,ff

[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\TreeView]
"Data"=hex:38,00,00,00,0b,00,00,00,01,00,00,00,8e,f0,ec,92,13,8b,f4,4c,99,e9,ae,26,92,38,21,85,01,00,00,00,0a,00,00,00,42,61,63,6b,67,72,6f,75,6e,64,01,f5,f5,f5,ff,01,1e,1e,1e,ff
```
