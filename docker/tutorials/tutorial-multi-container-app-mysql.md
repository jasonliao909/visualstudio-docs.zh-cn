---
title: 教程：具有 MySQL 和 Docker Compose 的多容器应用
description: 在本教程中，了解如何创建具有 MySQL 和 Docker Compose 的多容器应用。 使用多个容器缩放项目。
author: ucheNkadiCode
ms.author: uchen
ms.prod: vs-code
ms.topic: tutorial
ms.date: 03/04/2022
ms.custom: template-tutorial
ms.openlocfilehash: fd71143bac47f70a2192c9add5559fd4b12e87bb
ms.sourcegitcommit: 71f68518d53d29e892934863ce10ceaa7613a966
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139608507"
---
# <a name="tutorial-create-multi-container-apps-with-mysql-and-docker-compose"></a>教程：创建具有 MySQL 和 Docker Compose 的多容器应用

本教程中，你将学习多容器应用。
通过使用多个容器，可以将容器专用于不同的任务。
每个容器都应执行一项任务，而且应完成得很好。

下面是你可能想要使用多容器应用的一些原因：

- 利用单独的容器，你能够以不同于数据库的方式管理 API 和前端。
- 借助容器，你可使版本和更新版本相互隔离。
- 虽然你可在本地对数据库使用容器，但在生产环境中，你可能需要对数据库使用托管服务。
- 运行多个进程会要求使用进程管理器，这会让容器启动/关闭更加复杂。

你将更新应用程序以使其按图中所述的方式工作。

![图中显示了用一条线连接的两个标记为 Todo App 和 MySQL 的容器。](media/multi-app-architecture.png)

在本教程中，你将了解如何执行以下操作：

> [!div class="checklist"]
> - 启动 MySQL。
> - 使用 MySQL 运行应用。
> - 创建 Compose 文件。
> - 运行应用程序堆栈。

## <a name="prerequisites"></a>先决条件

本教程将继续学习一系列教程，从[使用 Visual Studio Code 创建和共享 Docker 应用](docker-tutorial.md)开始。
从该教程开始，其中包括先决条件。
然后学习以下教程：

- [永久保存数据和层 Docker 应用](tutorial-persist-data-layer-docker-app-with-vscode.md)。
- [将 Docker 应用部署到 Azure 云](tutorial-deploy-docker-app-azure.md)。

还需要以下项：

