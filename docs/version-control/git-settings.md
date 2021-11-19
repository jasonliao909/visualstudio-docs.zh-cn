---
title: Visual Studio 中的 Git 设置
titleSuffix: ''
description: 了解 Visual Studio 如何使用 .gitconfig 文件和 Git 设置来管理首选项
ms.date: 06/08/2021
ms.topic: conceptual
ms.author: prnadago
author: prnadago
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.manager: jmartens
monikerRange: '>=vs-2019'
ms.openlocfilehash: f8dd9781833706a73b82a71236d42cc71c9fb9ec
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833085"
---
# <a name="git-settings-and-preferences-in-visual-studio"></a>Visual Studio 中的 Git 设置和首选项

在 Visual Studio 中，你可以配置和查看常见的 Git 设置和首选项，例如你的姓名和电子邮件地址、你的首选差异和合并工具等。 可以在 " **git 全局设置**" 页上的 "**选项" 对话框** 中查看和配置这些设置和首选项 (应用于所有存储库) 或 **Git 存储库设置**"页 (适用于当前存储库) 。

你可以配置两种类型的设置：

- [Git 设置](#git-settings) -此部分中的设置对应于 git 配置文件中保存的 git 设置。 可以在 Visual Studio 中查看和修改这些设置，但这些设置由 Git 配置文件管理。
- [Visual Studio 设置](#visual-studio-settings)-本部分中的设置配置 Visual Studio 管理的 Git 相关设置和首选项。

## <a name="how-to-configure-settings"></a>如何配置设置

1. 若要在 Visual Studio 中配置 Git 设置，请从顶级 Git 菜单中选择 "**设置**"。

   :::image type="content" source="media/git-menu-settings.png" alt-text="带有标注的 Git 菜单设置命令。":::

2. 选择 " **git 全局设置** 或 **git 存储库设置** 以查看和配置全局级别或存储库级别设置。

   :::image type="content" source="media/source-control-settings.png" alt-text="&quot;选项&quot; 对话框的 &quot;导航&quot; 窗格中的 &quot;标注到 Git&quot; 设置。":::

3. 你可以配置几个常见的 Git 设置，如本文的以下各节所述。 配置所需的设置后，请选择 **"确定"** 以保存更新的设置。

   :::image type="content" source="media/ok-button.png" alt-text="带标注到 &quot;确定&quot; 按钮的 &quot;选项&quot; 对话框的显示区域。":::

## <a name="git-settings"></a>Git 设置

你还可以配置和检查某些最常见的 Git 配置设置。 可以在 Visual Studio 中查看和修改以下设置，即使这些设置由 Git 配置文件管理。

- [姓名和电子邮件](#name-and-email)
- [提取期间修剪远程分支](#prune-remote-branches-during-fetch)
- [拉取时，本地分支变基](#rebase-local-branch-when-pulling)
- [加密网络提供程序](#cryptographic-network-provider)
- [凭据帮助器](#credential-helper)
- [& 合并工具的差异](#diff--merge-tools)
- [Git 文件](#git-files)
- [远程](#remotes)
- [其他设置](#other-settings)

>[!NOTE]
>Visual Studio 的 **全局设置** 中配置的 git 设置对应于 Git 的用户特定配置文件中的设置，并且 **存储设置库** 中的设置对应于存储库特定的配置文件中的设置。 有关 Git 配置的详细信息，请参阅关于[自定义 git 的 Pro git](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)、 [git-config 文档](https://git-scm.com/docs/git-config)和[配置文件上的 Pro git 引用](https://git-scm.com/docs/git-config#FILES)。 若要配置未在 Visual Studio 公开的 Git 设置，请使用 `git config` 命令将值写入配置文件： `git config [--local|--global|--system] section.key value` 。

### <a name="name-and-email"></a>姓名和电子邮件

您提供的名称和电子邮件将用作您进行的任何提交的提交者信息。 此设置在全局和存储库范围内可用，并对应于 `git config` [user.name](https://git-scm.com/docs/git-config#Documentation/git-config.txt-username) 和 [user.email](https://git-scm.com/docs/git-config#Documentation/git-config.txt-useremail) 设置。

1. 从 Git 菜单中转到 **设置**。 若要在全局级别设置你的用户名和电子邮件，请参阅 **Git global 设置**;若要在存储库级别设置你的用户名和电子邮件，请参阅 **Git 存储库设置**。

2. 提供你的用户名和电子邮件，然后选择 **"确定"** 保存。 

   :::image type="content" source="media/user-email-setting.png" alt-text="&quot;选项&quot; 对话框中的 &quot;Git 全局设置&quot; 窗格，带有用于用户名电子邮件的标注。":::

### <a name="prune-remote-branches-during-fetch"></a>提取期间修剪远程分支

删除功能将删除远程跟踪分支，这些分支不再存在于远程，并可帮助你保持你的分支列表整洁并保持最新状态。 此设置可在全局范围和存储库范围内使用，并且对应于 `git config` [fetch](https://git-scm.com/docs/git-config#Documentation/git-config.txt-fetchprune) 设置。

建议在全局级别将此选项设置为 **True** 。 有效的设置如下所示：

- 建议 (为 True) 
- 错误
- 取消设置 (默认值) 

1. 从 Git 菜单中转到 **设置**。 请参阅 **Git global 设置** 在全局级别配置此选项;请参阅 **Git 存储库设置**，在存储库级别配置此选项。

2. **在提取过程中将 "修剪远程分支**" 设置为 " **True** (建议) "。 选择 **"确定"** 保存。

:::image type="content" source="media/prune-setting.png" alt-text="屏幕截图，显示 &quot;提取时修剪远程分支&quot;，并从下拉选项中选择 &quot;True&quot;。":::    

### <a name="rebase-local-branch-when-pulling"></a>拉取时，本地分支变基

变基设置不在上游分支中的当前分支中的提交所做的更改，将当前分支重置为上游分支，然后应用已设置的更改。 此设置可在全局范围和存储库范围内使用，并且对应于 `git config` [pull. 基址](https://git-scm.com/docs/git-config#Documentation/git-config.txt-pullrebase) 设置。 有效的设置如下所示：

- True：提取后，在上游分支顶部启用当前分支。
- False：将当前分支合并到上游分支中。
- 取消设置 (默认) ：除非在其他配置文件中指定，否则将当前分支合并到上游分支。
- Interactive：在交互模式下为变基。
- Preserve：在没有平展本地创建的合并提交的情况下变基。

1. 从 Git 菜单中转到 **设置**。 请参阅 **Git global 设置** 在全局级别配置此选项;请参阅 **Git 存储库设置**，在存储库级别配置此选项。

2. 在拉取到所需的设置 **时设置变基本地分支** ，然后选择 **"确定"** 保存。

    :::image type="content" source="media/rebase-setting.png" alt-text="屏幕截图，显示从下拉选项中突出显示 &quot;拉&quot; 和 &quot;True&quot; 时变基 &quot;本地分支&quot;。":::

在 Visual Studio 中，不能配置 `pull.rebase` 为 **交互式** 的。 Visual Studio 没有交互式的变基支持。
若要将配置 `pull.rebase` 为使用交互模式，请使用命令行。

### <a name="cryptographic-network-provider"></a>加密网络提供程序

加密网络提供程序是全局范围内的 Git 配置设置，用于配置运行时要使用的 TLS/SSL 后端，并对应于 `git config` [sslBackend](https://git-scm.com/docs/git-config#Documentation/git-config.txt-httpsslBackend) 设置。 值为，如下所示：

- OpenSSL：将 [OpenSSL](https://www.openssl.org/) 用于 TLS 和 SSL 协议。
- 安全通道：将 [安全通道 (schannel) ](/windows/win32/secauthn/secure-channel) 用于 TLS 和 SSL 协议。 Schannel 是本机 Windows 解决方案，可访问 Windows 凭据存储，从而允许企业范围内的证书管理。
- 取消设置 (默认) ：如果未设置此设置，则默认值为 OpenSSL。

1. 从 Git 菜单中转到 **设置**。 请参阅 **Git Global 设置** 以配置此设置。

2. 将 **加密网络提供程序** 设置为所需的值，然后选择 **"确定"** 保存。

   :::image type="content" source="media/network-provider-setting.png" alt-text="显示 &quot;加密网络提供程序&quot; 的屏幕截图，其中突出显示了 &quot;OpenSSL&quot;，并从下拉。":::

### <a name="credential-helper"></a>凭据帮助器

当 Visual Studio 执行远程 Git 操作时，远程终结点可能会拒绝请求，因为它要求向请求提供凭据。 此时，Git 将调用凭据帮助器，后者将返回执行操作所需的凭据，然后再次尝试请求。 所使用的凭据帮助器对应于 `git config` [credential. helper](https://git-scm.com/docs/gitcredentials) 设置。 可在全局范围内使用以下值：

- GCM for Windows：使用[Git 凭据管理器作为帮助程序 Windows](https://github.com/microsoft/Git-Credential-Manager-for-Windows) 。
- GCM Core：使用 [Git 凭据管理器核心](https://github.com/microsoft/Git-Credential-Manager-Core) 作为帮助程序。
- 取消设置 (默认) ：如果未设置此设置，则使用系统配置中设置的凭据帮助程序。 对于 Windows 2.29 的 Git，默认凭据助手为 GCM Core。

1. 从 Git 菜单中转到 **设置**。 请参阅 **Git Global 设置** 以配置此设置。

2. 将 **Credential helper** 设置为所需的值，然后选择 **"确定"** 保存。

:::image type="content" source="media/credential-helper-setting.png" alt-text="显示 &quot;选项&quot; 对话框中的 &quot;凭据帮助程序&quot; 设置的屏幕截图。":::

### <a name="diff--merge-tools"></a>& 合并工具的差异

Git 将在首选工具中显示差异和合并冲突。 本部分中的设置对应于 `git config` [diff](https://git-scm.com/docs/git-config#Documentation/git-config.txt-difftool) 和 [merge。工具](https://git-scm.com/docs/git-config#Documentation/git-config.txt-mergetool) 设置。 可以通过选择 "**使用 Visual Studio**"，将 git 配置为使用 Visual Studio 作为 **git 全局设置** 和 **git 存储设置库** 中的合并或比较工具。 若要配置其他差异和合并工具，请将 `git config` 与 [diff. 工具](https://git-scm.com/docs/git-config#Documentation/git-config.txt-difftool) 或 [merge](https://git-scm.com/docs/git-config#Documentation/git-config.txt-mergetool) 一起使用。

:::image type="content" source="media/tools-setting.png" alt-text="屏幕截图，显示在 &quot;选项&quot; 对话框中设置默认差异工具和合并工具的部分。":::

### <a name="git-files"></a>Git 文件

可以使用 **git 存储库** 中的 " **git 文件**" 部分设置范围，查看和编辑存储库的 [.gitignore](https://git-scm.com/docs/gitignore)和 [.gitattributes](https://git-scm.com/docs/gitattributes)文件。

:::image type="content" source="media/git-files-setting.png" alt-text="显示用于查看和编辑存储库中的&quot;忽略&quot;和&quot;属性&quot;文件的部分的屏幕截图。":::

### <a name="remotes"></a>遥控器

可以使用"Git **存储库"** 下的"远程"**窗格设置** 为存储库配置远程。 此设置对应于 [git remote](https://git-scm.com/docs/git-remote) 命令，并允许添加、编辑或删除远程。

:::image type="content" source="media/remotes-settings.png" alt-text="显示&quot;选项&quot;对话框中的&quot;Git 远程&quot;窗格的屏幕截图。":::

### <a name="other-settings"></a>其他设置

若要查看所有其他 Git 配置设置，可以打开和查看配置文件本身，也可以运行 来 `git config --list` 显示设置。

## <a name="visual-studio-settings"></a>Visual Studio 设置

以下设置管理 Visual Studio 中的 Git 相关首选项，并且由 Visual Studio 而不是 Git 配置文件进行管理。 本部分的所有设置都配置在 **Git 全局** 设置页。

- [默认位置](#default-location)
- [打开存储库时，关闭不在 Git 下的打开解决方案](#close-open-solutions-not-under-git-when-opening-a-repository)
- [允许从第三方源下载创作图像](#enable-download-of-author-images-from-third-party-sources)
- [默认情况下，合并后提交更改](#commit-changes-after-merge-by-default)
- [启用推送 --force](#enable-push---force-with-lease)
- [打开 Git 存储库解决方案资源管理器打开文件夹中的文件夹](#open-folder-in-solution-explorer-when-opening-a-git-repository)
- [打开 Git 存储库时自动加载解决方案](#automatically-load-the-solution-when-opening-a-git-repository)
- [双击或 Enter 键自动签出分支](#automatically-check-out-branches-with-double-click-or-the-enter-key)

### <a name="default-location"></a>默认位置

**默认** 位置配置克隆存储库的默认文件夹。

:::image type="content" source="media/default-location-setting.png" alt-text="显示&quot;选项&quot;对话框中默认位置字段的屏幕截图。":::

### <a name="close-open-solutions-not-under-git-when-opening-a-repository"></a>打开存储库时，关闭不在 Git 下的打开解决方案

默认情况下，Visual Studio切换到另一个存储库时关闭任何打开的解决方案或文件夹。 这样做时，它还可能会基于你在打开 Git 存储库时选择在 解决方案资源管理器 中打开文件夹以及打开 [Git](#open-folder-in-solution-explorer-when-opening-a-git-repository) 存储库时自动加载解决方案，来加载新存储库的解决方案或 [文件夹](#automatically-load-the-solution-when-opening-a-git-repository)。 这保持打开的代码和打开的存储库之间的一致性。 但是，如果解决方案与存储库不在同一文件夹根目录下，则切换到其存储库时，可能需要使解决方案保持打开状态。 可以使用此设置来这样做。 值为 ，如下所示：

- 是：打开存储库时，当前打开的解决方案始终关闭
- 否：打开存储库时，Visual Studio检查当前解决方案是否在 Git 下。 如果不是，则解决方案将保持打开状态。
- 始终 (默认) ：设置此选项后，可以通过打开每个存储库的对话框进行选择，无论是希望保持当前解决方案打开还是关闭它。

:::image type="content" source="media/close-sln-setting.png" alt-text="显示&quot;选项&quot;对话框中的关闭解决方案设置的屏幕截图。":::


### <a name="enable-download-of-author-images-from-third-party-sources"></a>允许从第三方源下载创作图像

允许从第三方源下载创作图像是全局Visual Studio特定设置。 选中后，从 [Gravatar](https://en.gravatar.com/)映像服务 下载作者映像（如果可用）并显示在提交和历史记录视图中。

:::image type="content" source="media/download-image-setting.png" alt-text="显示复选框的屏幕截图，该复选框用于从&quot;选项&quot;对话框中的第三方源下载创作图像。 ":::

>[!IMPORTANT]
>为了在"提交"和"历史记录"视图中提供作者图像，该工具为存储在活动存储库中的作者电子邮件地址创建 MD5 哈希。 然后，此哈希将发送到 Gravatar，为以前注册过该服务的用户查找匹配的哈希值。 如果找到匹配项，则用户图像会从服务中检索并显示在Visual Studio。 未配置该服务的用户将返回随机生成的映像。 请注意，电子邮件地址不会由 Visual Studio记录，也不会与 Gravatar 或其他任何第三方共享。

### <a name="commit-changes-after-merge-by-default"></a>默认情况下，合并后提交更改

默认 **启用"合并后提交** 更改"后，当分支与当前分支合并时，Git 会自动创建新的提交。

:::image type="content" source="media/merge-commit-setting.png" alt-text="显示&quot;选项&quot;对话框中默认在合并后提交更改的复选框的屏幕截图。":::

- 选中此选项 `git merge` 后，Visual Studio命令通过 选项 `--commit` 运行。
- 如果未选中， `git merge` 则由 Visual Studio的命令将随选项 `--no-commit --no-ff` 一起运行。

有关这些选项的详细信息，请参阅 [--commit 和 --no-commit](https://git-scm.com/docs/git-merge#Documentation/git-merge.txt---commit) 和 [--no-ff](https://git-scm.com/docs/git-merge#Documentation/git-merge.txt---no-ff)。

### <a name="enable-push---force-with-lease"></a>启用推送 --force-with-lease

启用后，此设置允许从 `push --force-with-lease` Visual Studio。 默认情况下，**禁用"启用推送 --force-with-lease"。**

:::image type="content" source="media/push-force-setting.png" alt-text="屏幕截图显示了在&quot;选项&quot;对话框中启用具有租约的推送强制的复选框。":::

有关详细信息，请参阅 [push --force-with-lease](https://git-scm.com/docs/git-push#Documentation/git-push.txt---no-force-with-lease)。

### <a name="open-folder-in-solution-explorer-when-opening-a-git-repository"></a>打开 Git 存储库解决方案资源管理器打开文件夹中的文件夹
<!-- todo: write section -->
使用 Visual Studio打开或切换到 Git 存储库时，Visual Studio加载 Git 内容，以便从 IDE 中查看更改、提交、分支和管理存储库。 此外，Visual Studio还会在 解决方案资源管理器 中加载存储库的代码。 Visual Studio将扫描存储库文件夹中的解决方案、CMakeLists.txt或它识别的其他任何视图文件，并显示为 解决方案资源管理器。 可以从中选择要加载的解决方案或文件夹来查看目录内容。 关闭此复选框时，Visual Studio不会打开存储库中的存储库解决方案资源管理器。 这实质上是允许以Visual Studio Git 存储库管理器打开数据库。 此设置默认启用。

:::image type="content" source="media/open-folder-setting.png" alt-text="显示打开&quot;选项&quot;对话框中的 Git 存储库时打开文件夹的复选框的屏幕截图。":::

### <a name="automatically-load-the-solution-when-opening-a-git-repository"></a>打开 Git 存储库时自动加载解决方案

此设置仅在打开 Git 存储库设置解决方案资源管理器 [打开"打开](#open-folder-in-solution-explorer-when-opening-a-git-repository) "文件夹时适用。 在 Visual Studio 中打开 Git 存储库时，后续文件夹扫描检测到存储库中只有一个解决方案，Visual Studio自动加载该解决方案。 如果关闭设置，则解决方案资源管理器将在视图列表中显示存储库中的单个解决方案。 但它不会加载解决方案。 默认情况下，此设置为关闭状态。

:::image type="content" source="media/load-solution-setting.png" alt-text="屏幕截图显示了在&quot;选项&quot;对话框中打开 Git 存储库时自动加载解决方案的复选框。":::

### <a name="automatically-check-out-branches-with-double-click-or-the-enter-key"></a>双击或 Enter 键自动签出分支

"Git 存储库"窗口包含树结构中显示的分支列表。 单个选择分支将切换提交历史记录窗格以显示所选分支的提交。 若要签出分支，可以右键单击打开上下文菜单，然后选择"签出 **"。** 如果启用此设置，则双击或按 Enter 键将签出分支并显示其提交。 
  
:::image type="content" source="media/checkout-branch-setting.png" alt-text="屏幕截图显示了在&quot;选项&quot;对话框中双击或 Enter 键签出分支的复选框。":::


## <a name="see-also"></a>另请参阅

> [!IMPORTANT]
> 如果你对我们有任何建议，请告诉我们！ 我们非常感激能够通过[开发人员社区](https://aka.ms/vsgitsuggestions)门户与你交流设计决策。

- Microsoft Learn 上的 [Visual Studio 中的 Git 和 GitHub 入门](/learn/modules/visual-studio-github-push/)教程
- YouTube 上的 [Visual Studio 中的 Git 入门](https://www.youtube.com/watch?v=GCZ9x3yqkyc)视频
- [通过 Git 中的 Git Visual Studio](https://devblogs.microsoft.com/visualstudio/enhanced-productivity-with-git-in-visual-studio/)博客文章
- [“选项”对话框](../ide/reference/options-dialog-box-visual-studio.md)
