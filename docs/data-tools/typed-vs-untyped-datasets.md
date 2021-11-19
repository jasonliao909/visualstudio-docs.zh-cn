---
title: 类型化与非类型化数据集
description: 了解类型化和非类型化数据集之间的差异。 对比类型化和非类型化数据集中的数据访问。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: c83ba0bb-5425-4d47-8891-6b4dbf937701
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 3ce12fd272297429ba62c4e947025ada7c350d26
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601071"
---
# <a name="typed-vs-untyped-datasets"></a>类型化与非类型化数据集
类型化数据集是首先从基本 <xref:System.Data.DataSet> 类派生出来的数据集，然后使用存储在 .xsd 文件中的“数据集设计器”中的信息来生成新的强类型化数据集类。 来自架构（表、列等）的信息将被生成并编译到此新的数据集类中，作为一组第一类对象和属性。 因为类型化数据集继承自基类 <xref:System.Data.DataSet>，类型化类假定 <xref:System.Data.DataSet> 类的所有功能，并且可以与以 <xref:System.Data.DataSet> 类的实例作为参数的方法一起使用。

相反，非类型化数据集没有相应的内置架构。 与类型化数据集一样，非类型化数据集包含表、列等，但这些仅作为集合公开。 （但是，在手动创建非类型化数据集中的表和其他数据元素之后，可以使用该数据集的 <xref:System.Data.DataSet.WriteXmlSchema%2A> 方法将数据集的结构导出为架构。）

## <a name="contrast-data-access-in-typed-and-untyped-datasets"></a>对比类型化和非类型化数据集中的数据访问
类型化数据集的类有一个对象模型，其属性采用表和列的实际名称。 例如，如果使用类型化数据集，则可以使用如下所示的代码来引用列：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet4":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet4":::

相反，如果使用非类型化的数据集，则等效的代码为：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet5":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet5":::

类型化访问不仅更易于读取，而且在 Visual Studio 代码编辑器中由 IntelliSense 完全支持。 除了更易于使用以外，类型化的数据集的语法还在编译时提供类型检查，大大降低了向数据集成员赋值时出现错误的可能性。 如果更改 <xref:System.Data.DataSet> 类中的列名，并编译应用程序，则会收到一个生成错误。 通过双击“任务列表”中的生成错误，则可以直接跳到引用旧列名称的一行或几行代码。 在运行时访问类型化数据集中的表和列还会稍微快一些，因为访问是在编译时确定的，而不是在运行时通过集合确定。

尽管类型化数据集有许多优点，但非类型化数据集在各种情况下都很有用。 最明显的情况是数据集没有可用的架构。 例如，如果你的应用程序与返回数据集的组件交互，但事先并不知道它的结构是什么，就可能会发生这种情况。 类似地，有时你使用的数据没有静态的、可预测的结构。 在这种情况下，使用类型化数据集是不切实际的，因为在数据结构中的每次更改都必须重新生成类型化数据集类。

更常见的情况是，很多时候你可能在没有可用模式的情况下动态创建数据集。 在这种情况下，数据集只是一种方便的结构，你可以在其中保存信息，只要数据可以用关系方式表示。 同时，你可以利用数据集的功能，例如将要传递给另一个进程的信息序列化或写出 XML 文件的功能。

## <a name="see-also"></a>另请参阅

- [数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
