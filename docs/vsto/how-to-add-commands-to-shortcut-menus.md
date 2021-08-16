---
title: 如何：向快捷菜单添加命令
description: 了解如何使用外接程序将命令添加到 Office 应用程序中的VSTO菜单。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office menus, creating
- Office development in Visual Studio, context menus
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: a85b45dbe8ffd616b89078795f0cd9ffe11da7fd97e92339dab8ed2162ae2d2f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121424200"
---
# <a name="how-to-add-commands-to-shortcut-menus"></a>如何：向快捷菜单添加命令
  本主题演示如何使用外接程序将命令添加到 Office 应用程序中的VSTO菜单。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

### <a name="to-add-commands-to-shortcut-menus-in-office"></a>将命令添加到 Office 的快捷菜单中

1. 将“功能区 XML”  项添加到文档级项目或 VSTO 外接程序项目中。 有关详细信息，请参阅 [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。 在

2. 在“解决方案资源管理器”中，选择“”  或“” 。

3. 在菜单栏上，选择“视图” > “代码”。

     “ThisAddin”  类文件随即在代码编辑器中打开。

4. 将下面的代码添加到 **ThisAddin** 类中。 此代码可替代 `CreateRibbonExtensibilityObject` 方法，并将功能区 XML 类返回到 Office 应用程序。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_menus.cs/thisaddin.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_menus.vb/thisaddin.vb" id="Snippet1":::

5. 在“解决方案资源管理器” 中，选择功能区 XML 文件。 默认情况下，功能区 XML 文件名为 *Ribbon1.xml。*

6. 在菜单栏上，选择“视图” > “代码”。

     功能区 XML 文件随即在代码编辑器中打开。

7. 在代码编辑器中添加 XML，该 XML 描述快捷菜单以及要添加到快捷菜单的控件。

     下面的示例将向 Word 文档的快捷菜单添加按钮、菜单和库控件。 此快捷菜单的控件 ID 是 ContextMenuText。 有关 2010 Office控件 ID 的完整列表，请参阅[Office 2010](https://www.microsoft.com/download/details.aspx?id=6627)帮助文件：Office Fluent 用户界面控件标识符 。

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <customUI xmlns="http://schemas.microsoft.com/office/2009/07/customui">
      <contextMenus>
        <contextMenu idMso="ContextMenuText">
          <button id="MyButton" label="My Button" insertBeforeMso="HyperlinkInsert" onAction="GetButtonID" />
          <menu id="MySubMenu" label="My Submenu" >
            <button id="MyButton2" label="Button on submenu" />
          </menu>
          <gallery id="galleryOne" label="My Gallery">
            <item id="item1" imageMso="HappyFace" />
            <item id="item2" imageMso="HappyFace" />
            <item id="item3" imageMso="HappyFace" />
            <item id="item4" imageMso="HappyFace" />
          </gallery>
        </contextMenu>
      </contextMenus>
    </customUI>
    ```

8. 在“解决方案资源管理器” 中，选择“MyRibbon.cs”  或“MyRibbon.vb” 。

9. 为要处理的每个 `Ribbon1` 控件将回调方法添加到 类。

     下面的回叫方法将处理“我的按钮”  按钮。 此代码会在光标当前位置向活动文档添加一个字符串。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_menus.vb/ribbon1.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_menus.cs/ribbon1.cs" id="Snippet2":::

## <a name="see-also"></a>请参阅
- [OfficeUI 自定义](../vsto/office-ui-customization.md)
- [演练：为书签创建快捷菜单](../vsto/walkthrough-creating-shortcut-menus-for-bookmarks.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
- [自定义 2010 Office中的上下文菜单](/previous-versions/office/developer/office-2010/ee691832(v=office.14))
