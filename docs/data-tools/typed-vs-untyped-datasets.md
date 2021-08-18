---
title: 类型化与非类型化数据集
description: 了解类型化数据集和未类型化数据集的区别。 对比类型化数据集和未类型化数据集中的数据访问。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122036831"
---
# <a name="typed-vs-untyped-datasets"></a>类型化与非类型化数据集
类型数据集是一个数据集，它首先派生自基类，然后使用 <xref:System.Data.DataSet> **数据集设计器（** 存储在 .xsd 文件中）的信息来生成新的强类型数据集类。 架构中 (表、列等的信息作为一组一) 对象和属性生成并编译到此新的数据集类中。 由于类型化数据集继承自基类，因此类型化类假定类的所有功能，并可用于将类的实例作为参数 <xref:System.Data.DataSet> <xref:System.Data.DataSet> <xref:System.Data.DataSet> 的方法。

相反，非类型化数据集没有相应的内置架构。 与在类型化数据集中一样，非类型化数据集包含表、列等，但这些仅作为集合公开。  (但是，在非类型化数据集中手动创建表和其他数据元素后，可以使用数据集的 <xref:System.Data.DataSet.WriteXmlSchema%2A> method.) 

## <a name="contrast-data-access-in-typed-and-untyped-datasets"></a>对类型化数据集和未类型化数据集中的数据访问进行对比
类型数据集的 类具有一个对象模型，其属性用于表和列的实际名称。 例如，如果使用类型数据集，可以使用如下所示的代码引用列：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet4":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet4":::

相反，如果使用非类型化数据集，则等效代码为：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet5":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet5":::

在代码编辑器 中，IntelliSense 不仅更易于阅读，还完全支持Visual Studio **访问**。 除了更易于使用之外，类型数据集的语法还提供编译时的类型检查，大大减少了向数据集成员分配值时出错的可能性。 如果更改类中列的名称，然后编译 <xref:System.Data.DataSet> 应用程序，则会收到生成错误。 通过双击列中的生成 **任务列表，** 可以直接转到引用旧列名的代码行或代码行。 运行时，对类型数据集中的表和列的访问速度也略快一些，因为访问是在编译时确定的，而不是通过运行时的集合确定的。

即使类型化数据集有许多优点，但非类型化数据集在多种情况下都很有用。 最明显的情况是数据集没有可用的架构。 例如，如果应用程序正在与返回数据集的组件交互，但事先不知道其结构是什么，则可能会发生这种情况。 同样，有时处理的数据没有静态的可预测结构。 在这种情况下，使用类型化数据集不切实际，因为必须重新生成类型化数据集类，并且数据结构中每次更改。

更一般地，在许多情况下，你可能会在架构不可用的情况下动态创建数据集。 在这种情况下，数据集只是一种方便的结构，只要数据可以以关系方式表示，就可以在结构中保留信息。 同时，可以利用数据集的功能，例如序列化信息以传递给另一个进程或写出 XML 文件的功能。

## <a name="see-also"></a>请参阅

- [数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
