---
title: Visual Studio 新增功能文档
description: Visual Studio 文档中的新增功能
ms.date: 11/01/2021
helpviewer_keywords:
- Visual Studio, what's new, docs
- what's new [Visual Studio]
ms.assetid: 89844796-621B-4EF5-9D76-197084B011CB
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: 2e6b673622ba469c2c6fea70ca57846eadef9ebc
ms.sourcegitcommit: 67dc39e93c86ba50eb5ca877b0471fb8ab8475ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2021
ms.locfileid: "132002063"
---
# <a name="whats-new-in-visual-studio-docs"></a>Visual Studio 新增功能文档

欢迎了解 Visual Studio 文档中的新增功能。以下部分提供了过去四个月的 Visual Studio 文档中的新增功能。

## <a name="october-2021"></a>2021 年 10 月

### <a name="containers"></a>容器

**更新的文章**

- [快速入门：将 Docker 与 Visual Studio 中的 React 单页面应用结合使用](../containers/container-tools-react.md) - 更新 VS 2022
- [启动 Compose 服务的子集](../containers/launch-profiles.md) - 更新 VS 2022
- [教程：使用 Docker Compose 创建多容器应用](../containers/tutorial-multicontainer.md)
  - 添加启动配置文件步骤并更新 VS 2022
  - 更新 .NET 6 和 VS 2022 预览版

### <a name="data-tools"></a>数据工具

**更新的文章**

- [在 Visual Studio 中处理数据](../data-tools/accessing-data-in-visual-studio.md) - 添加有关 32 位提供程序的注释
- [添加新连接](../data-tools/add-new-connections.md) - 添加有关 32 位提供程序的注释
- [连接到 Access 数据库中的数据](../data-tools/connect-to-data-in-an-access-database-windows-forms.md) - 添加有关 32 位提供程序的注释
- [在 Visual Studio 中创建一个数据库并添加表](../data-tools/create-a-sql-database-by-using-a-designer.md) - 更新 VS 2022

### <a name="debugger"></a>调试器

**更新的文章**

- [使用 Visual Studio 调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)
  - VS2022 调试器断点，强制运行到光标处更新
- [在 Visual Studio 调试器中使用断点](../debugger/using-breakpoints.md) - VS2022 调试器断点，强制运行到光标处更新
- [在 Azure 中的 IIS 上的 Visual Studio 中远程调试 ASP.NET Core](../debugger/remote-debugging-azure.md) - 适用于 Azure 应用服务的远程调试的更新，.NET 6 更新

### <a name="deployment"></a>部署

**新文章** 

- [发布概述](../deployment/publish-overview.md)
- [快速入门：发布 ASP.NET Web 应用](../deployment/quickstart-deploy-aspnet-web-app.md)

**更新的文章**

