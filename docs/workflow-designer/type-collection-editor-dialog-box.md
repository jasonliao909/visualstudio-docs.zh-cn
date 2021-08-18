---
title: 工作流设计器 - "类型集合编辑器"对话框
description: 了解如何使用"类型集合编辑器"对话框将已知类型添加到"发送和接收"活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- TypeCollectionEditor.UI
ms.assetid: 63cdea6b-bca2-4c06-b8b4-c8faabd40726
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 9178601dad13630f0e830fe14766ec91d08fb380d7006214a60f79fef1014379
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121365817"
---
# <a name="type-collection-editor-dialog-box"></a>“类型集合编辑器”对话框

"**类型集合编辑器**"对话框用于向"发送和接收"活动 **添加已知** 类型。  此对话框还用于向 **InvokeMethod** 活动添加泛型类型参数。 当用于"**发送和接收"** 活动以添加已知类型时 **，"类型** 集合编辑器"对话框要求类型添加项是唯一的。 如果添加重复类型，并且通过单击"确定"提交更改，则返回错误消息。 当用于 **InvokeMethod** 活动以添加泛型类型参数时，"类型集合编辑器"对话框允许添加重复类型。 

有关详细信息，请参阅数据 [协定已知类型](/dotnet/framework/wcf/feature-details/data-contract-known-types)。

下表描述了"类型集合" (UI) 元素 **的** 用户界面。

|UI 元素|说明|
|-|-----------------|
|**Type List**|已添加或移除的类型的列表。|

## <a name="to-bring-up-the-type-collection-editor-for-the-send-and-receive-activities"></a>为 Send 和 Receive 活动打开“类型集合编辑器”

1. 在设计 **视图中****选择"发送**"或"接收"活动。

2. 按 **F4** 打开"属性 **"** 窗口。

3. 在" **属性** "窗口中，单击 **KnownTypes 属性旁边的省略号** 按钮。

## <a name="to-bring-up-the-type-collection-editor-for-the-invokemethod-activity"></a>为 InvokeMethod 活动打开“类型集合编辑器”

1. 在设计 **视图中选择 InvokeMethod** 活动。

2. 按 **F4** 打开"属性 **"** 窗口。

3. 在" **属性** "窗口中，单击 **GenericTypeArguments** 属性旁边的省略号按钮。
