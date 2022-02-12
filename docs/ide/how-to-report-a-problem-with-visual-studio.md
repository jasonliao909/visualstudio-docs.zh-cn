---
title: 报告 Visual Studio 的问题
description: 了解如何报告 Visual Studio 的问题
ms.date: 10/07/2021
ms.topic: how-to
ms.assetid: bee01179-cde5-4419-9095-190ee0ba5902
author: madskristensen
ms.author: madsk
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 2105002d56da13862e6e0d6646d602b43c331046
ms.sourcegitcommit: a439b1878939b2364cee0d09b851c2a67c42e563
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2022
ms.locfileid: "138567380"
---
# <a name="report-a-problem-with-the-visual-studio-product-or-installer"></a>报告 Visual Studio 产品或安装程序的问题

> [!NOTE]
> 对于 Visual Studio for Mac，请参阅[如何报告 Visual Studio for Mac 的问题](/visualstudio/mac/report-a-problem)。

可以通过 Visual Studio 或其安装程序报告问题。 利用内置的反馈工具，你可以轻松添加可帮助 Visual Studio 团队诊断和修复问题的诊断信息。 

下面是报告问题的步骤。

1. 在 Visual Studio 中，选择右上角的反馈图标并选择“报告问题”。 此外可以从菜单“帮助” > “发送反馈” > “报告问题”来访问反馈工具。
![屏幕截图显示在 Visual Studio 窗口右上角已选中“反馈”图标，并且已在下文菜单中选中“报告问题”。](media/feedback-button.png)
或者，如果无法安装 Visual Studio 或无法访问 Visual Studio 中的反馈工具，则在 Visual Studio 安装程序中报告问题。  在安装程序中，选择右上角的反馈图标并选择“报告问题”。
![屏幕截图显示在 Visual Studio 安装程序右上角已选中“反馈”图标，并且已在下文菜单中选中“报告问题”。](media/installer.png)

1. 单击“报告问题”将打开默认浏览器，并使用登录 Visual Studio 时使用的同一帐户登录

   ![登录以报告问题](../ide/media/feedback-browser-top.png)

1. 首先输入 bug 报告的描述性标题。 它的长度必须至少为 25 个字符。

    ![报告问题](../ide/media/feedback-report.png)

1. 开始键入后，“标题”字段下会显示可能的重复项

    ![搜索重复项](../ide/media/feedback-search.png)

1. 选择可能的重复 bug 报告，查看是否存在与自己的问题匹配的项。 如果存在，则为其投票，而非创建自己的票证。

    ![为重复项投票](../ide/media/feedback-duplicate.png)

1. 如果未找到任何重复项，则继续输入问题的说明。 尽可能清楚地说明问题，使我们更有可能重现 bug，这一点很重要。 请确保包含清晰的重现步骤。

1. 如果与 bug 报告相关，请通过选中“包括 Visual Studio 屏幕截图”复选框来抓取屏幕截图。  你甚至可以直接在浏览器中裁剪屏幕截图，以删除任何敏感或无关的部分。

    ![抓取屏幕截图](../ide/media/feedback-screenshot.png)仅 Microsoft 工程师可以查看此屏幕截图

1. <a name="trace"/>要帮助 Visual Studio 工程团队解决问题，最佳方法之一是提供跟踪和堆转储文件供其查看。 可以通过记录导致 bug 的步骤轻松执行此操作。

    ![记录你的操作](../ide/media/feedback-recording.png)仅 Microsoft 工程师可以查看该记录

5. 查看附加的文件，并上传其他文件（如果你认为这有助于诊断问题）。

    ![附加的文件](../ide/media/feedback-attachments.png)仅 Microsoft 工程师可以查看附加的文件

6. 最后一步是点击“提交”按钮。 提交报告会直接将报告发送到内部 Visual Studio bug 报告系统等待会审。

你的每个问题报告都会成为我们核心工程系统中的工作项，使你能够直接与产品团队互动，以帮助我们识别和解决有影响力的问题。 提供丰富诊断信息的反馈对于改进 Visual Studio 产品系列至关重要。 非常感谢你花时间报告问题。

此外，你还可以对其他社区成员的反馈进行投票，以便更多地关注问题并帮助更快地解决问题。

## <a name="when-further-information-is-needed"></a>如果需要进一步信息

