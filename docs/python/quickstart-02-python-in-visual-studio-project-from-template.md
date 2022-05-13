---
title: 快速入门 - 使用模板创建 Python 项目
description: 在此快速入门教程中，使用基本 Flask 应用的内置模板创建适合 Python 的 Visual Studio 项目。
ms.date: 05/12/2022
ms.topic: quickstart
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
ms.custom: devdivchpfy22
ms.workload:
- python
- data-science
ms.openlocfilehash: 0b227d0161e0a5b91338c2f6335584fffb112bba
ms.sourcegitcommit: caf5ca17efde4dc4de8b1bdfbe7770f6d705024d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2022
ms.locfileid: "145017674"
---
# <a name="quickstart-create-a-python-project-from-a-template-in-visual-studio"></a>快速入门：从 Visual Studio 中的模板创建 Python 项目

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

[在 Visual Studio 中安装 Python 支持](installing-python-support-in-visual-studio.md)后，就可以使用各种模板轻松创建新的 Python 项目。 在此快速入门教程中，使用模板创建简单的 Flask 应用。 生成的项目与按照[快速入门 - 通过 Flask 创建 Web 应用](../ide/quickstart-python.md)手动创建的项目相似。

::: moniker range="<=vs-2019"

1. 启动 Visual Studio。
1. 在顶部菜单栏中 **，选择“** > **文件新建****Project**”，然后在“**新建** > Project”对话框中搜索“空白Flask **Web Project** 模板，在中间列表中选择一个名称，然后选择 **”确定**“ ：

    :::image type="content" source="media/quickstart-python-06-blank-flask-template.png" alt-text="使用空白Flask Web Project模板创建新项目的屏幕截图。":::

1. Visual Studio 中显示对话框，提示“此项目需要外部包。” 显示此对话框的原因是模板包括指定 Flask 依赖项的 requirements.txt 文件。 Visual Studio 可自动安装包，且让你能够将这些包安装到虚拟环境中。 安装到全局环境时建议使用虚拟环境，因此选择“安装到虚拟环境”继续操作。

    :::image type="content" source="media/quickstart-python-07-install-into-virtual-environment.png" alt-text="将Flask安装到虚拟环境中的屏幕截图。":::

