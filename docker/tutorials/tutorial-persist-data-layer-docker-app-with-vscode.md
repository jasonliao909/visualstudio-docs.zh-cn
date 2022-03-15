---
title: 教程：在 VS Code 中使用卷在容器应用中永久保存数据
description: 本教程介绍如何永久保存数据，如何使用绑定装载，以及如何使用 VS Code 分层 (Yarn) 应用。
author: ucheNkadiCode
ms.author: uchen
ms.prod: vs-code
ms.topic: tutorial
ms.date: 03/04/2022
ms.custom:
- template-tutorial
- contperf-fy22q3
ms.openlocfilehash: 004e26bc87106bcfd6899ca06acf5975f6469cda
ms.sourcegitcommit: 5b2c3a2c5f22e0cd6d35aab6049c1f61c4916e74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2022
ms.locfileid: "139852186"
---
# <a name="tutorial-persist-data-in-a-container-app-using-volumes-in-vs-code"></a>教程：在 VS Code 中使用卷在容器应用中永久保存数据

在本教程中，你将学习如何在容器应用程序中永久保存数据。
运行或更新它时，数据仍然可用。
可使用两种主要类型的卷来永久保存数据。
本教程重点介绍已命名的卷。

此外，还将介绍绑定装载，它控制主机上的确切装载点。
可以使用绑定装载来永久保存数据，但也可以使用它来将更多数据添加到容器中。
在处理应用程序时，你可以使用绑定装载将源代码装载到容器中，以使其查看代码更改、做出响应并让你立即看到更改。

本教程还介绍了映像分层、层缓存和多阶段生成。

本教程介绍如何执行下列操作：

> [!div class="checklist"]
> - 了解容器中的数据。
> - 使用已命名的卷永久保存数据。
> - 使用绑定装载。
> - 查看映像层。
> - 缓存依赖项。
> - 了解多阶段生成。

## <a name="prerequisites"></a>先决条件

本教程将继续学习上一个教程，即[使用 Visual Studio Code 创建和共享 Docker 应用](docker-tutorial.md)。
从该教程开始，其中包括先决条件。

## <a name="understand-data-across-containers"></a>了解容器中的数据

在本部分中，将启动两个容器，并在每个容器中各创建一个文件。
在一个容器中创建的文件不能在另一个容器中使用。

1. 使用以下命令启动 `ubuntu` 容器：

   ```bash
   docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"
   ```

   此命令使用 `&&` 启动对两个命令的调用。
   第一部分会选取一个随机数字，并将其写入 `/data.txt`。
   第二个命令监视文件以使容器保持运行。

1. 在 VS Code 的“Docker”区域中，右键单击 ubuntu 容器，然后选择“附加 Shell” 。

   ![屏幕截图显示 Docker 扩展，其中选择了容器，并且在上下文菜单中选择了“附加 Shell”。](media/attach_shell.png)

   随即会打开在 Ubuntu 容器中运行 shell 的终端。

1. 运行以下命令，查看 `/data.txt` 文件的内容。

   ```bash
   cat /data.txt
   ```

   该终端显示 1 到 1000 之间的数字。

   若要使用命令行查看此结果，请使用 `docker ps` 命令获取容器 ID，并运行以下命令。

   ```bash
   docker exec <container-id> cat /data.txt
   ```

1. 启用另一个 `ubuntu` 容器。

   ```bash
   docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"
   ```

1. 使用此命令来查看文件夹内容。

   ```bash
   docker run -it ubuntu ls /
   ```

   该文件夹内应不包含 `data.txt` 文件，因为它只写入第一个容器的暂存空间。

1. 选择这两个 Ubuntu 容器。 右键单击并选择“移除”。
   在命令行中，可以使用 `docker rm -f` 命令移除它们。

## <a name="persist-your-todo-data-using-named-volumes"></a>使用已命名的卷永久保存待办事项数据

