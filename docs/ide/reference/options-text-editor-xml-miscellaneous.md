---
title: 选项, 文本编辑器, XML, 杂项
description: 了解如何使用 XAML 部分中的“杂项”页面来更改 XML 编辑器的自动完成和架构设置。
ms.custom: SEO-VS-2020
ms.date: 10/29/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Miscellaneous
ms.assetid: b6538cbe-badd-4313-a1fb-39e906736bbe
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.openlocfilehash: 8874a6ee31dd00662544e710d28f5d0e53491425
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122048838"
---
# <a name="options-text-editor-xml-miscellaneous"></a>选项, 文本编辑器, XML, 杂项

使用“杂项”选项页更改 XML 编辑器的自动完成和架构设置。 要访问杂项 XML 选项，请选择“工具” > “选项” > “文本编辑器” > “XML”，然后选择“杂项”    。

## <a name="auto-insert"></a>自动插入

**结束标记**

创作 XML 元素时，文本编辑器将添加结束标记。 如果选择了元素开始标记，该编辑器将插入匹配的关闭标记，包括匹配的命名空间前缀。 默认情况下，此复选框为选中状态。

**特性引号**

在创作 XML 属性时，编辑器会插入 `="` 和 `"` 字符并将插入符号 (^) 置于引号之间。 默认情况下，此复选框为选中状态。

**命名空间声明**

文本编辑器将在需要的位置自动插入命名空间声明。 默认情况下，此复选框为选中状态。

**其他标记(注释，CDATA)**

注释、CDATA、DOCTYPE、处理指令和其他标记是自动完成的。 默认情况下，此复选框为选中状态。

## <a name="network"></a>网络

**自动下载 DTD 和架构**

架构和文档类型定义 (DTD) 是从 HTTP 位置上自动下载的。 此功能使用了启用自动代理服务器检测功能的 System.Net。 默认情况下，此复选框为选中状态。

## <a name="outlining"></a>大纲显示

**打开文件时进入大纲模式**

打开文件时，将启用大纲显示功能。 默认情况下，此复选框为选中状态。

## <a name="caching"></a>缓存

**架构**

指定架构缓存的位置。 “浏览”按钮在新窗口中打开当前架构的缓存位置。 默认位置为 %VsInstallDir%\xml\Schemas。

## <a name="see-also"></a>请参阅

- [XML 选项 - 格式设置](options-text-editor-xml-formatting.md)
- [Visual Studio 中的 XML 工具](../../xml-tools/xml-tools-in-visual-studio.md)