1. Visual Studio 随即显示“添加虚拟环境”对话框。 接受默认设置并选择“创建”，然后同意任意升级请求。

     > [!Tip]
     > 开始一个项目时，强烈建议立即创建虚拟环境，因为大多数 Visual Studio 模板均有此项提示。 在你添加和删除库时，虚拟环境随之保证项目的确切需求。 然后，可轻松生成 requirements.txt 文件。在其他开发计算机上重新安装这些依赖项时使用此文件（因为此时使用源代码管理功能集），将项目部署到生产服务器时也使用此文件。 有关虚拟环境及其优势的详细信息，请参阅[使用虚拟环境](../python/selecting-a-python-environment-for-a-project.md#use-virtual-environments)和[使用 requirements.txt 管理所需的包](../python/managing-required-packages-with-requirements-txt.md)。

1. Visual Studio 创建该环境后，在“解决方案资源管理器”中查看是否已具备 app.py 文件和 requirements.txt。 打开 app.py，可看到模板提供了类似[快速入门 - 使用 Flask 创建 Web 应用](../ide/quickstart-python.md)中的代码，还增添了几个部分。 此处显示的所有代码都由模板创建，因此无需将任何代码粘贴到 *自己 app.py* 。

    代码开始部分为以下必要导入：

    ```python
        from flask import Flask
        app = Flask(__name__)
    ```

    接下来是以下行，它在将应用部署到 Web 主机时非常有用：

    ```python
        wsgi_app = app.wsgi_app
    ```

    然后是路由修饰器，修饰定义视图的简单函数：

    ```python
        @app.route('/')
        def hello():
        """Renders a sample page."""
        return "Hello World!"
    ```

    最后，以下启动代码允许通过环境变量设置主机和端口，而不是硬编码它们。 此类代码可让你轻松控制开发和生产计算机上的配置，而无需更改代码：

    ```python
        if __name__ == '__main__':
        import os
        HOST = os.environ.get('SERVER_HOST', 'localhost')
        try:
        PORT = int(os.environ.get('SERVER_PORT', '5555'))
        except ValueError:
        PORT = 5555
        app.run(HOST, PORT)
    ```

1. 选择 **“调试** > **”"开始"菜单而不调试** 以运行应用并打开浏览器。`localhost:5555`
::: moniker-end

::: moniker range=">=vs-2022"

1. "开始"菜单 Visual Studio并从顶部菜单栏中选择 **“FileNew** >  >  **Project**。 然后在“**新建Project**”对话框中搜索“空白 flask”，从列表中选择 **空白Flask Web Project** 模板，然后选择“**下一步**”。  

     :::image type="content" source="media/vs-2022/quickstart-python-06-blank-flask-template.png" alt-text="使用空白Flask Web Project模板创建新项目的屏幕截图。":::

1. Visual Studio显示项目配置对话框，为项目命名并选择“**创建**”。

     :::image type="content" source="media/vs-2022/quickstart-python-065-blank-flask-project-config.png" alt-text="使用名称和所需位置配置新项目字段的屏幕截图。":::

1. Visual Studio 中显示对话框，提示“此项目需要外部包。” 显示此对话框的原因是模板包括指定 Flask 依赖项的 requirements.txt 文件。 Visual Studio 可自动安装包，且让你能够将这些包安装到虚拟环境中。 安装到全局环境时建议使用虚拟环境，因此选择“安装到虚拟环境”继续操作。

1. Visual Studio 随即显示“添加虚拟环境”对话框。 接受默认设置并选择“创建”，然后同意任意升级请求。

     :::image type="content" source="media/vs-2022/quickstart-python-07-install-into-virtual-environment.png" alt-text="将Flask安装到虚拟环境中的屏幕截图。":::

     > [!Tip]
     > 开始一个项目时，强烈建议立即创建虚拟环境，因为大多数 Visual Studio 模板均有此项提示。 在你添加和删除库时，虚拟环境随之保证项目的确切需求。 然后，可轻松生成 requirements.txt 文件。在其他开发计算机上重新安装这些依赖项时使用此文件（因为此时使用源代码管理功能集），将项目部署到生产服务器时也使用此文件。 有关虚拟环境及其优势的详细信息，请参阅[使用虚拟环境](../python/selecting-a-python-environment-for-a-project.md#use-virtual-environments)和[使用 requirements.txt 管理所需的包](../python/managing-required-packages-with-requirements-txt.md)。

1. Visual Studio 创建该环境后，在“解决方案资源管理器”中查看是否已具备 app.py 文件和 requirements.txt。 打开 app.py，可看到模板提供了类似[快速入门 - 使用 Flask 创建 Web 应用](../ide/quickstart-python.md)中的代码，还增添了几个部分。 此处显示的所有代码都由模板创建，因此无需将任何代码粘贴到 *自己 app.py* 。

    代码开始部分为以下必要导入：

    ```python
    from flask import Flask
    app = Flask(__name__)
    ```

    接下来是以下行，它在将应用部署到 Web 主机时非常有用：

    ```python
        wsgi_app = app.wsgi_app
    ```

    然后是路由修饰器，修饰定义视图的简单函数：

    ```python
        @app.route('/')
        def hello():
        """Renders a sample page."""
        return "Hello World!"
    ```

    下面的启动代码允许通过环境变量设置主机和端口，而不是对其进行硬编码。 此类代码可让你轻松控制开发和生产计算机上的配置，而无需更改代码：

    ```python
        if __name__ == '__main__':
        import os
        HOST = os.environ.get('SERVER_HOST', 'localhost')
        try:
        PORT = int(os.environ.get('SERVER_PORT', '5555'))
        except ValueError:
        PORT = 5555
        app.run(HOST, PORT)
    ```

1. 选择 **“调试** > **”"开始"菜单而不调试** 以运行应用并打开浏览器。`localhost:5555`
::: moniker-end

**问：Visual Studio 还提供哪些 Python 模板？**

**答**：在安装了 Python 工作负载的情况下，Visual Studio 提供多种项目模板，其中包括用于 [Flask、Bottle 和 Django Web 框架](../python/python-web-application-project-templates.md)、Azure 云服务以及不同机器学习方案的模板，甚至还有一个模板用于根据带 Python 应用的现有文件夹结构创建项目。 通过 **FileNew** >  >  访问这些模板 **Project** 对话框，方法是选择 **Python** 语言节点及其子节点。

Visual Studio 还提供各种文件或项模板，用于快速创建 Python 类、Python 包、Python 单元测试、web.config 文件等内容。 如果打开了 Python 项目，可依次单击“项目” > “添加新项”菜单命令来访问项模板。 请参阅[项模板](python-item-templates.md)引用。

使用模板可以在启动项目或创建文件时节省大量时间。 它们也是了解不同应用类型和代码结构的好方法。 最好先花几分钟基于不同模板创建项目和项，熟悉模板的功能。

**问：我还能使用 Cookiecutter 模板吗？**

**答**：能！ 事实上，Visual Studio 提供与 Cookiecutter 的直接集成（详情请参阅[快速入门：使用 Cookiecutter 模板创建项目](../python/quickstart-04-python-in-visual-studio-project-from-cookiecutter.md)）。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [教程：在 Visual Studio 中使用 Python](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

## <a name="see-also"></a>另请参阅

- [手动标识现有 Python 解释器](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)
[在 Windows 上的 Visual Studio 中安装 Python 支持](installing-python-support-in-visual-studio.md#how-to-install-python-support-in-visual-studio-on-windows)
- [Python 工具安装目录](installing-python-support-in-visual-studio.md#install-locations)
