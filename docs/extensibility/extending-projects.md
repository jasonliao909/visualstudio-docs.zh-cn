---
title: 扩展项目 |Microsoft Docs
description: 了解如何在 Visual Studio SDK 中创建自己的自定义项目类型，以及如何管理不同类型的 Visual Studio 解决方案。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- projects [Visual Studio]
ms.assetid: 096d273d-4fe9-4f24-9b00-470bfbdf4bdf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a6d7d93f4cd805db5bd161517c0af9a862457edb47aff912e6eab0afa7de0dbf
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448346"
---
# <a name="extend-projects"></a>扩展项目
项目和解决方案是 Visual Studio 将代码和资源文件组织成编译和部署单元的方法。 可以在[ (Visual Studio SDK) 的项目](../extensibility/extending-projects.md)中找到有关项目的详细信息。

 你可以创建自己 Visual Studio 的项目类型和项目的托管包框架，你可以在项目的[托管包框架](https://github.com/tunnelvisionlabs/MPFProj10)中下载这些项目类型。 若要了解如何实现自定义项目，请参阅[新项目生成：在](../extensibility/internals/new-project-generation-under-the-hood-part-one.md)幕后，第二部分是[生成新项目：](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)

 本节中的主题介绍如何创建自定义项目，以及如何管理不同类型的 Visual Studio 解决方案。

## <a name="in-this-section"></a>本节内容
- [创建基本项目系统，第1部分](../extensibility/creating-a-basic-project-system-part-1.md) 描述如何创建自定义项目系统。

- [创建基本项目系统，第2部分](../extensibility/creating-a-basic-project-system-part-2.md) 描述如何创建自定义项目系统。

- [在项目文件中保存数据](../extensibility/saving-data-in-project-files.md) 说明如何将添加到项目 (<em>。</em>proj * ) 文件。

- [在运行时验证项目的子类型](../extensibility/verifying-subtypes-of-a-project-at-run-time.md) 说明如何在运行时验证项目的子类型。

- [添加和删除属性页](../extensibility/adding-and-removing-property-pages.md) 说明如何为自定义项目自定义属性页。

- [向项目项添加特性](../extensibility/adding-an-attribute-to-a-project-item.md) 说明如何将属性添加到自定义项目项。

- [保留项目项的属性](../extensibility/persisting-the-property-of-a-project-item.md) 说明如何保存自定义项目项的属性。

- [管理通用 Windows 项目](../extensibility/managing-universal-windows-projects.md)介绍如何管理通用项目。
