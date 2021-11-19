---
title: 自定义数据绑定控件的标题
description: 自定义 Visual Studio 创建数据绑定控件的标题的方式。 修改“数据源”窗口的智能标题行为。 关闭智能标题。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601177"
---
# <a name="customize-how-visual-studio-creates-captions-for-data-bound-controls"></a>自定义 Visual Studio 创建数据绑定控件的标题的方式

将项从[数据源](add-new-data-sources.md#data-sources-window)窗口拖到设计器上时，需要特别注意：在发现两个或更多个单词连接在一起时，标题标签中的列名将重新格式化为一个可读性更强的字符串。

::: moniker range="vs-2017"

可以通过在 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Data Designers 注册表项中设置 SmartCaptionExpression、SmartCaptionReplacement 和 SmartCaptionSuffix 值来自定义创建标签的方式   。

::: moniker-end

::: moniker range=">=vs-2019"

可以通过在 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\16.0\Data Designers 注册表项中设置 SmartCaptionExpression、SmartCaptionReplacement 和 SmartCaptionSuffix 值来自定义创建标签的方式   。

::: moniker-end

> [!NOTE]
> 在创建此注册表项之前，此注册表项不存在。

智能标题由输入到 SmartCaptionExpression 值的正则表达式控制。 添加“数据设计器”注册表项会替代控制标题标签的默认正则表达式。 有关正则表达式的详细信息，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。

下表介绍了控制标题标签的注册表值。

|注册表项|说明|
|-------------------|-----------------|
|**SmartCaptionExpression**|用于匹配模式的正则表达式。|
|**SmartCaptionReplacement**|显示在 SmartCaptionExpression 中匹配的所有组的格式。|
|**SmartCaptionSuffix**|追加到标题末尾的可选字符串。|

下表列出了这些注册表值的内部默认设置。

|注册表项|默认值|说明|
|-------------------|-------------------|-----------------|
|**SmartCaptionExpression**|**(\\\p{Ll})(\\\p{Lu})&#124;_+**|匹配后接大写字符或下划线小写字符。|
|**SmartCaptionReplacement**|**$1 $2**|$1 表示在表达式的第一个括号中匹配的任何字符，$2 表示在第二个括号中匹配的任何字符 。 替换为第一个匹配项、一个空格，然后是第二个匹配项。|
|**SmartCaptionSuffix**|**:**|表示追加到返回的字符串的字符。 例如，如果标题是 `Company Name` ，则后缀会使其为 `Company Name:`|

> [!CAUTION]
> 在注册表编辑器中执行任何操作时都要格外小心。 在编辑注册表之前对其进行备份。 如果注册表编辑器使用不当，则可能会产生严重问题，导致重新安装操作系统。 Microsoft 不保证不正确使用注册表编辑器所引起的问题能够得到解决。 你自行承担使用注册表编辑器的风险。
>
> 有关备份、编辑和还原注册表的信息，请参阅[适用于高级用户的 Windows 注册表信息](https://support.microsoft.com/help/256986/windows-registry-information-for-advanced-users)。

## <a name="modify-the-smart-captioning-behavior-of-the-data-sources-window"></a>修改“数据源”窗口的智能标题行为

1. 单击“启动”，然后单击“运行”打开命令窗口 。

2. 在“运行”对话框中键入 `regedit`，然后单击“确定” 。

3. 展开“HKEY_CURRENT_USER > 软件 > Microsoft > VisualStudio”节点   。

::: moniker range="vs-2017"

4. 右键单击 15.0 节点，并创建名为的新密钥 `Data Designers` 。

::: moniker-end

::: moniker range=">=vs-2019"

4. 右键单击 16.0 节点，并创建名为的新密钥 `Data Designers` 。

::: moniker-end

5. 右键单击“数据设计器”节点，然后创建三个新的字符串值：

    - `SmartCaptionExpression`
    - `SmartCaptionReplacement`
    - `SmartCaptionSuffix`

6. 右键单击 SmartCaptionExpression 值，然后选择“修改” 。

7. 输入希望“数据源”窗口使用的正则表达式。

8. 右键单击 SmartCaptionReplacement 值，然后选择“修改” 。

9. 输入以在正则表达式中显示匹配模式的方式设置格式的替换字符串。

10. 右键单击 SmartCaptionSuffix 值，然后选择“修改” 。

11. 输入要在标题末尾显示的任何字符。

    下一次从“数据源”窗口拖动项时，将使用提供的新注册表值创建标题标签。

## <a name="turn-off-the-smart-captioning-feature"></a>关闭智能标题功能

1. 单击“启动”，然后单击“运行”打开命令窗口 。

2. 在“运行”对话框中键入 `regedit`，然后单击“确定” 。

3. 展开“HKEY_CURRENT_USER > 软件 > Microsoft > VisualStudio”节点   。

::: moniker range="vs-2017"

4. 右键单击 15.0 节点，并创建名为的新密钥 `Data Designers` 。

::: moniker-end

::: moniker range=">=vs-2019"

4. 右键单击 16.0 节点，并创建名为的新密钥 `Data Designers` 。

::: moniker-end

5. 右键单击“数据设计器”节点，然后创建三个新的字符串值：

    - `SmartCaptionExpression`
    - `SmartCaptionReplacement`
    - `SmartCaptionSuffix`

6. 右键单击 SmartCaptionExpression 项，然后选择“修改” 。

7. 输入 `(.*)` 作为值。 这将匹配整个字符串。

8. 右键单击 SmartCaptionReplacement 项，然后选择“修改” 。

9. 输入 `$1` 作为值。 这会将字符串替换为匹配的值，即整个字符串，因此它将保持不变。

    下一次从“数据源”窗口拖动项时，将使用未经修改的标题创建标题标签。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
