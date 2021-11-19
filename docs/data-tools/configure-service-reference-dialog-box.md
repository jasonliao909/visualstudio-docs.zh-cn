---
title: “配置服务引用”对话框
description: 使用 Visual Studio 中的“配置服务引用”对话框来配置 Windows Communication Foundation (WCF) 服务的行为。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- msvse_wcf.dlg.ConfigureServiceReference
helpviewer_keywords:
- WCF services, Configure Service Reference dialog box
- service references [Visual Studio], configuring behavior
- Configure Service Reference dialog box
ms.assetid: 25e4c36b-2db6-4e71-9010-b7068255d09d
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 894583846c5e9a8843fbf9abeaa449b7b548abb2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601208"
---
# <a name="configure-service-reference-dialog-box"></a>“配置服务引用”对话框

通过“配置服务引用”对话框可以配置 Windows Communication Foundation (WCF) 服务的行为。

要访问“配置服务引用”对话框，请右键单击“解决方案资源管理器”中的服务引用，然后选择“配置服务引用”。 还可以通过单击“添加服务引用对话框”中的“高级”按钮来访问该对话框。

## <a name="task-list"></a>任务列表

- 要更改承载 WCF 服务的地址，请在“地址”字段中输入新的地址。

- 要更改 WCF 客户端中类的访问级别，请在“生成的类的访问级别”列表中选择访问级别关键字。

- 要异步调用 WCF 服务方法，请选中“生成异步操作”复选框。

- 要在 WCF 客户端中生成消息约定类型，请选中“始终生成消息约定”复选框。

- 要为 WCF 客户端指定列表集合类型或字典集合类型，请从“集合类型”和“字典集合类型”列表中选择类型。

- 要禁用类型共享，请清除“重新使用引用的程序集中的类型”复选框。 要对引用的程序集的子集启用类型共享，请选中“重新使用引用的程序集中的类型”复选框，接着选中“重新使用所引用的指定程序集中的类型”，然后在“引用的程序集列表”中选择所需的引用。

## <a name="uielement-list"></a>UIElement 列表

**Address**

更新服务引用查找服务的 web 地址。 例如，在开发过程中，服务可能托管在开发服务器上，之后又移到了生产服务器上，因而需要进行地址更改。

> [!NOTE]
> 从“添加服务引用”对话框中显示“配置服务引用”对话框时，“地址”元素不可用。

**生成的类的访问级别**

确定 WCF 客户端类的代码访问级别。

> [!NOTE]
> 对于网站项目，该选项将始终设置为 `Public`，并且无法更改。 有关详细信息，请参阅[服务引用疑难解答](../data-tools/troubleshooting-service-references.md)。

**生成异步操作**

确定 WCF 服务方法是同步调用（默认）还是异步调用。

**生成基于任务的操作**

编写异步代码时，此选项允许你使用随 .Net 4 一起引入的任务并行库 (TPL)。 请参阅[任务并行库 (TPL)](/dotnet/standard/parallel-programming/task-parallel-library-tpl)。

**始终生成消息约定**

确定是否将为 WCF 客户端生成消息协定类型。 有关消息约定的详细信息，请参阅[使用消息约定](/dotnet/framework/wcf/feature-details/using-message-contracts)。

**集合类型**

为 WCF 客户端指定列表集合类型。 默认类型为 <xref:System.Array>。

**字典集合类型**

为 WCF 客户端指定字典集合类型。 默认类型为 <xref:System.Collections.Generic.Dictionary%602>。

**重新使用引用的程序集中的类型**

确定在添加或更新服务时，WCF 客户端是否将设法重用引用的程序集中已经存在的类型，而不是生成新的类型。 默认情况下，此选项处于选中状态。

**重新使用所有引用的程序集中的类型**

如果选择此选项，则会尽可能重用“引用的程序集列表”中的所有类型。 默认情况下选择此选项。

**重新使用所引用的指定程序集中的类型**

如果选择此选项，将只重用“引用的程序集列表”中选定的类型。

**引用的程序集列表**

包含一个列表，此列表针对项目或网站列出了引用的程序集。 如果选择“重新使用所指定的引用的指定程序集中的类型”则可以选择或清除个别程序集。

**添加 Web 引用**

显示“添加 Web 引用”对话框。

> [!NOTE]
> 此选项应仅用于面向 .NET Framework 版本 2.0 的项目。
>
> [!NOTE]
> 仅在从“添加服务引用”对话框中显示“配置服务引用”对话框时，“添加 Web 引用”按钮才可用  。

## <a name="see-also"></a>另请参阅

- [如何：添加对 Web 服务的引用](how-to-add-update-or-remove-a-wcf-data-service-reference.md)
- [Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/configure-service-reference-dialog-box.md)
