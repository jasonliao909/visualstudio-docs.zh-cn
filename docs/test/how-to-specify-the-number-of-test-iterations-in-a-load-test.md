---
title: 在负载测试运行设置中指定迭代数
description: 了解如何使用负载测试编辑器指定要对负载测试的所有场景中的所有 Web 性能和单元测试运行的迭代次数。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, properties
- load tests, run settings
ms.assetid: 45a625db-b3e7-4d64-beda-b9a76248096d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.openlocfilehash: 3af6b33cb2c611023790f3f70ac4446ac6f99a36
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122092457"
---
# <a name="how-to-specify-the-number-of-test-iterations-in-a-load-test-run-setting"></a>如何：在负载测试运行设置中指定测试迭代数

在用“新建负载测试向导”创建负载测试之后，可以使用“负载测试编辑器”来更改方案属性以满足测试需求和目标   。 有关详细信息，请参阅[演练：创建和运行负载测试](../test/walkthrough-create-and-run-a-load-test.md)。

使用负载测试编辑器，可在“属性”窗口中编辑运行设置值的“测试迭代”属性    。 “测试迭代”  属性使用“负载测试编辑器”  指定要对负载测试的所有方案中的所有 Web 性能测试和单元测试运行的迭代数。

> [!NOTE]
> 有关运行设置属性及其说明的完整列表，请参见[负载测试运行设置属性](../test/load-test-run-settings-properties.md)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-specify-the-number-of-test-iterations-in-a-run-setting"></a>在运行设置中指定测试迭代次数

1. 打开一个负载测试。

     “负载测试编辑器”随即出现并显示负载测试树。 

2. 在负载测试树的“运行设置”文件夹中，选择“运行设置”。 

3. 在“视图”菜单上，选择“属性窗口”以查看负载运行设置的类别和属性。  

4. 将“使用测试迭代”属性设置为 True。  

5. 在“测试迭代”属性中输入一个数字，指示要在负载测试期间运行的测试迭代的次数。 

6. 更改完此属性后，请选择“文件”菜单上的“保存”。   然后，可以使用新的“测试迭代”值运行负载测试。 

## <a name="see-also"></a>另请参阅

- [配置负载测试运行设置](../test/configure-load-test-run-settings.md)
- [负载测试方案属性](../test/load-test-scenario-properties.md)