如果问题缺少重要信息，我们将分配“需要更多信息”状态。 我们将在问题上评论称我们需要该特定信息，你也将收到电子邮件通知。 如果我们在 7 天内未收到该信息，将向你发送提醒。 之后，如果你 14 天内未操作，我们将关闭该票证。

1. 访问电子邮件中指向问题报表的链接，或者转到主页，以查看处于“需要详细信息”状态的所有报表。

    ![Visual Studio 反馈窗口主页的屏幕截图。 列出了一个反馈项，并使用红色的“需要更多信息”标签进行了标记。](../ide/media/feedback-my-feedback.png)

1. 选择问题报告上的“提供详细信息”链接将导航到新屏幕。 在该屏幕中，可以看到请求的信息。

   ![Visual Studio 反馈窗口的屏幕截图，其中显示 Microsoft 为解决问题而请求的信息。](../ide/media/feedback-need-more-info.png)

1. 可以通过添加注释、附件或记录步骤来提供更多信息。 此体验类似于报告新问题或在对问题进行投票时提供其他信息。

1. 提供额外信息后，发出请求的 Microsoft 工程师会收到相关通知。 如果获取的信息足以开展调查，问题状态随即更改。 否则，工程师会要求提供更多信息。

在“我的反馈”屏幕上可以查看这些请求，以及其他所有“问题”和“建议”  。

## <a name="problem-status"></a>问题状态

报告问题后，可通过状态了解你的提交在其生命周期中所处的位置。 当 Microsoft 团队审核你的反馈时，他们会将其设置为适当的状态。 通过参考下面列出的状态及其含义和颜色指示来跟踪问题报告的进度。

