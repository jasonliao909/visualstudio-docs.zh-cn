---
title: 工作流设计器 - 如何：使用痕迹导航
description: 了解如何使用痕迹导航访问子活动、导航到上级活动，或就地展开或折叠活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 4a688056-37dc-406a-9071-be2141e192fe
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: b0daeebb7db8ca87ebd225f683b171b56e28822d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664678"
---
# <a name="how-to-use-breadcrumb-navigation"></a>如何：使用痕迹导航

有三种主要方法来更改在活动中显示的活动工作流设计器：

1. 双击以钻入子活动。

2. 单击痕迹栏上的按钮以导航到祖先活动。

3. 就地展开或折叠活动。

## <a name="using-breadcrumb-navigation"></a>使用痕迹导航

1. 双击所单击工作流设计器，将根活动更改为单击的活动。 单击的活动随后在根上完全展开，其上级显示在痕迹导航栏中。 这有时称为钻入或钻出某个活动。

2. 若要导航到当前根活动的一个祖先，请单击痕迹栏中的相应活动。

## <a name="expanding-or-collapsing-an-activity-in-place"></a>就地展开或折叠活动

1. 单击活动上的 V 形将就地展开或折叠该活动。

2. 单击该按钮更改展开状态时，新的展开状态将保存在 XAML 中。

    > [!WARNING]
    > 并非所有活动都可就地展开。 在两种情况下不能就地展开活动：一种是活动的父级不允许其子级就地展开（例如，流程图中的活动不能就地展开），另一种是活动设计器不允许自身就地展开。 尽管所有活动设计器都不包含工作流设计器具有后一行为，但某些自定义活动可能会表现出此行为。

## <a name="expanding-all-or-collapsing-all-activities"></a>展开或折叠所有活动

1. 使用用户界面 **中的****"全部** 展开"和"全部折叠"按钮可展开或折叠当前痕迹根下的所有活动。 请注意，全部展开和全部折叠是全局状态。 这意味着，使用痕迹导航更改根活动时，展开所有或折叠所有状态将一直保留，直到单击"还原 **"。**

2. 应用"全部展开"或"折叠所有状态"后，可以单击显示为返回的"还原"按钮，查看以前应用于每个活动的状态。

    > [!WARNING]
    > 如果活动（如 ）已就地选择退出展开，则流程图设计器上将禁用与"全部展开"和"全部折叠" <xref:System.Activities.Statements.Flowchart> **按钮关联的** 功能。   有关流程图 **设计器的详细信息** ，请参阅 [流程图主题](../workflow-designer/flowchart-activity-designer.md) 。

    > [!WARNING]
    > "全部展开"在 **Switch** 和 **TryCatch 活动设计器中** 也具有特殊效果。 单击" **全部展开"** 时，将显示所有切换事例以及所有 try/catch/finally 块。 单击 **"** 还原 **"** 或"全部折叠"，这些设计器将返回到其默认状态，你可以从该状态单击单个 case/block 以查看其内容。
