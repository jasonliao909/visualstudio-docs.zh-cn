---
title: 演练：将自定义 XAML 添加到起始页|Microsoft Docs
description: 了解如何使用本Visual Studio创建包含 Web 浏览器的自定义 Web 浏览器起始页。
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
ms.openlocfilehash: 4da513c5040b6da97a9a545b5b40892d8cdc4c30
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122158042"
---
# <a name="walkthrough-add-custom-xaml-to-the-start-page"></a>演练：将自定义 XAML 添加到起始页

本演练演示如何在包含 Web 浏览器Visual Studio自定义浏览器。

## <a name="add-custom-xaml"></a>添加自定义 XAML

1. 按照创建自定义起始页 中的说明 [创建起始页](../extensibility/creating-a-custom-start-page.md)。

2. 在 *MainWindow.xaml* 文件中，找到 \<Grid> 部分。

3. 在 \<TabControl> 元素中添加 \<TabItem> 元素和 \< Grid> ，如以下示例所示。

    ```xml
    <Grid>
        <TabControl>
            <TabItem Header="Bing" Height="Auto">
                <Frame Source="http://www.bing.com" />
            </TabItem>
        </TabControl>
    </Grid>
    ```

4. 添加第二 \<TabItem> 个 ， \<Button> 其元素可打开新项目：

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

     将打开 Visual Studio实例，其中已安装自定义起始页，但未选择该页。

2. 在 Visual Studio 试验实例中，打开"工具 **/选项/环境"** 页。

3. 选择"**启动"。** 在"**自定义起始页"列表中**，选择 *.xaml* 文件，然后单击"确定 **"。**

4. 在“视图”  菜单上，单击“起始页” 。

5. 单击 **"必应** 选项卡。

     应会看到一必应网页。

6. 单击 **"MyButton"** 选项卡。

     应会看到 **"MyProject"** 按钮，这将打开"新建 **Project对话框。**

7. 关闭实验实例。

若要应用自定义起始页，请在"工具选项  >  **环境**"  >  **中选择**"启动 **"。** 在"**自定义起始页"列表中**，选择 *.xaml* 文件，然后单击"确定 **"。**

## <a name="next-steps"></a>后续步骤

此时Visual Studio页包含一个选项卡，该选项卡显示 Web 浏览器选项卡和 MyButton 选项卡。可以使用代码隐藏模型来创建自定义起始页，以添加自定义.dll，如将用户控件添加到起始页[中所示](../extensibility/adding-user-control-to-the-start-page.md)。 可以通过将生成的 .vsix 文件发布到 Visual Studio [Marketplace](https://marketplace.visualstudio.com/)网站或其他网站或网络共享，与其他用户共享自定义起始页。 有关更多信息，请参见 [Deploying Custom Start Pages](../extensibility/deploying-custom-start-pages.md)。

## <a name="see-also"></a>请参阅

- [自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)
- [WPF 容器控件](/previous-versions/bb675291(v=vs.110))