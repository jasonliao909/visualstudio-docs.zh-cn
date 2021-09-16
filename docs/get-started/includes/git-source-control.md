---
ms.date: 08/30/2021
ms.technology: vs-ide-general
ms.custom: vs-get-started
ms.author: tglee
author: TerryGLee
manager: jmartens
ms.topic: include
ms.openlocfilehash: e045d40958e339d497cea8509110618769649182
ms.sourcegitcommit: 559c662b2d60048300b76ea6ed3defaa2a259492
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2021
ms.locfileid: "127832844"
---
::: moniker range=">=vs-2019"

## <a name="add-git-source-control"></a>添加 Git 源代码管理

现在你已经创建了应用，可能需要将它添加到 Git 存储库。 我们已经为你准备好了。 Visual Studio 通过 Git 工具简化了该过程，你可直接从 IDE 中使用这些工具。

> [!TIP]
> Git 是使用最广泛的新式版本控制系统，因此无论你是专业开发人员，还是正在学习如何编码，Git 都非常有用。 如果你是刚刚接触 Git，可访问 [https://git-scm.com/](https://git-scm.com/) 网站开始了解。 在这里，你能找到速查表、畅销在线图书和 Git 基础知识视频。

若要将代码与 Git 关联，需要首先创建一个新的 Git 存储库来容纳代码。 下面介绍如何操作：

1. 在 Visual Studio 右下角的状态栏中，选择“添加到源代码管理”，然后选择“Git” 。

    :::image type="content" source="../media/vs-2022/git-add-source-control.png" alt-text="“解决方案资源管理器”窗格下的 Git 源代码管理按钮的屏幕截图，其中突出显示了“添加到源代码管理”按钮。":::

1. 在“创建 Git 存储库”对话框中，登录到 GitHub。

    :::image type="content" source="../media/vs-2022/git-create-repo.png" alt-text="“创建 Git 存储库”对话框窗口的屏幕截图，可在其中登录到 GitHub。":::

    存储库名称根据你的文件夹位置自动填充。 默认情况下，新存储库是专用的，这意味着只有你可以访问它。

    > [!TIP]
    > 无论存储库是公用的还是专用的，都最好将代码的远程备份安全地存储在 GitHub 上。 即使你不与团队合作，也可使用任意计算机上在远程存储库中访问你的代码。

1. 选择“创建并推送”。

    创建存储库后，状态栏中会显示状态详细信息。

    :::image type="content" source="../media/vs-2022/git-new-private-repo-status-details.png" alt-text="存储库状态栏的屏幕截图，它位于 Visual Studio 的“解决方案资源管理器”窗格下。":::

    带箭头的第一个图标显示当前分支中的传出/传入提交数。 可以使用此图标来拉取任何传入提交或推送任何传出提交。 还可选择先查看这些提交。 为此，请选择图标，然后选择“查看传出/传入”。

    带铅笔的第二个图标显示代码的未提交更改数。 可选择此图标，在“Git 更改”窗口中查看这些更改。

若要详细了解如何在应用中使用 Git，请参阅 [Visual Studio 版本控制文档](../../version-control/index.yml)。

::: moniker-end