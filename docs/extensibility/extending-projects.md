---
title: 扩展项目|Microsoft Docs
description: 了解如何在 Visual Studio SDK 中创建自己的自定义项目类型，以及如何管理不同类型的Visual Studio解决方案。
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
ms.openlocfilehash: 429c408fb54d77e9eb8705302f24880e27e84080
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122159355"
---
# <a name="extend-projects"></a>扩展项目
项目和解决方案是将代码Visual Studio文件组织到编译和部署单元中的方法。 可以在 PROJECTs (Visual Studio SDK) [中查找有关项目) 。 ](../extensibility/extending-projects.md)

 可以使用适用于项目的 Visual Studio SDK 和托管包框架创建自己的项目类型，可在项目的托管包[框架下载这些类型](https://github.com/tunnelvisionlabs/MPFProj10)。 若要了解如何实现自定义项目，请参阅新建项目生成[](../extensibility/internals/new-project-generation-under-the-hood-part-one.md)：底层第一部分和新项目生成：在底层，第[二部分](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)。

 本节中的主题介绍如何创建自定义项目以及如何管理不同类型的Visual Studio解决方案。

## <a name="in-this-section"></a>本节内容
- [创建基本项目系统，第 1 部分](../extensibility/creating-a-basic-project-system-part-1.md) 介绍如何创建自定义项目系统。

- [创建基本项目系统，第 2 部分](../extensibility/creating-a-basic-project-system-part-2.md) 介绍如何创建自定义项目系统。

- [将数据保存在项目文件中](../extensibility/saving-data-in-project-files.md) 说明如何将 添加到项目 <em> (。</em>proj*) 文件。

- [运行时验证项目的子类型](../extensibility/verifying-subtypes-of-a-project-at-run-time.md) 说明如何运行时验证项目的子类型。

- [添加和删除属性页](../extensibility/adding-and-removing-property-pages.md) 说明如何自定义自定义项目的属性页。

- [向项目项添加属性](../extensibility/adding-an-attribute-to-a-project-item.md) 说明如何将属性添加到自定义项目项。

- [保留项目项的 属性](../extensibility/persisting-the-property-of-a-project-item.md) 说明如何保留自定义项目项的属性。

- [管理通用Windows项目](../extensibility/managing-universal-windows-projects.md)说明如何管理通用项目。
