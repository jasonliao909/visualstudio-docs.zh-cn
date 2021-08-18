---
title: 演练：将自定义 XAML 添加到起始页 |Microsoft Docs
description: 了解如何使用本演练创建包含 web 浏览器的自定义 Visual Studio 起始页。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- custom start page
- xaml start page
ms.assetid: 9af4d5f9-1cfc-4221-aea7-c8cd3f7571a6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 748dd9b52dcb92412066242778bb8cff592b5d36b6159241577d47d0cbcc60be
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121334986"
---
# <a name="walkthrough-add-custom-xaml-to-the-start-page"></a>演练：将自定义 XAML 添加到起始页

本演练演示如何创建包含 Web 浏览器的自定义 Visual Studio 起始页。

## <a name="add-custom-xaml"></a>添加自定义 XAML

1. 按照 [创建自定义起始页](../extensibility/creating-a-custom-start-page.md)中的说明创建起始页。

2. 在 *mainwindow.xaml* 文件中，找到 \<Grid> 部分。

3. 在 \<TabControl> 元素内添加元素和 \<TabItem> \< Grid> ，如下面的示例中所示。

    ```xml
    <Grid>
        <TabControl>
            <TabItem Header="Bing" Height="Auto">
                <Frame Source="http://www.bing.com" />
            </TabItem>
        </TabControl>
    </Grid>
    ```

4. 添加第二个 \<TabItem> ，其中包含用于 \<Button> 打开新项目的元素：

    ```xml
    <Grid>
        <TabControl>
            <TabItem Header="MyButton" Height="Auto">
                <Button Name="btnNewProj" Content="New Project"
                    Command="{x:Static vscom:VSCommands.ExecuteCommand}"
                    CommandParameter="File.NewProject" >
                </Button>
            </TabItem>
            <TabItem Header="Bing" Height="Auto">
                <Frame Source="http://www.bing.com" />
            </TabItem>
        </TabControl>
    </Grid>
    ```

## <a name="test-the-custom-start-page"></a>测试自定义起始页

1. 按 **F5**。

     Visual Studio 的实验实例随即打开，并且已安装自定义起始页但未选中。

2. 在 Visual Studio 的实验实例中，打开 **Tools/Options/环境** 页。

3. 选择 " **启动**"。 在 " **自定义起始页** " 列表中，选择您 *的 .xaml* 文件，然后单击 **"确定"**。

4. 在“视图”  菜单上，单击“起始页” 。

5. 单击 "**必应**" 选项卡。

     应该会看到一个必应网页。

6. 单击 " **mybutton.src** " 选项卡。

     应会看到 " **MyProject** " 按钮，该按钮将打开 "**新建 Project** " 对话框。

7. 关闭实验实例。

若要应用自定义起始页，请在 "**工具**  >  **选项**  >  "**环境** 中选择 "**启动**"。 在 " **自定义起始页** " 列表中，选择您 *的 .xaml* 文件，然后单击 **"确定"**。

## <a name="next-steps"></a>后续步骤

Visual Studio 起始页现在包含一个显示 "Web 浏览器" 选项卡和 "mybutton.src" 选项卡的选项卡。可以通过使用 *代码隐藏* 模型添加自定义的 .dll 来创建具有其他功能的自定义起始页，如 [将用户控件添加到起始页](../extensibility/adding-user-control-to-the-start-page.md)中所示。 您可以通过将生成的 .vsix 文件发布到[Visual Studio Marketplace](https://marketplace.visualstudio.com/)网站或其他网站或网络共享来与其他用户共享自定义起始页。 有关更多信息，请参见 [Deploying Custom Start Pages](../extensibility/deploying-custom-start-pages.md)。

## <a name="see-also"></a>请参阅

- [自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)
- [WPF 容器控件](/previous-versions/bb675291(v=vs.110))