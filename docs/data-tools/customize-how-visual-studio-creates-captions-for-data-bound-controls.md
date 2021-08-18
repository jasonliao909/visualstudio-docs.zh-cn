---
title: 自定义数据绑定控件的标题
description: 自定义Visual Studio为数据绑定控件创建标题。 修改"数据源"窗口的智能字幕行为。 关闭智能字幕。
ms.custom: SEO-VS-2020
ms.date: 11/03/2017
ms.topic: how-to
helpviewer_keywords:
- Label captions, Data Sources window
- smart captions
- captions, data-bound
- Data Sources Window, label captions
ms.assetid: 6d4d15f8-4d78-42fd-af64-779ae98d62c8
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 3a5979fda1e2fcbe8664df7171b1053acebb0506
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122052806"
---
# <a name="customize-how-visual-studio-creates-captions-for-data-bound-controls"></a>自定义 Visual Studio 创建数据绑定控件的标题的方式

将项从"数据源"[](add-new-data-sources.md#data-sources-window)窗口拖动到设计器时，需要特别注意：当发现两个或多个单词连接在一起时，标题标签中的列名将重新格式化为更具可读性的字符串。

::: moniker range="vs-2017"

可以通过在注册表项中设置 **SmartCaptionExpression、SmartCaptionReplacement****和** **SmartCaptionSuffix** 值来自定义创建这些HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Data Designers的方式。

::: moniker-end

::: moniker range=">=vs-2019"

可以通过在注册表项中设置 **SmartCaptionExpression、SmartCaptionReplacement****和** **SmartCaptionSuffix** 值来自定义创建这些HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\16.0\Data Designers的方式。

::: moniker-end

> [!NOTE]
> 创建注册表项之前，此注册表项不存在。

智能字幕由输入到 **SmartCaptionExpression** 值中的正则表达式控制。 添加 **数据设计器** 注册表项会替代控制标题标签的默认正则表达式。 有关正则表达式详细信息，请参阅在 Visual Studio 中使用[正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。

下表描述了控制标题标签的注册表值。

|注册表项|说明|
|-------------------|-----------------|
|**SmartCaptionExpression**|用于匹配模式的正则表达式。|
|**SmartCaptionReplacement**|显示 **SmartCaptionExpression 中匹配的任何组的格式**。|
|**SmartCaptionSuffix**|要追加到标题末尾的可选字符串。|

下表列出了这些注册表值的内部默认设置。

|注册表项|默认值|说明|
|-------------------|-------------------|-----------------|
|**SmartCaptionExpression**|**(\\ \p{Ll})  (\\ \p{Lu}) &#124;_+**|匹配后跟大写字符或下划线的小写字符。|
|**SmartCaptionReplacement**|**$1 $2**|**$1** 表示在表达式的第一个括号中匹配的任何字符 **，$2** 表示第二个括号中匹配的任何字符。 替换项是第一个匹配项、一个空格，然后第二个匹配项。|
|**SmartCaptionSuffix**|**:**|表示追加到返回的字符串的字符。 例如，如果标题为 `Company Name` ，则后缀会使其 `Company Name:`|

> [!CAUTION]
> 在注册表编辑器中执行任何内容时，请非常小心。 在编辑注册表之前对其进行备份。 如果错误地使用注册表编辑器，可能会导致严重问题，这些问题可能需要重新安装操作系统。 Microsoft 不保证不正确地使用注册表编辑器导致的问题能够得到解决。 你自行承担使用注册表编辑器的风险。
>
> 有关备份、编辑和还原注册表的信息，请参阅Windows[用户的注册表信息](https://support.microsoft.com/help/256986/windows-registry-information-for-advanced-users)。

## <a name="modify-the-smart-captioning-behavior-of-the-data-sources-window"></a>修改"数据源"窗口的智能字幕行为

1. 单击"启动"，然后单击 **"运行** "打开命令 **窗口**。

2. 在 `regedit` "运行 **"对话框中键入**，然后单击"确定 **"。**

3. 展开 **"HKEY_CURRENT_USER**  >    >  **Microsoft**  >  **VisualStudio"节点**。

::: moniker range="vs-2017"

4. 右键单击 **15.0** 节点，并创建名为 **的新密钥** `Data Designers` 。

::: moniker-end

::: moniker range=">=vs-2019"

4. 右键单击 **16.0** 节点，并创建名为 **的新密钥** `Data Designers` 。

::: moniker-end

5. 右键单击" **数据设计器"节点** ，然后创建三个新的字符串值：

    - `SmartCaptionExpression`
    - `SmartCaptionReplacement`
    - `SmartCaptionSuffix`

6. 右键单击 **SmartCaptionExpression** 值，然后选择"修改 **"。**

7. 输入希望"数据源"窗口 **使用的** 正则表达式。

8. 右键单击 **SmartCaptionReplacement 值，** 然后选择"修改 **"。**

9. 输入以在正则表达式中显示匹配模式的方式设置格式的替换字符串。

10. 右键单击 **SmartCaptionSuffix** 值，然后选择"修改 **"。**

11. 输入要显示在标题末尾的任何字符。

    下次从"数据源"窗口 **拖动** 项时，会使用提供的新注册表值创建标题标签。

## <a name="turn-off-the-smart-captioning-feature"></a>关闭智能字幕功能

1. 单击"启动"，然后单击 **"运行** "打开命令 **窗口**。

2. 在 `regedit` "运行 **"对话框中键入**，然后单击"确定 **"。**

3. 展开 **"HKEY_CURRENT_USER**  >    >  **Microsoft**  >  **VisualStudio"节点**。

::: moniker range="vs-2017"

4. 右键单击 **15.0** 节点，并创建名为 **的新密钥** `Data Designers` 。

::: moniker-end

::: moniker range=">=vs-2019"

4. 右键单击 **16.0** 节点，并创建名为 **的新密钥** `Data Designers` 。

::: moniker-end

5. 右键单击" **数据设计器"节点** ，然后创建三个新的字符串值：

    - `SmartCaptionExpression`
    - `SmartCaptionReplacement`
    - `SmartCaptionSuffix`

6. 右键单击 **SmartCaptionExpression 项，然后选择**"修改 **"。**

7. 输入 `(.*)` 作为值。 这将匹配整个字符串。

8. 右键单击 **SmartCaptionReplacement 项，然后选择**"修改 **"。**

9. 输入 `$1` 作为值。 这会将字符串替换为匹配的值，即整个字符串，以便它将保持不变。

    下次从"数据源"窗口 **拖动** 项时，会使用未修改的标题创建标题标签。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