默认情况下，待办事项应用将其数据存储在 [SQLite 数据库](https://www.sqlite.org/index.html) (`/etc/todos/todo.db`) 中。
SQLite 数据库是关系数据库，它将数据存储为单个文件。
此方法适用于小型项目。

可以在主机上永久保存单个文件。
将其提供给下一个容器时，应用程序可以从中断处继续。
通过创建卷并将其附加或装载到存储数据的目录，可永久保存数据。
容器会写入 todo.db 文件，并数据永久保存在卷中的主机上。

对于此部分，请使用已命名的卷。
Docker 维护磁盘上卷的物理位置。
参考卷的名称，Docker 会提供正确的数据。

1. 使用 `docker volume create` 命令创建卷。

   ```bash
   docker volume create todo-db
   ```

1. 在“容器”下，选择“入门”并右键单击 。 选择“停止”以停止应用容器。

   若要从命令行停止容器，请使用 `docker stop` 命令。

1. 使用以下命令启动“getting-started”容器。

   ```bash
   docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started
   ```

   卷参数指定要装载的卷和位置 `/etc/todos`。

1. 刷新浏览器以重新加载应用。
   如果已关闭浏览器窗口，请转到 `http://localhost:3000/`。
   将一些项添加到待办事项列表中。

   ![屏幕截图显示了示例应用，其中向列表中添加了多个项。](media/items-added.png)

1. 移除待办事项应用的“getting-started”容器。
   右键单击“Docker”区域中的容器，然后选择“移除”或使用 `docker stop` 和 `docker rm` 命令。

1. 使用相同命令启动新容器：

   ```bash
   docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started
   ```

   此命令装载与之前相同的驱动器。
   刷新浏览器。
   已添加的项仍在列表中。

1. 再次移除“getting-started”容器。

下面介绍的已命名的卷和绑定装载是默认 Docker 引擎安装支持的主要卷类型。

| 属性 | 命名卷 | 绑定挂载 |
| -------- | ------------- | ----------- |
| 主机位置 | Docker 选择 | 由你控制 |
| 装载示例（使用 `-v`） | my-volume:/usr/local/data | /path/to/data:/usr/local/data |
| 使用容器内容填充新卷 | 是 | 否 |
| 支持卷驱动程序 | 是 | 否 |

有许多卷驱动程序插件可用于支持 NFS、SFTP、NetApp 等。
这些插件对于在群集环境（如 Swarm 或 Kubernetes）中的多个主机上运行容器尤其重要。

如果你想知道 Docker 实际存储数据的位置，请运行以下命令。

```bash
docker volume inspect todo-db
```

查看输出，类似于以下结果。

```output
[
    {
        "CreatedAt": "2019-09-26T02:18:36Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/todo-db/_data",
        "Name": "todo-db",
        "Options": {},
        "Scope": "local"
    }
]
```

`Mountpoint` 是实际存储数据的位置。
在大多数计算机上，需要具有根访问权限才能从主机访问此目录。

## <a name="use-bind-mounts"></a>使用绑定装载

使用绑定装载，你可以控制主机上的确切装载点。
此方法可永久保存数据，但通常用于向容器提供更多数据。
可以使用绑定装载将源代码装载到容器中，以使其查看代码更改、做出响应并让你立即看到更改。

若要运行容器以支持开发工作流，请执行以下步骤：

1. 移除所有 `getting-started` 容器。

1. 在 `app` 文件夹中，运行以下命令。

   ```bash
   docker run -dp 3000:3000 -w /app -v ${PWD}:/app node:12-alpine sh -c "yarn install && yarn run dev"
   ```

   此命令包含以下参数。

   - `-dp 3000:3000` 与以前相同。 在分离模式下运行并创建端口映射。
   - `-w /app` 容器内的工作目录。
   - `-v ${PWD}:/app"` 将当前目录从容器中的主机绑定装载到 `/app` 目录。
   - `node:12-alpine` 要使用的映像。 此映像是 Dockerfile 中应用的基本映像。
   - `sh -c "yarn install && yarn run dev"` 一个命令。 它使用 `sh` 启动 shell，并运行 `yarn install` 来安装所有依赖项。 然后它会运行 `yarn run dev`。 如果你查看 `package.json`，将看到 `dev` 脚本正在启动 `nodemon`。

1. 可以使用 `docker logs` 来查看日志。

   ```bash
   docker logs -f <container-id>
   ```

   ```output
   $ nodemon src/index.js
   [nodemon] 1.19.2
   [nodemon] to restart at any time, enter `rs`
   [nodemon] watching dir(s): *.*
   [nodemon] starting `node src/index.js`
   Using sqlite database at /etc/todos/todo.db
   Listening on port 3000
   ```

   看到此列表中的最后一个条目时，应用正在运行。

   查看完日志后，在终端窗口中选择任意键，或在外部窗口中选择Ctrl+C 。

1. 在 VS Code 中，打开 src/static/js/app.js。 更改第 109 行的“添加项”按钮的文本。

   ```diff
   - {submitting ? 'Adding...' : 'Add Item'}
   + {submitting ? 'Adding...' : 'Add'}
   ```

   保存所做更改。

1. 刷新浏览器。 你应该会看到更改。

   ![屏幕截图显示了按钮上具有新文本的示例应用。](media/updated-add-button.png)

## <a name="view-image-layers"></a>查看映像层

你可以查看构成映像的层。
运行 `docker image history` 命令，查看用于创建映像的每个层的命令。

1. 使用 `docker image history`，查看在本教程前面部分创建的 getting-started 映像中的层。

   ```bash
   docker image history getting-started
   ```

   结果应该类似于下面的输出。

   ```plaintext
   IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
   a78a40cbf866        18 seconds ago      /bin/sh -c #(nop)  CMD ["node" "/app/src/ind…   0B                  
   f1d1808565d6        19 seconds ago      /bin/sh -c yarn install --production            85.4MB              
   a2c054d14948        36 seconds ago      /bin/sh -c #(nop) COPY dir:5dc710ad87c789593…   198kB               
   9577ae713121        37 seconds ago      /bin/sh -c #(nop) WORKDIR /app                  0B                  
   b95baba1cfdb        13 days ago         /bin/sh -c #(nop)  CMD ["node"]                 0B                  
   <missing>           13 days ago         /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…   0B                  
   <missing>           13 days ago         /bin/sh -c #(nop) COPY file:238737301d473041…   116B                
   <missing>           13 days ago         /bin/sh -c apk add --no-cache --virtual .bui…   5.35MB              
   <missing>           13 days ago         /bin/sh -c #(nop)  ENV YARN_VERSION=1.21.1      0B                  
   <missing>           13 days ago         /bin/sh -c addgroup -g 1000 node     && addu…   74.3MB              
   <missing>           13 days ago         /bin/sh -c #(nop)  ENV NODE_VERSION=12.14.1     0B                  
   <missing>           13 days ago         /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B                  
   <missing>           13 days ago         /bin/sh -c #(nop) ADD file:e69d441d729412d24…   5.59MB   
   ```

   每一行表示映像中的一个层。
   底部显示的是基本输出，顶部显示的是最新的输出。
   使用此信息，可以查看每个层的大小，帮助诊断大型映像的问题。

1. 其中几行被截断。 如果添加 `--no-trunc` 参数，将获得完整输出。

   ```bash
   docker image history --no-trunc getting-started
   ```

## <a name="cache-dependencies"></a>缓存依赖项

层发生更改后，还必须重新创建所有下游层。
下面还是 Dockerfile：

```dockerfile
FROM node:12-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "/app/src/index.js"]
```

Dockerfile 中的每个命令都会成为映像中的新层。
若要最大程度地减少层，可以重新构建 Dockerfile 以支持缓存依赖项。
对于基于节点的应用程序，这些依赖项在 `package.json` 文件中定义。

方法是先仅复制该文件，安装依赖项，然后再复制其他所有内容。
该过程仅在 `package.json` 发生更改时重新创建 yarn 依赖项。

1. 先更新要在 `package.json` 中复制的 Dockerfile，安装依赖项，然后再复制其他所有内容。
   下面是新文件：

   ```dockerfile
   FROM node:12-alpine
   WORKDIR /app
   COPY package.json yarn.lock ./
   RUN yarn install --production
   COPY . .
   CMD ["node", "/app/src/index.js"]
   ```

1. 使用 `docker build` 生成新映像。

   ```bash
   docker build -t getting-started .
   ```

   你应该看到类似于以下结果的输出：

   ```output
   Sending build context to Docker daemon  219.1kB
   Step 1/6 : FROM node:12-alpine
   ---> b0dc3a5e5e9e
   Step 2/6 : WORKDIR /app
   ---> Using cache
   ---> 9577ae713121
   Step 3/6 : COPY package* yarn.lock ./
   ---> bd5306f49fc8
   Step 4/6 : RUN yarn install --production
   ---> Running in d53a06c9e4c2
   yarn install v1.17.3
   [1/4] Resolving packages...
   [2/4] Fetching packages...
   info fsevents@1.2.9: The platform "linux" is incompatible with this module.
   info "fsevents@1.2.9" is an optional dependency and failed compatibility check. Excluding it from installation.
   [3/4] Linking dependencies...
   [4/4] Building fresh packages...
   Done in 10.89s.
   Removing intermediate container d53a06c9e4c2
   ---> 4e68fbc2d704
   Step 5/6 : COPY . .
   ---> a239a11f68d8
   Step 6/6 : CMD ["node", "/app/src/index.js"]
   ---> Running in 49999f68df8f
   Removing intermediate container 49999f68df8f
   ---> e709c03bc597
   Successfully built e709c03bc597
   Successfully tagged getting-started:latest
   ```

   所有层都已重新生成。
   这是预期的结果，因为更改了 Dockerfile。

1. 更改 src/static/index.html。
   例如，将标题更改为“The Awesome Todo App”。

1. 现在，再次使用 `docker build` 生成 Docker 映像。 这次的输出看起来应该略有不同。

   ```plaintext hl_lines="5 8 11"
   Sending build context to Docker daemon  219.1kB
   Step 1/6 : FROM node:12-alpine
   ---> b0dc3a5e5e9e
   Step 2/6 : WORKDIR /app
   ---> Using cache
   ---> 9577ae713121
   Step 3/6 : COPY package* yarn.lock ./
   ---> Using cache
   ---> bd5306f49fc8
   Step 4/6 : RUN yarn install --production
   ---> Using cache
   ---> 4e68fbc2d704
   Step 5/6 : COPY . .
   ---> cccde25a3d9a
   Step 6/6 : CMD ["node", "/app/src/index.js"]
   ---> Running in 2be75662c150
   Removing intermediate container 2be75662c150
   ---> 458e5c6f080c
   Successfully built 458e5c6f080c
   Successfully tagged getting-started:latest
   ```

   由于使用的是生成缓存，因此它的运行速度应快得多。

## <a name="multi-stage-builds"></a>多阶段生成

多阶段生成是非常强大的工具，可帮助使用多个阶段来创建映像。
它们有以下几个优点：

- 可将生成时依赖项与运行时依赖项分开
- 可通过仅传送应用需要运行的内容来减小整体映像大小

本部分提供了一些简单的示例。

### <a name="maventomcat-example"></a>Maven/Tomcat 示例

生成基于 Java 的应用程序时，需要使用 JDK 将源代码编译为 Java 字节码。
在生产环境中不需要 JDK。
可以使用 Maven 或 Gradle 等工具来帮助生成应用。
最终映像中也不需要这些工具。

```dockerfile
FROM maven AS build
WORKDIR /app
COPY . .
RUN mvn package

FROM tomcat
COPY --from=build /app/target/file.war /usr/local/tomcat/webapps 
```

此示例使用一个阶段 `build`，以通过 Maven 来执行实际的 Java 生成。
第二个阶段（从“FROM tomcat”开始）从 `build` 阶段复制文件。
最终映像只是要创建的最后一个阶段（可以使用 `--target` 参数来替代它）。

### <a name="react-example"></a>React 示例

在生成 React 应用程序时，需要使用 Node 环境将 JavaScript 代码、SASS 样式表等编译为静态 HTML、JavaScript 和 CSS。
如果未执行服务器端呈现，则无需为生产版本使用 Node 环境。

```dockerfile
FROM node:12 AS build
WORKDIR /app
COPY package* yarn.lock ./
RUN yarn install
COPY public ./public
COPY src ./src
RUN yarn run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
```

此示例使用 `node:12` 映像执行生成（最大化层缓存），然后将输出复制到 nginx 容器中。

## <a name="clean-up-resources"></a>清理资源

保留迄今为止所完成的一切内容，以继续学习本系列教程。

## <a name="next-steps"></a>后续步骤

你已学习了用于为容器应用永久保存数据的选项。

接下来，尝试学习本系列的下一教程：

> [!div class="nextstepaction"]
> [将 Docker 应用部署到 Azure 云](tutorial-deploy-docker-app-azure.md)
