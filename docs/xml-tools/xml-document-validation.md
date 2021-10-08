---
title: XML 编辑器中的 XML 文档验证
description: 了解 XML 编辑器中的 XML 文档验证，以及它如何检查 XML 1.0 语法并在你键入内容时执行数据验证。
ms.custom: SEO-VS-2020
ms.date: 09/16/2021
ms.topic: conceptual
ms.assetid: abb353bd-6c4a-4978-b03b-a8c245bbfb55
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-xml-tools
ms.workload:
- multiple
ms.openlocfilehash: 1dc2fcbbac33fe19cd50b44675609f7121c1be69
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128429661"
---
# <a name="xml-document-validation"></a>XML 文档验证

XML 编辑器检查 XML 1.0 语法，还会在你键入内容时执行数据验证。 编辑器可以使用文档类型定义 (DTD) 或架构进行验证。 红色的波浪形下划线突出显示任何 XML 1.0 格式正确的错误。 蓝色的波浪形下划线根据 DTD 或架构验证显示语义错误。 每个错误在错误列表中有关联的条目。 将鼠标光标暂时停留在波浪形下划线上，也可以查看错误消息。

将已编译架构的 `targetNamespace` 与元素的 xmlns 声明进行匹配，可以找到验证中使用的架构。 已编译架构从下列位置之一加载（按优先级顺序列出）：

- 从在文档“属性”窗口的“架构”字段中指定的文件名 。

- 内联架构或 DTD。

- 外部 DTD 或 `xsd:schemaLocation` 和 `xsd:noNamespaceSchemaLocation` 属性

- “x-schema”XDR 架构命名空间 URI。

如果架构具有非空目标命名空间，在下列附加位置也可以找到架构：

- 包含架构的另一个编辑器窗口。

- 当前解决方案中的架构。

- 架构缓存目录中的架构。

## <a name="xslt-files"></a>XSLT 文件
在编辑 XSLT 文件时，使用架构缓存中的 xslt.xsd 文件进行验证。 验证错误以蓝色的波浪形下划线显示。 XSLT 编译器中的错误显示为红色的波浪形下划线。

## <a name="xml-schema-xsd-files"></a>XML 架构 (XSD) 文件
在编辑 XML 架构文件时，使用架构缓存中的 xsdschema.xsd 文件进行验证。 验证错误以蓝色的波浪形下划线显示。 任何编译错误也会显示为红色的波浪形下划线。

## <a name="entity-reference-limit"></a>实体引用限制
DTD 处理默认将实体引用数限制为 10,000 个引用，并可以容纳大多数 XML 架构。  Visual Studio 中的错误消息可能是“已超过文件名的实体引用限制”。

如果在处理 XML 文档时遇到此限制，并且希望将验证程序扩展到更大的架构，可以使用 `MaxNumberOfDtdEntityReferences` Visual Studio 注册表项进行更改。 如需详细了解如何进行此更改，请参阅[为 Visual Studio 实例编辑注册表](../install/tools-for-managing-visual-studio-instances.md#editing-the-registry-for-a-visual-studio-instance)。 请注意，这适用于用户在此计算机上打开的所有 XML 文档。

## <a name="see-also"></a>请参阅

- [XML 编辑器](../xml-tools/xml-editor.md)