| **State** | **说明**                                                                                                         |
|-------------|-------------------------------------------------------------------------------------------------------------------------|
|  ![开发人员社区上问题报告的“新”状态](../ide/media/ProblemStates/New.jpg)           | “新”表示错误或问题是新报告的，尚未采取任何措施  。                    |
| ![开发人员社区上问题报告的“已会审”状态](../ide/media/ProblemStates/Triaged.jpg)    | “已会审”表示已完成初步步骤，例如审核、翻译和重复项初始检查  。 票证已发送给相应的工程团队以供考虑。                                     |
| ![开发人员社区上问题报告的“正在考虑中”状态](../ide/media/ProblemStates/UnderConsideration.jpg)   | “正在考虑中”表示 Microsoft 正在审核社区影响问题，并会相应地确定其优先级  。 如果社区影响尚不明确或重要，我们将继续监视此状态下的问题。                                                                                           |
| ![开发人员社区上问题报告的“正在调查中”状态](../ide/media/ProblemStates/UnderInvestigation.jpg)    |  “正在调查中”表示工程师正在积极调查你的问题以找到解决方案  。                                                                                           |
|   ![开发人员社区问题报告的“需要更多信息”状态](../ide/media/ProblemStates/NeedMoreInfo.jpg) | “需要更多信息”表示需要你提供更多诊断信息，以便继续进行调查  。  [了解如何对“需要更多信息”请求做出响应。](./how-to-report-a-problem-with-visual-studio.md#when-further-information-is-needed)                                                                                        |
| ![开发人员社区上问题报告的“已有修补程序 - 等待发布”状态](../ide/media/ProblemStates/FixedPendingRelease.jpg)    | “已有修补程序 - 等待发布”表示已有该问题的修补程序，并且即将提供预览版或即将发布  。  当提供修补程序预览版后，问题将被标记为指定预览版本的“已有修补程序版本”标记。 |
| ![开发人员社区上问题报告的“已关闭 - 已有修补程序”状态](../ide/media/ProblemStates/ClosedFixed.jpg)    | “已关闭 - 已有修补程序”表示已针对此问题发布了修补程序  。 该问题现在也标有“已有修补程序版本:”标签，用于指定发布版本。 |
| ![开发人员社区上问题报告的“已关闭 - 重复”状态](../ide/media/ProblemStates/ClosedDuplicate.jpg)    | “已关闭 - 重复”表示你的问题已通过其他反馈进行了报告  。 我们将提供跟踪原始问题报告的链接。 |
| ![开发人员社区上问题报告的“已关闭 - 较低优先级”状态](../ide/media/ProblemStates/ClosedLowerPriority.jpg)    | “已关闭 - 较低优先级”：为了让在开发者社区中的每个人都具备最佳价值，我们会优先考虑客户影响最大的问题  。 虽然我们目前无法解决此特定问题，但请放心，我们会重视你的所有反馈并据此改进 Visual Studio。 |
| ![开发人员社区上问题报告的“已关闭 - 不是一个 Bug”状态](../ide/media/ProblemStates/ClosedNotABug.jpg)    | “已关闭 - 不是一个 Bug”表示已确定报告的功能是基于当前设计  。 |
| ![开发人员社区上问题报告的“已关闭 - 信息不足”状态](../ide/media/ProblemStates/ClosedNotEnoughInfo.jpg)    | “已关闭 - 信息不足”表示我们没有足够的信息来调查此问题  。 获得所需信息后，我们会重新考虑此反馈。 |
| ![开发人员社区上问题报告的“已关闭 - 其他产品”状态](../ide/media/ProblemStates/ClosedOtherProduct.jpg)    | “已关闭 - 其他产品”表示已确定你的问题适用于其他产品  。 请参阅 Microsoft 对外部产品和任何相关链接的注释。 |

## <a name="faq"></a>FAQ

#### <a name="how-can-i-increase-the-chance-of-my-problem-getting-resolved-quickly"></a>如何才能增加问题得到快速解决的可能性？
建议使用搜索来确保尚未报告所要报告的问题。 如果找到与问题相符的现有项目，请关注并对该问题票证进行投票。

提供可以帮助团队重现你所遇问题的所有信息。  此信息包括必要的重现步骤、代码片段、屏幕截图、重现记录、日志文件和其他项目。

#### <a name="how-is-my-feedback-prioritized"></a>我的反馈是如何设置优先级的？
我们从客户那里收集大量有价值的问题。 为了确保我们在开发人员社区中为每个人带来最大价值，我们会优先对社区影响最大的反馈采取措施。

如果我们未亲自回复你的反馈，请相信我们对你的意见深怀感谢。 请放心，你的所有反馈都会传达给合适的团队。

非常感谢你抽出宝贵的时间帮助我们改进 Visual Studio。

#### <a name="what-actions-can-i-take-if-im-not-satisfied-with-the-resolution"></a>如果我对解决方案不满意，可以采取什么行动？
我们的团队会尽力诊断并解决你遇到的任何问题，但有时可能你对我们的建议不完全感到满意。 请在回复中发表对反馈的评论，让我们确切地知道你不满意的地方，我们会尽力确保满足你的需求。

#### <a name="how-will-i-get-notified-of-progress-on-my-feedback"></a>如何获取有关反馈进度的通知？
Microsoft 工程团队将通过对反馈票证添加注释并在票证取得进展时更改票证状态来与你沟通。 监视在票证状态更改时或发布评论时发送的电子邮件通知。  可以在开发人员社区网站上的“配置文件”和“首选项”设置中管理通知的频率。

#### <a name="why-cant-i-add-a-problem-for-visual-studio-ide-on-the-developer-community-website"></a>为什么不能在开发人员社区网站上添加 Visual Studio IDE 问题？
通过 Visual Studio 报告问题可在报告中自动包含诊断信息。 这些信息非常重要，有助于我们的工程师充分理解你的问题并努力解决问题。

通过 Visual Studio 进行报告时，你可轻松与我们共享丰富的诊断信息，例如较大日志文件、故障信息、屏幕截图、重现记录以及其他项目，有助于我们更快地提供更高质量的解决方法。

## <a name="search-for-solutions-or-provide-feedback"></a>搜索解决方案或提供反馈

如果不希望或不能使用 Visual Studio 报告问题，可能 [Visual Studio 开发人员社区](https://developercommunity2.visualstudio.com/search?space=8)页上已报告此问题并且已发布解决方案。

如果没有要报告的问题但希望建议一项功能，也可以在此处提供反馈。 有关详细信息，请参阅[建议一项功能](https://aka.ms/feedback/suggest?space=8)页面。

## <a name="see-also"></a>请参阅

* [开发者社区指南](./developer-community-guidelines.md)
* [报告 Visual Studio for Mac 的问题](/visualstudio/mac/report-a-problem)
* [报告 C++ 问题](/cpp/how-to-report-a-problem-with-the-visual-cpp-toolset)
* [Visual Studio 开发者社区](https://developercommunity.visualstudio.com/home)
* [开发人员社区数据隐私](developer-community-privacy.md)