- [需要在 Visual Studio # 中完成部署；显示在搜索结果中的页标题。包括品牌在内，小于 60 个字符。](../deployment/index.yml) - 添加发布概述
- [从 IIS 中获取发布设置并将其导入 Visual Studio](../deployment/tutorial-import-publish-settings-iis.md) - 添加发布概述

### <a name="extensibility"></a>扩展性

**更新的文章**

- [Visual Studio 2022 中的重大 API 更改](../extensibility/migration/breaking-api-list.md) - 更新 VS 2022 中断性变更列表以在旧版查找 API 中包括重大更改

### <a name="ide"></a>IDE

**新文章**

- [使用 PerfView 收集 ETL 跟踪，以及创建用于所有调用堆栈的小型转储](./report-a-problem-perfview-minidumps.md) - 新文章创建用于合并 ETL 跟踪和创建小型转储内容

**更新的文章**
- [Visual Studio 客户体验改善计划](./visual-studio-experience-improvement-program.md)
  - 更新 VS 2022 并修复 github 问题 7139
  - 将系统生成的日志文章与 VSCEIP 合并
- [应用程序属性页（UWP 项目）](./reference/application-page-project-designer-uwp.md) - 添加“Windows 10 及更高版本”更新和更新的链接
- [配置文件和文件夹的信任设置](./reference/trust-settings.md) - 添加 VS 2022 的信任设置
- [糟糕！未找到 `F1` 帮助匹配项](./not-in-toc/default.md) - 删除和重定向排查 IDE 错误
- [针对 Visual Studio 建议功能](./suggest-a-feature.md) - 将建议状态置于表中
- [在文件中查找](./find-in-files.md) - VS 2022 的代码搜索更新
- [在文件中替换](./replace-in-files.md) - VS 2022 的代码搜索更新
- [选项、文本编辑器、C/C++、高级](./reference/options-text-editor-c-cpp-advanced.md) - 更新 C++ 文本编辑器选项，修复 7125
- [选项、文本编辑器、C/C++、视图](./reference/options-text-editor-c-cpp-view.md) - 更新 C++ 文本编辑器选项，修复 7125
- [如何报告 Visual Studio 或 Visual Studio 安装程序的问题](./how-to-report-a-problem-with-visual-studio.md) - 将“报告问题、状态和常见问题解答”合并到“如何报告问题”页中

### <a name="install"></a>安装

**更新的文章**

- [控制对基于网络的 Visual Studio 部署的更新](../install/controlling-updates-to-visual-studio-deployments.md) - 添加有关更新 VS 中的更新通知设置的命令和信息
- [Visual Studio 工作负载和组件 ID](../install/workload-and-component-ids.md) - 发布 VS 2022 预览版 5 (RC)
- [Visual Studio 生成工具组件目录](../install/workload-component-id-vs-build-tools.md) - 发布 VS 2022 预览版 5 (RC)
- [Visual Studio Community 组件目录](../install/workload-component-id-vs-community.md) - 发布 VS 2022 预览版 5 (RC)
- [Visual Studio Enterprise 组件目录](../install/workload-component-id-vs-enterprise.md) - 发布 VS 2022 预览版 5 (RC)
- [Visual Studio Professional 组件目录](../install/workload-component-id-vs-professional.md) - 发布 VS 2022 预览版 5 (RC)
- [Visual Studio 团队资源管理器组件目录](../install/workload-component-id-vs-team-explorer.md) - 发布 VS 2022 预览版 5 (RC)
- [Visual Studio Test Agent 组件目录](../install/workload-component-id-vs-test-agent.md) - 发布 VS 2022 预览版 5 (RC)
- [Visual Studio Test Controller 组件目录](../install/workload-component-id-vs-test-controller.md) - 发布 VS 2022 预览版 5 (RC)

### <a name="javascript"></a>JavaScript

**更新的文章**
- [在 Visual Studio 中管理 npm 包](../javascript/npm-package-management.md) - 新 JS/TS 项目类型的单元测试和 npm 更新
- [在 Visual Studio 中对 JavaScript 和 TypeScript 代码进行单元测试](../javascript/unit-testing-javascript-with-visual-studio.md) - 新 JS/TS 项目类型的单元测试和 npm 更新

### <a name="msbuild"></a>MSBuild

**新文章**

- [MSBuild 错误的默认 F1 页面](../msbuild/msbuild-errors.md)
- [配置任务](../msbuild/configure-tasks.md)
- [MSB4018: 任务意外失败](../msbuild/errors/msb4018.md)
- [MSB4062: 无法从程序集加载任务](../msbuild/errors/msb4062.md)

**更新的文章**

- [MSBuild 项](../msbuild/msbuild-items.md) - 记录 MatchOnMetadata
- [属性函数](../msbuild/property-functions.md) - 添加未记录的参数 versionPartCount，并阐明有关嵌套属性函数中的枚举值的文本
- [演练：使用 MSBuild](../msbuild/walkthrough-using-msbuild.md) - 更新 MSBuild 的安装链接并阐明项目生成信息

### <a name="test"></a>测试

**新文章**

- [使用热重载的测试执行](../test/test-execution-with-hot-reload.md)

### <a name="community-contributors-in-october"></a>10 月社区参与者

在此期间，以下人员为 Visual Studio 文档做出了贡献。 谢谢！ 请访问[登陆页面中的新增内容](index.yml)中“参与”下的链接，了解如何参与。

- [LarissaCrawford](https://github.com/LarissaCrawford) - Larissa Crawford (6)
- [cdmihai](https://github.com/cdmihai) - Mihai Codoban (1)
- [GitHubPang](https://github.com/GitHubPang) (1)
- [gopal-amlekar](https://github.com/gopal-amlekar) - Gopal Amlekar (1)
- [ralbury-mwb](https://github.com/ralbury-mwb) - Richard Albury (1)
- [Thieum](https://github.com/Thieum) - Matthieu Penant (1)

## <a name="september-2021"></a>2021 年 9 月

### <a name="code-quality"></a>代码质量

**更新的文章**

- [从旧版分析 (FxCop) 迁移到源分析（.NET 分析器）](../code-quality/migrate-from-legacy-analysis-to-net-analyzers.md) - 有关禁用旧版代码分析的其他说明

### <a name="debugger"></a>调试器

**更新的文章**

- [初步了解 Visual Studio 调试器](../debugger/debugger-feature-tour.md) - 有关调试、诊断和部署的内容性能更新
- [配置 Windows 防火墙以便进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md) - VS 2022 的远程调试器更新
- [远程调试器端口分配](../debugger/remote-debugger-port-assignments.md) - VS 2022 的远程调试器更新

### <a name="deployment"></a>部署

**新文章** 

- [使用 Visual Studio 创建的 GitHub Actions 工作流将应用程序部署到 Azure](../deployment/azure-deployment-using-github-actions.md) - 创建了新文章

**更新的文章**

- [初步了解 Visual Studio 部署](../deployment/deploying-applications-services-and-components.md) - 有关调试、诊断和部署的内容性能更新
- [使用 Visual Studio 创建的 GitHub Actions 工作流将应用程序部署到 Azure](../deployment/azure-deployment-using-github-actions.md)
  - VS 2022 的远程调试器更新
  - GitHub Actions CI/CD 发布中的编辑传递
  - VS 和 GitHub Actions 的新操作指南的初始提交

### <a name="extensibility"></a>扩展性

**新文章**

- [如何：使用 VsixUtil 创建用于 Visual Studio 专用库的 ATOM 馈送 (VsixFeed)](../extensibility/how-to-create-vsix-feed-for-private-gallery.md) - 创建了新文章

**更新的文章**

- [创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)
  - 从 VS 2022 开始，UWP 扩展 SDK 必须在 SdkManifest.xml 中列出工具箱项目

### <a name="get-started"></a>入门

**新文章**

- [教程：在打开存储库中的项目](../get-started/tutorial-open-project-from-repo.md) - 创建了新文章

### <a name="ide"></a>IDE

**更新的文章**
- [Visual Studio 的功能](./advanced-feature-overview.md) - 更新源代码管理部分
- [Visual Studio 中的键盘快捷方式](./default-keyboard-shortcuts-in-visual-studio.md) - 3 个部分的目录和 ABC 顺序
- [Visual Studio 2022（预览版）中的新增功能](./whats-new-visual-studio-2022.md) - 修订标题层次结构、重新排列信息并添加动态 GIF
- [如何：更改生成输出目录](./how-to-change-the-build-output-directory.md)
  - 针对 Visual Studio 2022 预览版进行查看并在需要时更新
  - 更新适用于 VS 2022 的生成配置文章
- [如何：配置项目以面向目标平台](./how-to-configure-projects-to-target-platforms.md) - 针对 Visual Studio 2022 进行查看并在需要时更新
- [了解解决方案资源管理器](./use-solution-explorer.md) - 添加解决方案资源管理器上下文菜单信息

### <a name="install"></a>安装

**更新的文章**

- [容器的高级示例](../install/advanced-build-tools-container.md)
  - 添加 start /wait 命令以修复 github 问题 #6765
  - 更新安装 VS 生成工具的方法

### <a name="javascript"></a>JavaScript

**新文章**

- [Visual Studio 2022 中的 JavaScript 和 TypeScript](../javascript/javascript-in-vs-2022.md) - 创建了新文章

**更新的文章**
- [教程：在 Visual Studio 中使用 Vue 创建 ASP.NET Core 应用](../javascript/tutorial-asp-net-core-with-vue.md) - 草拟了 Visual Studio 2022 中的 JavaScript 和 TypeScript 的新增功能

### <a name="msbuild"></a>MSBuild

**更新的文章**

- [属性函数](../msbuild/property-functions.md)
  - 改进了 Get...OfFileAbove 说明

### <a name="vsto"></a>VSTO

**新文章**

- [Visual Studio Tools for Office Runtime](../vsto/visual-studio-tools-for-office-runtime.md) - 创建了新文章

### <a name="xaml-tools"></a>XAML 工具

**更新的文章**

- [XAML 热重载：在 WPF 和 UWP 应用运行时编写和调试它们](../xaml-tools/xaml-hot-reload.md)
  - 更新元数据，并对文本进行少量编辑
  - 更新 XAML 热重载简介部分

## <a name="august-2021"></a>2021 年 8 月

### <a name="containers"></a>容器

**更新的文章**

- [如何配置 Visual Studio 容器工具](../containers/container-tools-configure.md) - 容器工具 8 月内容
- [适用于 Docker 的 Visual Studio 容器工具](../containers/overview.md) - 容器工具 8 月内容
- [使用“容器”窗口](../containers/view-and-diagnose-containers.md) - 容器工具 8 月内容

### <a name="debugger"></a>调试器

**更新的文章**

- [远程调试远程 IIS 计算机上的 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md) - WS 2019 和 .NET 5 刷新
- [远程调试 Visual Studio 中远程 IIS 计算机上的 ASP.NET Core](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md) - WS 2019 和 .NET 5 刷新
- [在 Visual Studio 中的 Azure 中远程调试 IIS 上的 ASP.NET Core](../debugger/remote-debugging-azure.md) - WS 2019 和 .NET 5 刷新
- [附加到在 Docker 容器上运行的进程](../debugger/attach-to-process-running-in-docker-container.md) - Linux 附加到进程的方案更新
- [使用 Visual Studio 在 WSL 中调试 .NET 应用](../debugger/debug-dotnet-core-in-wsl-2.md) - WSL 调试更新

### <a name="deployment"></a>部署

**更新的文章**

- [通过在 Visual Studio 中导入发布设置将应用程序发布到 IIS](../deployment/tutorial-import-publish-settings-iis.md) - WS 2019 和 .NET 5 刷新

### <a name="extensibility"></a>扩展性

**更新的文章**

- [添加语言服务器协议扩展](../extensibility/adding-an-lsp-extension.md) - 关于 LSP 扩展中的 MiddleLayer 文档的更新信息

### <a name="ide"></a>IDE

**新文章**

- [注册 Dotfuscator Community](./dotfuscator/register.md) - 已创建新文章
- [从 Dotfuscator Community 5 升级](./dotfuscator/upgrade-from-5.md) - 已创建新文章

**更新的文章**
- [如何：使用引用管理器添加或删除引用](./how-to-add-or-remove-references-by-using-the-reference-manager.md) - 更新“添加 > 引用”部分
- [What's new in Visual Studio 2022（预览版）中的新增功能](./whats-new-visual-studio-2022.md) - Visual Studio 2022 预览版 3 中的新增功能更新
- [第 6 步：使用 Git](../python/tutorial-working-with-python-in-visual-studio-step-06-working-with-git.md) - 将已更新的 Git 源代码管理信息添加到 Python 教程
- [教程：在 Visual Studio 中创建简单的 C# 控制台应用（第 1 部分/共 2 部分）](../get-started/csharp/tutorial-console.md) - 将 Git 源代码管理信息添加到 CSharp 控制台教程
- [教程：Visual Studio 中的 Visual Basic 入门](../get-started/visual-basic/tutorial-console.md) - 将 Git 源代码管理信息添加到 VB 控制台教程
- [在 C++ 中创建控制台计算器](/cpp/get-started/tutorial-console-cpp) - 将 Git 信息添加到 C++ 控制台计算器教程

### <a name="install"></a>安装

**更新的文章**

- [在容器中安装生成工具](../install/build-tools-container.md) - Visual Studio 2022 更新

### <a name="javascript"></a>JavaScript

**新文章**

- [教程：在 Visual Studio 中使用 Vue 创建 ASP.NET Core 应用](../javascript/tutorial-asp-net-core-with-vue.md) - 已创建新文章
- [创建 Angular 应用](../javascript/tutorial-create-angular-app.md) - 已创建新文章
- [创建 React 应用](../javascript/tutorial-create-react-app.md) - 已创建新文章
- [创建 Vue.js 应用](../javascript/tutorial-create-vue-app.md) - 已创建新文章

**更新的文章**
- [需要 Visual Studio # 中的 JavaScript 和 TypeScript；搜索结果中显示页标题。包括品牌。小于 60 个字符。](../javascript/index.yml) - 用不同的链接更新索引页面

### <a name="test"></a>测试

**新文章**

- [远程测试（试验性预览）](../test/remote-testing.md)- 已创建新文章

**更新的文章**

- [单元测试入门](../test/getting-started-with-unit-testing.md) - 在教程中添加 C++ 支持和单元测试改进

## <a name="july-2021"></a>2021 年 7 月

### <a name="debugger"></a>调试器

**更新的文章**

- [创建自定义数据可视化工具](../debugger/create-custom-visualizers-of-data.md) - 更新可视化工具文档，添加了更多步骤，适用于 .NET 5.0 场景
- [演练：使用 C 编写可视化工具\#](../debugger/walkthrough-writing-a-visualizer-in-csharp.md) - .NET 5 的可视化工具内容和自定义数据对象的新内容

### <a name="extensibility"></a>扩展性

**新文章**

- [Visual Studio 2017 扩展性常见问题解答](../extensibility/faq-2017.yml)

### <a name="ide"></a>IDE

**新文章**

- [Visual Studio 2022（预览版）中的新增功能](./whats-new-visual-studio-2022.md)
- [报告问题：状态和常见问题解答](./how-to-report-a-problem-with-visual-studio.md)

**更新的文章**
- [在文件中查找](./find-in-files.md) - 添加了“多个搜索”部分，以及常规更新
- [配置文件和文件夹的信任设置](./reference/trust-settings.md) - 添加了有关 VS2022 中的新“信任设置”的信息
- [Visual Studio 中的默认键盘快捷方式](./default-keyboard-shortcuts-in-visual-studio.md) - 添加了键盘快捷方式说明

### <a name="javascript"></a>JavaScript

**新文章**

- [教程：在 Visual Studio 中使用 Angular 创建 ASP.NET Core 应用](../javascript/tutorial-asp-net-core-with-angular.md)
- [教程：在 Visual Studio 中使用 React 创建 ASP.NET Core 应用](../javascript/tutorial-asp-net-core-with-react.md)

### <a name="msbuild"></a>MSBuild

**新文章**

- [MSB3027：无法将“source”复制到“dest”。超出了“number”的重试次数。失败](../msbuild/errors/msb3027.md)
- [MSB3086](../msbuild/errors/msb3086.md)
- [MSB3190：ClickOnce 不支持请求执行级别“level”](../msbuild/errors/msb3190.md)
- [MSB3275](../msbuild/errors/msb3275.md)
- [MSB3303：无法解析 COM 引用“reference”版本“version”](../msbuild/errors/msb3303.md)
- [MSB3304：无法确定 COM 引用“reference”的依赖项](../msbuild/errors/msb3304.md)
- [MSB3305：正在处理来自路径“path”的 COM 引用“reference”](../msbuild/errors/msb3305.md)
- [MSB3325：无法导入以下密钥文件](../msbuild/errors/msb3325.md)
- [MSB3326：无法导入以下密钥文件](../msbuild/errors/msb3326.md)
- [MSB3327](../msbuild/errors/msb3327.md)
- [资源文件“name”的名称无效](../msbuild/errors/msb3553.md)
- [MSB3836](../msbuild/errors/msb3836.md)
- [MSB3884：无法找到规则集文件“filename”](../msbuild/errors/msb3884.md)
- [MSB4094](../msbuild/errors/msb4094.md)
- [MSB4096：项列表“item-list”中的项“item”未定义元数据“name”的值](../msbuild/errors/msb4096.md)
- [MSB4166](../msbuild/errors/msb4166.md)
- [MSB4175：无法从程序集“assembly-name”加载任务工厂“task-factory-name”](../msbuild/errors/msb4175.md)
- [MSB6001：“tool”的命令行开关无效](../msbuild/errors/msb6001.md)
- [MSB6011：传递给“task-name”任务的参数无效](../msbuild/errors/msb6011.md)
- [MSB3075：命令“name”已退出，代码为“error-code”。请验证你是否有足够权限来运行此命令](../msbuild/errors/msb3075.md)
- [MSB3103：Resx 文件无效](../msbuild/errors/msb3103.md)
- [MSB3274：无法解析主引用“name”，因为它是针对“version”框架构建的](../msbuild/errors/msb3274.md)
- [MSB3552：找不到资源文件“filename”](../msbuild/errors/msb3552.md)
- [MSB3554：无法写入输出文件“filename”](../msbuild/errors/msb3554.md)
- [MSB3645：找不到 .NET Framework v3.5 Service Pack 1。若要以“framework-version”为目标，必须安装 .NET Framework v3.5 Service Pack 1 或更高版本](../msbuild/errors/msb3645.md)
- [MSB3822：非字符串资源要求在运行时使用 System.Resources.Extensions 程序集，但未在此项目的引用中找到它](../msbuild/errors/msb3822.md)
- [MSB3971：找不到“name”的引用程序集](../msbuild/errors/msb3971.md)
- [MSB4086：在条件“condition”中，尝试对计算结果为“value”而不是数字的“expression”进行数值比较](../msbuild/errors/msb4086.md)
- [MSB4236：找不到指定的 SDK“name”](../msbuild/errors/msb4236.md)
- [MSB6004：指定的任务可执行文件位置“path”无效](../msbuild/errors/msb6004.md)

**更新的文章**

- [演练：使用 MSBuild](../msbuild/walkthrough-using-msbuild.md) - MSBuild 演练 VS 2022 程序文件