- [Docker Compose](https://docs.docker.com/compose/)。

  适用于 Windows 或 Mac 的 Docker Desktop，包括 Docker Compose。
  运行以下命令以进行验证：

  ```bash
  docker-compose version
  ```

  如果使用 Linux 操作系统，请[安装 Docker Compose](https://docs.docker.com/compose/install/)。

与前面的教程一样，可以从 VS Code“资源管理器”视图或“DOCKER”视图完成大部分任务 。
可以选择“终端” > “新建终端”，在 VS Code 中打开命令行窗口 。
还可以在 Bash 窗口中运行命令。
除非指定，否则任何标记为 Bash 的命令都可以在 Bash 窗口或 VS Code 终端中运行。

## <a name="start-mysql"></a>启动 MySQL

默认情况下，容器以隔离方式运行。
它们对同一台计算机上的其他进程或容器一无所知。
若要允许容器间进行通信，请使用网络。

如果两个容器在同一网络上，那么它们可彼此通信。
如果没在同一网络上，则没法通信。

有两种方法可将容器放在网络上：在启动时进行分配，或者连接现有容器。
在此示例中，先创建网络，然后在启动时附加 MySQL 容器。

1. 使用此命令创建网络。

   ```bash
   docker network create todo-app
   ```

1. 启动 MySQL 容器并将它附加到网络。

    ```bash
    docker run -d 
        --network todo-app --network-alias mysql 
        -v todo-mysql-data:/var/lib/mysql 
        -e MYSQL_ROOT_PASSWORD=<your-password> 
        -e MYSQL_DATABASE=todos 
        mysql:5.7
    ```

   此命令还定义了环境变量。
   有关详细信息，请参阅 [MySQL Docker Hub 列表](https://hub.docker.com/_/mysql/)。

   该命令指定了网络别名 `mysql`。

1. 使用 `docker ps` 命令获取容器 ID。

1. 若要确认你已启动并运行数据库，请连接到该数据库。

   ```bash
   docker exec -it <mysql-container-id> mysql -p
   ```

   在出现提示时，输入所使用的密码。

1. 在 MySQL shell 中，列出数据库并验证确保你看见 `todos` 数据库。

   ```sql
   SHOW DATABASES;
   ```

   你会看到以下输出。

   ```output
   +--------------------+
   | Database           |
   +--------------------+
   | information_schema |
   | mysql              |
   | performance_schema |
   | sys                |
   | todos              |
   +--------------------+
   5 rows in set (0.00 sec)
   ```

## <a name="run-your-app-with-mysql"></a>使用 MySQL 运行应用

待办事项应用支持设置环境变量来指定 MySQL 连接设置。

- `MYSQL_HOST` MySQL 服务器的主机名。
- `MYSQL_USER` 要用于连接的用户名。
- `MYSQL_PASSWORD` 要用于连接的密码。
- `MYSQL_DB` 连接后要使用的数据库。

> [!WARNING]
> 对于开发，可以使用环境变量来设置连接设置。
> 在生产环境中运行应用程序时，不建议采用此做法。
> 有关详细信息，请参阅[为何不该对机密数据使用环境变量](https://diogomonica.com/2017/03/27/why-you-shouldnt-use-env-variables-for-secret-data/)。
>
> 更安全的机制是使用容器编排框架提供的机密支持。
> 在大多数情况下，这些机密作为文件装载到正在运行的容器中。
>

此过程会启动应用，并将该容器连接到 MySQL 容器。

1. 使用以下 docker run 命令。
   该命令指定上面的环境变量。

    ```bash
    docker run -dp 3000:3000 
      -w /app -v ${PWD}:/app 
      --network todo-app 
      -e MYSQL_HOST=mysql 
      -e MYSQL_USER=root 
      -e MYSQL_PASSWORD=<your-password> 
      -e MYSQL_DB=todos 
      node:12-alpine 
      sh -c "yarn install && yarn run dev"
    ```

1. 在 VS Code 的 Docker 视图中，右键单击应用容器，然后选择“查看日志”。
   若要从命令行查看日志，请使用 `docker logs` 命令。

   结果中包含一行，指示该应用已连接到 MySQL 数据库。

   ```output
   # Previous log messages omitted
   $ nodemon src/index.js
   [nodemon] 1.19.2
   [nodemon] to restart at any time, enter `rs`
   [nodemon] watching dir(s): *.*
   [nodemon] starting `node src/index.js`
   Connected to mysql db at host mysql
   Listening on port 3000
   ```

1. 在浏览器中输入 `http://localhost:3000`。
   将一些项添加到待办事项列表中。

1. 按上一部分中的相同方式连接到 MySQL 数据库。
   运行此命令可验证是否正在向数据库写入项。

   ```bash
   docker exec -ti <mysql-container-id> mysql -p todos
   ```

   在 MySQL shell 中，运行以下命令。

   ```sql
   select * from todo_items;
   ```

   结果将类似于以下输出。

   ```output
   +--------------------------------------+--------------------+-----------+
   | id                                   | name               | completed |
   +--------------------------------------+--------------------+-----------+
   | c906ff08-60e6-44e6-8f49-ed56a0853e85 | Do amazing things! |         0 |
   | 2912a79e-8486-4bc3-a4c5-460793a575ab | Be awesome!        |         0 |
   +--------------------------------------+--------------------+-----------+
   ```

此时，拥有一个将数据存储在外部数据库中的应用程序。
该数据库在单独的容器中运行。
你已学习了容器网络。

## <a name="create-a-docker-compose-file"></a>创建 Docker Compose 文件

Docker Compose 有助于定义和共享多容器应用程序。
使用 Docker Compose，你可以创建用于定义服务的文件。
使用单个命令，可以启动所有内容，也可以将其全部销毁。

可以在文件中定义应用程序堆栈，并将该文件保存在项目存储库的根目录下，受版本控制。
利用此方法，其他人也可以参与你的项目。
他们只需克隆你的存储库。

1. 在应用项目的根目录中，创建名为 `docker-compose.yml` 的文件。

1. 在 Compose 文件中，首先定义架构版本。

   ```yaml
   version: "3.7"
   ```

   在大多数情况下，最好使用支持的最新版本。
   有关当前架构版本和兼容性矩阵，请参阅 [Compose 文件](https://docs.docker.com/compose/compose-file/)。

1. 定义要作为应用程序的一部分运行的服务（或容器）列表。

    ```yaml hl_lines="3"
    version: "3.7"

    services:
    ```

   > [!TIP]
   > 缩进在 .yml 文件中非常重要。
   > 如果要在 VS Code 中进行编辑，Intellisense 会指示错误。

1. 下面是用于应用容器的命令。
   将此信息添加到 .yml 文件。

   ```bash
   docker run -dp 3000:3000 
     -w /app -v ${PWD}:/app 
     --network todo-app 
     -e MYSQL_HOST=mysql 
     -e MYSQL_USER=root 
     -e MYSQL_PASSWORD=<your-password> 
     -e MYSQL_DB=todos 
     node:12-alpine 
     sh -c "yarn install && yarn run dev"
   ```

   定义容器的服务项和映像。

   ```yaml
   version: "3.7"

   services:
     app:
       image: node:12-alpine
   ```

   你可为服务选择任何名称。
   该名称会自动成为网络别名，这在定义 MySQL 服务时非常有用。

1. 添加命令。

    ```yaml
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
    ```

1. 指定用于服务的端口，该端口对应于上述命令中的 `-p 3000:3000`。

    ```yaml
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
    ```

1. 指定工作目录和卷映射

    ```yaml
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
        working_dir: /app
        volumes:
          - ./:/app
    ```

   在 Docker Compose 卷定义中，你可以使用当前目录中的相对路径。

1. 指定环境变量定义。

    ```yaml
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
        working_dir: /app
        volumes:
          - ./:/app
        environment:
          MYSQL_HOST: mysql
          MYSQL_USER: root
          MYSQL_PASSWORD: <your-password>
          MYSQL_DB: todos
    ```

1. 添加 MySQL 服务的定义。
   下面是你在上面所使用的命令：

   ```bash
   docker run -d 
     --network todo-app --network-alias mysql 
     -v todo-mysql-data:/var/lib/mysql 
     -e MYSQL_ROOT_PASSWORD=<your-password> 
     -e MYSQL_DATABASE=todos 
     mysql:5.7
   ```

   定义新服务，并将其命名为 mysql。
   在 `app` 定义后以相同的缩进级别添加文本。

    ```yaml hl_lines="6 7"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
    ```

   该服务会自动获取网络别名。
   指定要使用的映像。

1. 定义卷映射。

   使用与 `services:` 相同级别的 `volumes:` 部分指定卷。
   在映像下指定卷映射。

    ```yaml
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
        volumes:
          - todo-mysql-data:/var/lib/mysql
    
    volumes:
      todo-mysql-data:
    ```

1. 指定环境变量。

    ```yaml
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
        volumes:
          - todo-mysql-data:/var/lib/mysql
        environment: 
          MYSQL_ROOT_PASSWORD: <your-password>
          MYSQL_DATABASE: todos
    
    volumes:
      todo-mysql-data:
    ```

此时，完整的 `docker-compose.yml` 如下所示：

```yaml
version: "3.7"

services:
  app:
    image: node:12-alpine
    command: sh -c "yarn install && yarn run dev"
    ports:
      - 3000:3000
    working_dir: /app
    volumes:
      - ./:/app
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: <your-password>
      MYSQL_DB: todos

  mysql:
    image: mysql:5.7
    volumes:
      - todo-mysql-data:/var/lib/mysql
    environment: 
      MYSQL_ROOT_PASSWORD: <your-password>
      MYSQL_DATABASE: todos

volumes:
  todo-mysql-data:
```

## <a name="run-the-application-stack"></a>运行应用程序堆栈

现在，已拥有 `docker-compose.yml` 文件，请试运行看看。

1. 确保应用和数据库的其他副本未运行。
   在 Docker 扩展中，右键单击任何正在运行的容器，然后选择“移除”。
   或者，在命令行中，使用 `docker rm` 命令，如前面的示例所示。

1. 在“VS Code 资源管理器”中，右键单击 docker-compose.yml，然后选择“Compose Up”。
   或者，在命令行中，使用此 docker 命令。

   ```bash
   docker-compose up -d
   ```

   利用参数 `-d`，可使命令在后台运行。

   你应该看到类似于以下结果的输出。

   ```output
   Creating network "app_default" with the default driver
   Creating volume "app_todo-mysql-data" with default driver
   Creating app_app_1   ... done
   Creating app_mysql_1 ... done
   ```

   已创建卷以及网络。
   默认情况下，Docker Compose 会专门为应用程序堆栈创建网络。

1. 在 Docker 扩展中，右键单击应用容器，然后选择“查看日志”。
   若要从命令行查看日志，请使用 `docker logs` 命令。

   ```output
   mysql_1  | 2019-10-03T03:07:16.083639Z 0 [Note] mysqld: ready for connections.
   mysql_1  | Version: '5.7.27'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server (GPL)
   app_1    | Connected to mysql db at host mysql
   app_1    | Listening on port 3000
   ```

   来自每个服务的日志交汇形成一个流。
   通过此行为，可以监视与时间相关的问题。

   服务名称显示在行的开头，以帮助区分消息。
   若要查看特定服务的日志，可以将服务名称添加到日志命令的末尾。

1. 此时，你应能够打开应用。
   在浏览器中输入 `http://localhost:3000`。

使用完这些容器后，可以简单地将它们全部移除。

- 在“VS Code 资源管理器”中，右键单击 docker-compose.yml，然后选择“Compose Down” 。
- 在命令行上，运行 `docker-compose down`。

容器停止。
网络已移除。

默认情况下，不会移除 compose 文件中已命名的卷。
如果要移除卷，请运行 `docker-compose down --volumes`。

## <a name="clean-up-resources"></a>清理资源

你在本系列教程中使用的先决条件可用于未来的 Docker 开发。
无需删除或卸载任何内容。

## <a name="next-steps"></a>后续步骤

在本教程中，你学习了多容器应用和 Docker Compose。
Docker Compose 有助于显著简化多服务应用程序的定义和共享。

下面是一些可能对你有用的资源：

- [Docker Cloud Integration](https://github.com/docker/compose-cli)
- [示例](https://github.com/docker/awesome-compose)
