---
title: 模板策略和"属性"窗口|Microsoft Docs
description: 了解如何使用模板策略设置属性的默认值、隐藏属性以及添加属性窗口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, template policy
ms.assetid: 1d8019d3-5e57-47ba-b358-526b0796a63b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 84f08740ac47701506f37e3e3aababa329f1ef61
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122158796"
---
# <a name="template-policy-and-the-properties-window"></a>模板策略和属性窗口
当项目包含在企业模板项目中时，该企业模板项目可以强制实施策略。 模板策略成为约束系统，可用于设置属性的默认值、隐藏属性、添加属性等。

 使用模板策略控制"属性"窗口中 **信息的显示不同于** 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> 。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> 在组件级别处理对象属性，而模板策略可用于在解决方案或项目级别约束对象属性。 换句话说

- 在 上实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> 方法，以确定特定对象的" **属性"** 窗口中显示的内容

- 在解决方案和项目级别使用模板策略来确定以前指定的对象的"属性"窗口中显示的内容

  在 解决方案资源管理器 中选择了指定类型的项目 **项时**，使用模板策略在"属性"窗口中有选择地约束特定属性，这对处理项目的开发团队的所有成员都有利。  例如，使用模板策略，可以在数据库中为开发人员设置所有连接字符串信息，使连接字符串为只读。 这样，就可以提供一种简单的方式来确保每个开发人员都使用正确的数据访问路径。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>
- [扩展属性](../../extensibility/internals/extending-properties.md)
