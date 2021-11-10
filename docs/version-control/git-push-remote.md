---
title: 推送到 Visual Studio 中的远程库
titleSuffix: ''
description: 使用 Git 或 Azure DevOps 推送到 Visual Studio 中的远程库。
ms.date: 11/08/2021
ms.topic: how-to
author: TerryGLee
ms.author: tglee
ms.manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: 08aff69e0ced7390b35670a54cf32d004e7232b3
ms.sourcegitcommit: ac681e983f3b217c3fd9d2a31e3a3ddcc4dd3546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2021
ms.locfileid: "132041897"
---
# <a name="push-to-a-remote-in-visual-studio"></a>推送到 Visual Studio 中的远程库

向 GitHub 进行身份验证后，Visual Studio 可改进 GitHub 工作流。 其中一项改进是实现一键单击即可直接推送（也称为发布）本地项目到 GitHub。 简单 Git 工作流中的最后一个阶段是将更改推送到远程。

远程库是一个在云中存储代码的安全位置。 它通常称为“origin/main”（或 origin/master），其中“origin”是远程库的默认名称。 有关此术语的详细信息，请参阅 Git 网站上的 [Git 分支 - 远程分支](https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches)页。

下面介绍如何推送到 Visual Studio 中的远程库。

1. 请确保已打开某个文件，以便在以前[创建](git-create-repository.md)或[克隆](git-clone-repository.md)的存储库中使用。

1. 对文件进行更改，保存它，选择 **Git 更改** 选项卡，然后[提交](git-make-commit.md)该更改。

1. 在“Git 更改”窗口中，请注意包含传入和传出提交数量的链接文本。 在下面的示例中，链接文本读取“1 个传出/0 个传入”。

   :::image type="content" source="media/vs-2022/git-changes-window-outgoing-incoming.png" alt-text="“Git 更改”窗口，其中在 Visual Studio 2022 中突出显示了传出/传入链接文本。":::

   “传出”文本表示尚未推送到远程库的提交数，而“传入”文本表示已提取但尚未从远程库拉取的提交数。

1. 若要推送到远程库，请选择 “推送”按钮，或从“Git”菜单中选择“推送”。

## <a name="next-steps"></a>后续步骤

若要继续此旅程，请访问[在 Visual Studio 中提取、拉取和同步](git-fetch-pull-sync.md)页。

## <a name="see-also"></a>另请参阅

[Visual Studio 中的 Git 体验](git-with-visual-studio.md)
