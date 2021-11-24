---
title: Visual Studio 中的 Git 设置
titleSuffix: ''
description: 了解 Visual Studio 如何使用 .gitconfig 文件和 Git 设置来管理首选项
ms.date: 06/08/2021
ms.topic: conceptual
author: Taysser-Gherfal
ms.author: tglee
ms.manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
monikerRange: '>=vs-2019'
ms.openlocfilehash: efe8498a770a6bcb6394ce435ce997922e0cc955
ms.sourcegitcommit: dc12d3d0ca2ec3601cb9de7c22e61ecf22c7c514
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2021
ms.locfileid: "132264123"
---
# <a name="git-settings-and-preferences-in-visual-studio"></a>Visual Studio 中的 Git 设置和首选项

在 Visual Studio 中，可以配置和查看常见的 Git 设置和首选项，例如姓名和电子邮件地址、首选差异工具与合并工具等。 可以在“Git 全局设置”页（适用于所有存储库）或“Git 存储库设置”页（适用于当前存储库）上的“选项”对话框中查看和配置这些设置和首选项。

可以配置两种类型的设置：

- [Git 设置](#git-settings) - 本部分中的设置对应于保存在 Git 配置文件中的 Git 设置。 这些设置可以在 Visual Studio 中查看和修改，但由 Git 配置文件管理。
- [Visual Studio 设置](#visual-studio-settings) - 本部分中的设置配置由 Visual Studio 管理的 Git 相关设置和首选项。

## <a name="how-to-configure-settings"></a>如何配置设置

1. 若要在 Visual Studio 中配置 Git 设置，请从顶级 Git 菜单中选择“设置”。

   :::image type="content" source="media/git-menu-settings.png" alt-text="包含对设置命令的标注的 Git 菜单。":::

2. 选择“Git 全局设置”或“Git 存储库设置”以查看和配置全局级别或存储库级别设置。

   :::image type="content" source="media/source-control-settings.png" alt-text="“选项”对话框中的导航窗格，包含对 Git 设置的标注。":::

3. 可以配置多个常见的 Git 设置，如本文以下部分所述。 配置所需设置后，选择“确定”以保存更新后的设置。

   :::image type="content" source="media/ok-button.png" alt-text="“选项”对话框的显示区域，其中标注了“确定”按钮。":::

## <a name="git-settings"></a>Git 设置

还可以配置和检查一些最常见的 Git 配置设置。 你可以在 Visual Studio 中查看和修改以下设置，即使它们是由 Git 配置文件管理的。

- [姓名和电子邮件](#name-and-email)
- [在提取期间删除远程分支](#prune-remote-branches-during-fetch)
- [拉取时变基本地分支](#rebase-local-branch-when-pulling)
- [加密网络提供程序](#cryptographic-network-provider)
- [凭据帮助程序](#credential-helper)
- [差异工具与合并工具](#diff--merge-tools)
- [Git 文件](#git-files)
- [远程库](#remotes)
- [其他设置](#other-settings)

>[!NOTE]
>Visual Studio“全局设置”中配置的 Git 设置对应于 Git 用户特定配置文件中的设置，而“存储库设置”中的设置对应于存储库特定配置文件中的设置。 有关 Git 配置的详细信息，请参阅[关于自定义 Git 的 Pro Git 章节](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)、[git-config 文档](https://git-scm.com/docs/git-config)和[配置文件上的 Pro Git 引用](https://git-scm.com/docs/git-config#FILES)。 若要配置未在 Visual Studio 中公开的 Git 设置，请使用 `git config` 命令将值写入配置文件：`git config [--local|--global|--system] section.key value`。

### <a name="name-and-email"></a>姓名和电子邮件

你提供的名称和电子邮件将用作你进行的任何提交的提交者信息。 此设置在全局和存储库范围内可用，并对应于 `git config` [user.name](https://git-scm.com/docs/git-config#Documentation/git-config.txt-username) 和 [user.email](https://git-scm.com/docs/git-config#Documentation/git-config.txt-useremail) 设置。

1. 在 Git 菜单中，转到“设置”。 若要在全局级别设置用户名和电子邮件，请转到“Git 全局设置”；若要在存储库级别设置用户名和电子邮件，请转到“Git 存储库设置” 。

2. 提供用户名和电子邮件，然后选择“确定”以保存。

   :::image type="content" source="media/user-email-setting.png" alt-text="“选项”对话框中的“Git 全局设置”窗格，其中包含电子邮件用户名标注。":::

### <a name="prune-remote-branches-during-fetch"></a>在提取期间删除远程分支

删除操作会删除不再存在于远程库上的远程跟踪分支，有助于将分支列表保持干净和最新。 此设置可在全局范围和存储库范围内使用，并对应于 `git config` [fetch.prune](https://git-scm.com/docs/git-config#Documentation/git-config.txt-fetchprune) 设置。

建议在全局级别将此选项设置为 True。 有效设置如下：

- True（建议）
- False
- 取消设置（默认值）

1. 在 Git 菜单中，转到“设置”。 若要在全局级别配置此选项，请转到“Git 全局设置”；若要在存储库级别配置此选项，请转到“Git 存储库设置” 。

2. 将“在提取期间删除远程分支”设置为“True”（建议）。 选择“确定”以保存。

:::image type="content" source="media/prune-setting.png" alt-text="突出显示“在提取期间删除远程分支”，并从下拉列表中选择了“True”的屏幕截图。":::

### <a name="rebase-local-branch-when-pulling"></a>拉取时变基本地分支

变基会保留当前分支中不属于上游分支的提交所做的更改，将当前分支重置为上游分支，然后应用保留的更改。 此设置可在全局范围和存储库范围内使用，并对应于 `git config` [pull.rebase](https://git-scm.com/docs/git-config#Documentation/git-config.txt-pullrebase) 设置。 有效设置如下：

- True：提取后将当前分支变基到上游分支顶部。
- False：将当前分支合并到上游分支。
- 取消设置（默认值）：除非在其他配置文件中指定，否则将当前分支合并到上游分支。
- 交互式：在交互模式下变基。
- 保留：在不平展本地创建的合并提交的情况下变基。

1. 在 Git 菜单中，转到“设置”。 若要在全局级别配置此选项，请转到“Git 全局设置”；若要在存储库级别配置此选项，请转到“Git 存储库设置” 。

2. 将“拉取时变基本地分支”设置为所需设置，然后选择“确定”以保存。

    :::image type="content" source="media/rebase-setting.png" alt-text="突出显示“拉取时变基本地分支”，并从下拉列表中选择了“True”的屏幕截图。":::

在 Visual Studio 中，不能将 `pull.rebase` 配置为“交互式”。 Visual Studio 没有交互式变基支持。
若要将 `pull.rebase` 配置为使用交互模式，请使用命令行。

### <a name="cryptographic-network-provider"></a>加密网络提供程序

加密网络提供程序是全局范围的 Git 配置设置，用于配置要在运行时使用的 TLS/SSL 后端，并对应于 `git config` [http.sslBackend](https://git-scm.com/docs/git-config#Documentation/git-config.txt-httpsslBackend) 设置。 值包括：

- OpenSSL：将 [OpenSSL](https://www.openssl.org/) 用于 TLS 和 SSL 协议。
- 安全通道：将[安全通道 (schannel)](/windows/win32/secauthn/secure-channel) 用于 TLS 和 SSL 协议。 Schannel 是本机 Windows 解决方案，可以访问 Windows Credential Store，从而允许企业范围的证书管理。
- 取消设置（默认值）：如果取消设置此设置，则 OpenSSL 为默认值。

1. 在 Git 菜单中，转到“设置”。 请转到“Git 全局设置”以配置此设置。

2. 将“加密网络提供程序”设置为所需的值，然后选择”确定”以保存。

   :::image type="content" source="media/network-provider-setting.png" alt-text="突出显示“加密网络提供程序”，并从下拉列表中选择了“OpenSSL”的屏幕截图。":::

### <a name="credential-helper"></a>凭据帮助程序

当 Visual Studio 执行远程 Git 操作时，远程终结点可能会拒绝请求，因为它需要随请求一起提供凭据。 此时，Git 会调用凭据帮助程序，该帮助程序将返回执行该操作所需的凭据，然后重试请求。 所使用的凭据帮助程序对应于 `git config`[credential.helper](https://git-scm.com/docs/gitcredentials) 设置。 它在全局范围内提供，具有以下值：

- GCM for Windows：使用 [Git Credential Manager for Windows](https://github.com/microsoft/Git-Credential-Manager-for-Windows) 作为帮助程序。
- GCM Core：使用 [Git Credential Manager Core](https://github.com/microsoft/Git-Credential-Manager-Core) 作为帮助程序。
- 取消设置（默认值）：如果取消设置此设置，则使用系统配置中设置的凭据帮助程序。 从 Git for Windows 2.29 起，默认凭据帮助程序为 GCM Core。

1. 在 Git 菜单中，转到“设置”。 请转到“Git 全局设置”以配置此设置。

2. 将“凭据帮助程序”设置为所需的值，然后选择“确定”以保存。

:::image type="content" source="media/credential-helper-setting.png" alt-text="显示“选项”对话框中的“凭据帮助程序”设置的屏幕截图。":::

### <a name="diff--merge-tools"></a>差异工具与合并工具

Git 将在首选工具中显示差异与合并冲突。 本部分中的设置对应于 `git config` [diff.tool](https://git-scm.com/docs/git-config#Documentation/git-config.txt-difftool) 和 [merge.tool](https://git-scm.com/docs/git-config#Documentation/git-config.txt-mergetool) 设置。 可以通过选择“使用 Visual Studio”，将 Git 配置为使用 Visual Studio 作为“Git 全局设置”和“Git 存储设置库”中的合并或差异工具。 若要配置其他差异与合并工具，请将 `git config` 与 [diff.tool](https://git-scm.com/docs/git-config#Documentation/git-config.txt-difftool) 或 [merge.tool](https://git-scm.com/docs/git-config#Documentation/git-config.txt-mergetool) 开关一起使用。

:::image type="content" source="media/tools-setting.png" alt-text="显示在“选项”对话框中设置默认差异工具与合并工具的部分的屏幕截图。":::

### <a name="git-files"></a>Git 文件

可以使用“Git 存储库设置”范围中的“Git 文件”部分查看和编辑存储库的 [gitignore](https://git-scm.com/docs/gitignore) 和 [gitattributes](https://git-scm.com/docs/gitattributes) 文件。

:::image type="content" source="media/git-files-setting.png" alt-text="显示用于查看和编辑存储库中“Ignore”和“attributes”文件的部分的屏幕截图。":::

### <a name="remotes"></a>远程库

可以使用“Git 存储库设置”下的“远程库”窗格为存储库配置远程库。 此设置对应于 [git remote](https://git-scm.com/docs/git-remote) 命令，并允许添加、编辑或删除远程库。

:::image type="content" source="media/remotes-settings.png" alt-text="显示“选项”对话框中的“Git 远程库”窗格的屏幕截图。":::

### <a name="other-settings"></a>其他设置

若要查看所有其他 Git 配置设置，可以打开和查看配置文件本身，也可以运行 `git config --list` 来显示设置。

## <a name="visual-studio-settings"></a>Visual Studio 设置

以下设置管理 Visual Studio 中的 Git 相关首选项，由 Visual Studio 而不是 Git 配置文件管理。 本部分的所有设置都在“Git 全局设置”页中配置。

- [默认位置](#default-location)
- [打开存储库时，关闭未在 Git 下且打开的解决方案](#close-open-solutions-not-under-git-when-opening-a-repository)
- [支持从第三方源下载作者图像](#enable-download-of-author-images-from-third-party-sources)
- [默认情况下合并后提交更改](#commit-changes-after-merge-by-default)
- [启用 push --force](#enable-push---force-with-lease)
- [打开 Git 存储库时在解决方案资源管理器中打开文件夹](#open-folder-in-solution-explorer-when-opening-a-git-repository)
- [打开 Git 存储库时自动加载解决方案](#automatically-load-the-solution-when-opening-a-git-repository)
- [通过双击或按 Enter 键自动签出分支](#automatically-check-out-branches-with-double-click-or-the-enter-key)

### <a name="default-location"></a>默认位置

“默认位置”配置克隆存储库的默认文件夹。

:::image type="content" source="media/default-location-setting.png" alt-text="显示“选项”对话框中“默认位置”字段的屏幕截图。":::

### <a name="close-open-solutions-not-under-git-when-opening-a-repository"></a>打开存储库时，关闭未在 Git 下且打开的解决方案

默认情况下，当你切换到另一个存储库时，Visual Studio 将关闭任何打开的解决方案或文件夹。 这样做时，它还可能会基于你是选择[打开 Git 存储库时在解决方案资源管理器中打开文件夹](#open-folder-in-solution-explorer-when-opening-a-git-repository)还是[打开 Git 存储库时自动加载解决方案](#automatically-load-the-solution-when-opening-a-git-repository)，来加载新存储库的解决方案或文件夹。 这使得打开的代码和打开的存储库保持一致性。 但是，如果解决方案与存储库不在同一文件夹根目录下，则在你切换到解决方案的存储库时，可能需要使解决方案保持打开状态。 可以使用此设置来完成此操作。 值包括：

- 是：打开存储库时，当前打开的解决方案始终关闭
- 否：打开存储库时，Visual Studio 检查当前解决方案是否在 Git 下。 如果不在，则解决方案将保持打开状态。
- 始终询问（默认值）：设置此选项后，可以通过每个打开的存储库的对话框来选择是保持当前解决方案打开还是将其关闭。

:::image type="content" source="media/close-sln-setting.png" alt-text="显示“选项”对话框中的关闭解决方案设置的屏幕截图。":::


### <a name="enable-download-of-author-images-from-third-party-sources"></a>支持从第三方源下载作者图像

允许从第三方源下载作者图像是全局范围的 Visual Studio 特定设置。 选中后，从 [Gravatar 图像服务](https://en.gravatar.com/)下载作者图像（如果可用），并显示在提交和历史记录视图中。

:::image type="content" source="media/download-image-setting.png" alt-text="显示“选项”对话框中“启用从第三方源下载作者图像”复选框的屏幕截图。":::

>[!IMPORTANT]
>为了在“提交”和“历史记录”视图中提供作者图像，该工具为存储在活动存储库中的作者电子邮件地址创建 MD5 哈希。 然后，此哈希将发送到 Gravatar，为以前注册过该服务的用户查找匹配的哈希值。 如果找到匹配项，则会从服务中检索到用户图像并显示在 Visual Studio 中。 未配置该服务的用户将返回随机生成的图像。 请注意，电子邮件地址不会由 Visual Studio 记录，也不会与 Gravatar 或其他任何第三方共享。

### <a name="commit-changes-after-merge-by-default"></a>默认情况下合并后提交更改

启用“默认情况下合并后提交更改”后，当分支与当前分支合并时，Git 会自动创建新提交。

:::image type="content" source="media/merge-commit-setting.png" alt-text="显示“选项”对话框中“默认情况下合并后提交更改”复选框的屏幕截图。":::

- 选中此复选框后，Visual Studio 发出的 `git merge` 命令将与 `--commit` 选项一起运行。
- 如果未选中，Visual Studio 发出的 `git merge` 命令将与 `--no-commit --no-ff` 选项一起运行。

有关这些选项的详细信息，请参阅 [--commit 和 --no-commit](https://git-scm.com/docs/git-merge#Documentation/git-merge.txt---commit) 和 [--no-ff](https://git-scm.com/docs/git-merge#Documentation/git-merge.txt---no-ff)。

### <a name="enable-push---force-with-lease"></a>启用 push --force-with-lease

启用后，此设置允许从 Visual Studio 运行 `push --force-with-lease`。 默认情况下，“启用 push --force-with-lease”处于禁用状态。

:::image type="content" source="media/push-force-setting.png" alt-text="显示“选项”对话框中“启用 push force with lease”复选框的屏幕截图。":::

有关详细信息，请参阅 [push --force-with-lease](https://git-scm.com/docs/git-push#Documentation/git-push.txt---no-force-with-lease)。

### <a name="open-folder-in-solution-explorer-when-opening-a-git-repository"></a>打开 Git 存储库时在解决方案资源管理器中打开文件夹
<!-- todo: write section -->
使用 Visual Studio 打开或切换到 Git 存储库时，Visual Studio 会加载 Git 内容，以便从 IDE 中查看更改、提交、分支和管理存储库。 此外，Visual Studio 还会在解决方案资源管理器中加载存储库代码。 Visual Studio 将扫描存储库文件夹中的解决方案，CMakeLists.txt，或者它识别的其他任何视图文件，并在解决方案资源管理器中以列表形式显示。 可以从中选择要加载的解决方案或文件夹来查看目录内容。 关闭此复选框时，Visual Studio 不会打开解决方案资源管理器中的存储库文件夹。 这实质上允许你仅以 Git 存储库管理员身份打开 Visual Studio。 此设置默认启用。

:::image type="content" source="media/open-folder-setting.png" alt-text="显示“选项”对话框中打开 Git 存储库时打开文件夹的复选框的屏幕截图。":::

### <a name="automatically-load-the-solution-when-opening-a-git-repository"></a>打开 Git 存储库时自动加载解决方案

只有在启用了[打开 Git 存储库时在解决方案资源管理器中打开文件夹](#open-folder-in-solution-explorer-when-opening-a-git-repository)设置时，此设置才适用。 在 Visual Studio 中打开 Git 存储库时，如果后续文件夹扫描检测到存储库中只有一个解决方案，则 Visual Studio 会自动加载该解决方案。 如果关闭此设置，则解决方案资源管理器将在视图列表中显示存储库中的单个解决方案。 但它不会加载解决方案。 默认情况下，此设置关闭。

:::image type="content" source="media/load-solution-setting.png" alt-text="显示“选项”对话框中“打开 Git 存储库时自动加载解决方案”复选框的屏幕截图。":::

### <a name="automatically-check-out-branches-with-double-click-or-the-enter-key"></a>通过双击或按 Enter 键自动签出分支

“Git 存储库”窗口包含树结构中显示的分支列表。 选择单个分支将切换提交历史记录窗格以显示所选分支的提交。 若要签出分支，可以右键单击以打开上下文菜单，然后选择“签出”。 如果启用此设置，则双击或按 Enter 键将签出分支并显示其提交。

:::image type="content" source="media/checkout-branch-setting.png" alt-text="显示“选项”对话框中通过双击或按 Enter 键签出分支的复选框的屏幕截图。":::


## <a name="see-also"></a>另请参阅

> [!IMPORTANT]
> 如果你对我们有任何建议，请告诉我们！ 我们非常感激能够通过[开发人员社区](https://aka.ms/vsgitsuggestions)门户与你交流设计决策。

- Microsoft Learn 上的 [Visual Studio 中的 Git 和 GitHub 入门](/learn/modules/visual-studio-github-push/)教程
- YouTube 上的 [Visual Studio 中的 Git 入门](https://www.youtube.com/watch?v=GCZ9x3yqkyc)视频
- [在 Visual Studio 中使用 Git 提高工作效率](https://devblogs.microsoft.com/visualstudio/enhanced-productivity-with-git-in-visual-studio/)博客文章
- [“选项”对话框](../ide/reference/options-dialog-box-visual-studio.md)
