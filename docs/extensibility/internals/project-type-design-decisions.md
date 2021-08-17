---
title: Project类型设计决策|Microsoft Docs
description: 了解通过创建新项目类型扩展项目之前要做出的项目、项目文件持久性和承诺Visual Studio设计决策。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, project file persistence
- project types, commitment mechanics
- project types, items
- project types, design decisions
ms.assetid: f68671fe-fd7a-4e56-a0b5-330b0f1fedb1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 07559518e0873d2392b35594cc5fbff6f7de0c32d1a8810895a8e348da83f4f5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401409"
---
# <a name="project-type-design-decisions"></a>项目类型设计决策
创建新项目类型之前，必须对项目类型做出多个设计决策。 必须确定项目将包含的项目类型、项目文件的持久化方式以及将使用的承诺模型。

## <a name="project-items"></a>项目项
 项目是使用文件或抽象对象吗？ 如果使用文件，这些文件是基于引用还是基于目录的文件？ 文件或抽象对象是本地对象还是远程对象？

 项目中的项可以是文件，也可以是更抽象的对象，例如数据库存储库中的对象或 Internet 上的数据连接。 如果项是文件，则项目可以是基于引用的项目，也可以是基于目录的项目。

 在基于引用的项目中，项可以出现在多个项目中。 但是，项表示的实际文件仅位于一个目录中。 在基于目录的项目中，所有项目项都存在于目录结构中。

 本地项存储在安装应用程序的同一计算机上。 远程项可以存储在本地网络或 Internet 上其他位置的单独服务器上。

## <a name="project-file-persistence"></a>Project文件持久性
 数据是存储在公共平面文件系统中，还是存储在结构化存储中？ 文件是使用标准编辑器还是项目特定的编辑器打开？

 为了保留其数据，大多数应用程序将其数据保存在文件中，然后在用户必须查看或更改信息时重新读取数据。

 结构化存储（也称为复合文件）通常用于多个组件对象模型 (COM) 对象需要将持久数据存储在单个文件中。 借助结构化存储，多个不同的软件组件可以共享单个磁盘文件。

 对于项目中的项的持久性，有几个选项需要考虑。 可以执行以下任一选项：

- 更改后，单独保存每个文件。

- 在单个保存操作中捕获 **多个** 事务。

- 在本地保存文件，然后发布到服务器，或当项表示与远程对象的数据连接时，使用另一种方法保存项目项。

  有关持久性详细信息，[请参阅暂留](../../extensibility/internals/project-persistence.md)Project打开和保存Project[项](../../extensibility/internals/opening-and-saving-project-items.md)。

## <a name="project-commitment-model"></a>Project承诺模型
 持久化数据对象是直接模式还是事务处理模式打开？

 在直接模式下打开数据对象时，立即合并对数据所做的更改，或当用户手动保存文件时。

 使用事务处理模式打开数据对象时，更改将保存到内存中的临时位置，在用户手动选择保存文件之前不会提交。 此时，所有更改必须一起发生，否则不会进行更改。

## <a name="see-also"></a>请参阅
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)
- [项目持久性](../../extensibility/internals/project-persistence.md)
- [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)
- [项目模型核心组件](../../extensibility/internals/project-model-core-components.md)
- [创建项目类型](../../extensibility/internals/creating-project-types.md)
