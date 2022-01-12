---
title: 教程 2：创建计时数学测验
description: 了解如何构建一个测验，在该测验中，测验对象必须在指定时间内回答四道随机算术题。
ms.custom: SEO-VS-2020
ms.date: 10/16/2019
ms.assetid: d7165d08-ace3-457d-b57d-fb8f80760a6f
ms.topic: tutorial
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 34518774d1580915911a502e4608d1b6e9bb879e
ms.sourcegitcommit: fc874be3fe4637a23997b4ef2d99a2ee9a499581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2021
ms.locfileid: "135517378"
---
# <a name="tutorial-2-create-a-timed-math-quiz"></a>教程 2：创建计时数学测验

在本教程中，您将构建一个测验，在该测验中，测验对象必须在指定时间内回答四道随机算术题。

> [!NOTE]
> 本教程中同时涉及 C# 和 Visual Basic，因此请关注特定于你所用编程语言的信息。

本教程将指导你完成以下任务：

- 使用 <xref:System.Random> 类生成随机数。

- 使用 <xref:System.Windows.Forms.Timer> 控件触发事件，使之在特定时间发生。

- 使用 `if else` 语句控制程序流。

- 使用代码执行基本算术运算。

结束时，除数字不同外，测验应与以下屏幕截图类似：

![包含四个问题的数学测验](../ide/media/express_finishedquiz.png)

## <a name="tutorial-links"></a>教程链接

|Title|说明|
|-----------|-----------------|
|[步骤 1：创建项目并向窗体添加标签](../ide/step-1-create-a-project-and-add-labels-to-your-form.md)|首先创建项目，更改属性并添加 `Label` 控件。|
|[步骤 2：创建随机加法问题](../ide/step-2-create-a-random-addition-problem.md)|创建一道加法题，然后使用 `Random` 类生成随机数。|
|[步骤 3：添加倒计时计时器](../ide/step-3-add-a-countdown-timer.md)|添加一个倒计时计时器，以便对测验进行计时。|
|[步骤 4：添加 CheckTheAnswer() 方法](../ide/step-4-add-the-checktheanswer-parens-method.md)|添加一个方法，用于检查测验对象输入的问题答案是否正确。|
|[步骤 5：为 NumericUpDown 控件添加 Enter 事件处理程序](../ide/step-5-add-enter-event-handlers-for-the-numericupdown-controls.md)|添加事件处理程序，使您的测验更易于进行。|
|[步骤 6：添加减法问题](../ide/step-6-add-a-subtraction-problem.md)|添加一道可生成随机数的减法题，使用计时器并检查答案是否正确。|
|[步骤 7：添加乘法和除法问题](../ide/step-7-add-multiplication-and-division-problems.md)|添加可生成随机数的乘法和除法题，使用计时器并检查答案是否正确。|
|[步骤 8：自定义测验](../ide/step-8-customize-the-quiz.md)|尝试其他功能，例如更改颜色和添加提示。|

## <a name="next-steps"></a>后续步骤

要开始学习本教程，请从[步骤 1：创建项目并向窗体添加标签](../ide/step-1-create-a-project-and-add-labels-to-your-form.md)。

## <a name="see-also"></a>请参阅

* [更多 C# 教程](../get-started/csharp/index.yml)
* [Visual Basic 教程](../get-started/visual-basic/index.yml)
* [C++ 教程](/cpp/get-started/tutorial-console-cpp)