---
title: 使用 TensorBoard 监视
description: 了解如何使用 Visual Studio 通过 TensorBoard 直观显示模型培训进度。
ms.custom: SEO-VS-2020
author: jillre
ms.author: jillfra
manager: jmartens
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- multiple
ms.openlocfilehash: edb6fe17902ad84ec6d7a6e5b9929bd965e7c29b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99841388"
---
# <a name="monitor-with-tensorboard"></a>使用 TensorBoard 监视

可以使用 TensorBoard 可视化模型培训进度。

1. 右键单击项目，单击“运行 TensorBoard”；然后选择输出 TensorBoard 日志所在的目录。

    ![Visual Studio 解决方案资源管理器的屏幕截图，其中选中了 MNIST 项目。 打开了上下文菜单，并且选中了“Run TensorBoard”命令。](media/monitor-tensorboard/run-tensorboard.png)

2. 可注意到，错误随着时间推移减少，这意味着质量在不断提高。

    ![主 TensorBoard 窗口的屏幕截图，其中显示了 TensorBoard 日志中数据的图形可视化效果。](media/monitor-tensorboard/tensorboard.png)
