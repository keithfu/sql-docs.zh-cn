---
title: "SQL Server 2017 上 Docker 配置选项 |Microsoft 文档"
description: "了解不同使用和 SQL Server 2017 容器映像在 Docker 中与之进行交互的方式。 这包括持久保存数据，将文件，复制和故障排除。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f87c28e4d2ba7689d422ccf2f1a903765a39f27a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="configure-sql-server-2017-container-images-on-docker"></a>在 Docker 上配置 SQL Server 2017 容器映像

本主题说明如何配置和使用[mssql server linux 容器映像](https://hub.docker.com/r/microsoft/mssql-server-linux/)使用 Docker。 此映像包含在 Linux（基于 Ubuntu 16.04）上运行的 SQL Server。 它可与适用于 Linux 的 Docker 引擎 1.8 以上版本或适用于 Mac/Windows 的 Docker 配合使用。

> [!NOTE]
> 本主题专门重点介绍 mssql-server-linux 映像的使用。 未涵盖的 Windows 映像，但你可以了解有关它在[mssql server windows Docker Hub 页](https://hub.docker.com/r/microsoft/mssql-server-windows/)。

## <a name="pull-and-run-the-container-image"></a>请求和运行容器映像

若要请求并对 SQL Server 2017 运行 Docker 容器映像，按照以下快速入门教程中的的先决条件和步骤:

- [使用 Docker 运行 SQL Server 2017 容器映像](quickstart-install-connect-docker.md)

此配置主题提供了其他连接和下面的部分中的使用方案。

## <a name="connect-and-query"></a>连接和查询

可以从容器外部或内部对容器中的 SQL Server 进行连接和查询。 以下各节介绍了这两种方案。 

### <a name="tools-outside-the-container"></a>容器外的工具

可以从支持 SQL 连接的任何 Linux、Windows 或 macOS 外部工具连接到 Docker 计算机上的 SQL Server 实例。 一些常用工具包括：

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio 代码](sql-server-linux-develop-use-vscode.md)
- [在 Windows 上的 SQL Server Management Studio (SSMS)](sql-server-linux-develop-use-ssms.md)

下面的示例使用**sqlcmd**以连接到在 Docker 容器中运行的 SQL Server。 连接字符串中的 IP 地址是运行容器的主机的 IP 地址。

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

如果映射默认值不是主机端口**1433年**，将该端口添加到连接字符串。 例如，如果你指定`-p 1400:1433`中你`docker run`命令，然后通过显式连接指定端口 1400年。

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>容器内的工具

从 SQL Server 自 2017 年 1 CTP 2.0，开始[SQL Server 命令行工具](sql-server-linux-setup-tools.md)包含在容器映像。 如果使用交互式命令提示符附加至此映像，则可在本地运行工具。

1. 使用`docker exec -it`命令来启动交互式 bash shell 内你正在运行的容器。 在下面的示例`e69e056c702d`是容器 id。

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 无需始终指定完整的容器 ID。 只需要指定足够的字符，能够唯一标识它即可。 在此示例中，它可能是足够用于`e6`或`e69`而不是完整的 id。

2. 一旦位于容器内部，使用 sqlcmd 进行本地连接。 请注意， 默认情况下，sqlcmd 不在路径之中，因此需要指定完整的路径。

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. 当完成了 sqlcmd，键入`exit`。

4. 当完成了交互式命令提示符，键入`exit`。 退出交互式 Bash Shell 后，容器将继续运行。

## <a name="run-multiple-sql-server-containers"></a>运行多个 SQL Server 容器

Docker 支持在同一主机上运行多个 SQL Server 容器。 这就为要求在同一主机上运行多个 SQL Server 实例的方案提供了解决办法。 每个容器必须在一个不同的端口上公开自身。

下面的示例创建两个 SQL Server 容器，并将它们映射到端口**1401年**和**1402年**主机计算机上。

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1402:1433 -d microsoft/mssql-server-linux
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1402:1433 -d microsoft/mssql-server-linux
```

现在，两个 SQL Server 实例在单独的容器内运行。 客户端可通过使用 Docker 主机的 IP 地址和容器的端口号连接每个 SQL Server 实例。

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="persist"></a>保存数据

SQL Server 配置更改和数据库文件会保留容器，即使您重新启动的容器`docker stop`和`docker start`。 但是，如果删除的容器`docker rm`，容器中的所有内容将被删除，包括 SQL Server 和数据库。 以下部分说明了如何使用**数据卷**以保留你的数据库文件，即使删除关联的容器。

> [!IMPORTANT]
> 就 SQL Server 而言，了解 Docker 中的数据持久性至关重要。 除了本部分中讨论，请参阅 Docker 文档[如何管理 Docker 容器中的数据](https://docs.docker.com/engine/tutorials/dockervolumes/)。

### <a name="mount-a-host-directory-as-data-volume"></a>将主机目录装载为数据卷

第一种方法是在主机上装载目录，将其作为容器中的数据卷。 为此，请使用`docker run`命令`-v <host directory>:/var/opt/mssql`标志。 这允许在容器执行之间还原数据。

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

通过此方法，还能共享和查看位于主机上、Docker 外的文件。

> [!IMPORTANT]
> 当前不支持 Mac 上的 Docker 与 Linux 映像上 SQL Server 的主机卷映射。 请改为使用数据卷容器。 此限制是特定于`/var/opt/msql`目录。 从已装载目录进行读取操作可正常运行。 例如，可在 Mac 上使用 –v 装载主机目录，并通过驻留在主机上的 .bak 文件还原备份。

### <a name="use-data-volume-containers"></a>使用数据卷容器

第二个方法是使用数据卷容器。 可以通过指定卷名称而不是与主机目录中创建数据卷容器`-v`参数。 下面的示例创建名为的共享的数据卷**sqlvolume**。

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux
```

> [!NOTE]
> 早期版本的 Docker 不支持通过此方法在 run 命令中隐式创建数据卷。 在这种情况下，使用 Docker 文档中所述的显式步骤[创建和装载数据卷容器](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container)。

即使停止并删除此容器，数据卷仍然存在。 你可以查看其与`docker volume ls`命令。

```bash
docker volume ls
```

如果稍后又创建了另一个具有相同卷名的容器，则这个新容器将使用卷中包含的相同 SQL Server 数据。

若要删除数据卷容器，使用`docker volume rm`命令。

> [!WARNING]
> 如果你删除数据卷容器，容器中的任何 SQL Server 数据是*永久*删除。

### <a name="backup-and-restore"></a>备份和还原
除这些容器技术外，还可使用 SQL Server 标准备份和还原技术。 可通过备份文件来保护数据，或将数据移动至其他 SQL Server 实例。 有关详细信息，请参阅[SQL Server 备份和还原数据库在 Linux 上](sql-server-linux-backup-and-restore-database.md)。

> [!WARNING]
> 如要创建备份，请确保在容器外部创建或复制备份文件。 否则，一旦删除容器，也将随之删除备份文件。

## <a name="execute-commands-in-a-container"></a>在容器中执行命令

如果正在运行容器，那么可以从主机终端在容器内部执行命令。

要获取容器 ID，请运行：

```bash
docker ps
```

要在容器中启动 Bash 终端，请运行：

```bash
docker exec -ti <Container ID> /bin/bash
```

现在，可以运行这些命令，就像在容器内的终端上运行那样。 完成后，键入`exit`。 这将退出交互式命令会话，但容器将继续运行。

## <a name="copy-files-from-a-container"></a>从容器复制文件

要从容器复制文件，请使用下列命令：

```bash
docker cp <Container ID>:<Container path> <host path>
```

**示例：**

```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```

```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```

要将文件复制到容器中，请使用下列命令：

```bash
docker cp <Host path> <Container ID>:<Container path>
```

**示例：**

```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

## <a name="upgrade-sql-server-in-containers"></a>升级容器中的 SQL Server

若要使用 Docker 升级容器映像，请从注册表请求最新版本。 使用`docker pull`命令：

```bash
docker pull microsoft/mssql-server-linux:latest
```

这将更新任何新创建容器的 SQL Server 映像，但不会更新任何正在运行的容器中的 SQL Server。 为此，必须使用最新 SQL Server 容器映像创建新容器，并将数据迁移到该新容器。

1. 首先，请确保你正在使用它的[数据持久性技术](#persist)你现有的 SQL Server 容器。

2. 停止 SQL Server 容器与`docker stop`命令。

3. 创建一个新的 SQL Server 容器与`docker run`并指定映射的主机目录或数据卷容器。 新容器当前使用新版 SQL Server 和现有 SQL Server 数据。

4. 在新容器中验证数据库和数据。

5. 还可以删除的旧容器`docker rm`。

## <a id="troubleshooting"></a>故障排除

以下各节提供关于在容器中运行 SQL Server 的故障排除建议。

### <a name="docker-command-errors"></a>Docker 命令错误

如果出现任何错误`docker`命令，请确保运行 docker 服务，然后尝试使用提升的权限运行。

例如，在 Linux 上，你可能会收到以下错误时运行`docker`命令：

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

如果在 Linux 上收到此错误，请尝试运行相同开头的命令`sudo`。 如果失败，验证 Docker 服务是否正在运行；如果没有，请启动它。

```bash
sudo systemctl status docker
sudo systemctl start docker
```

在 Windows 上，验证将启动 PowerShell 或以管理员身份在命令提示符处。

### <a name="sql-server-container-startup-errors"></a>SQL Server 容器启动错误

如果 SQL Server 容器无法运行，请尝试下列测试：

- 如果你收到错误，例如**无法在网桥上创建终结点 CONTAINER_NAME。启动代理时出错： 侦听 tcp 0.0.0.0:1433 绑定： 已在使用的地址。**，然后尝试将容器端口 1433年映射到已在使用的端口。 在主机上本地运行 SQL Server 时可能发生此错误。 如果启动了两个 SQL Server 容器，并尝试将它们映射到同一主机端口，也可能发生此错误。 如果发生这种情况，使用`-p`参数映射到不同的主机的端口的容器端口 1433年。 例如： 

    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1400:1433 -d microsoft/mssql-server-linux`.
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1400:1433 -d microsoft/mssql-server-linux`.
    ```

- 检查是否有任何来自容器的错误消息。

    ```bash
    docker logs e69e056c702d
    ```

- 请确保满足中指定的最小内存和磁盘要求[要求](#requirements)本主题的部分。

- 如果正在使用任何容器管理软件，请确保它支持以根身份运行的容器进程。 容器中的 sqlservr 进程以根身份运行。

- 查看[SQL Server 安装程序和错误日志](#errorlogs)。

### <a name="sql-server-connection-failures"></a>SQL Server 连接故障

如果无法连接到在容器中运行的 SQL Server 实例，请尝试下列测试：

- 请确保 SQL Server 容器正在通过查看运行**状态**列`docker ps -a`输出。 否则，请使用`docker start <Container ID>`来启动它。

- 如果映射到非默认主机端口（非 1433），请确保在连接字符串中指定端口。 你可以看到您中的端口映射**端口**列`docker ps -a`输出。 例如，下列命令将 sqlcmd 连接至在端口 1401 上侦听的容器：

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- 如果你使用`docker run`与现有映射的数据卷或数据卷容器，SQL Server 将忽略的值`MSSQL_SA_PASSWORD`。 改为使用来自 SQL Server 数据（在数据卷或数据卷容器中）的预配置 SA 用户密码。 验证所使用的 SA 密码是否与附加到的数据相关联。

- 查看[SQL Server 安装程序和错误日志](#errorlogs)。

### <a name="sql-server-availability-groups"></a>SQL Server 可用性组

如果正在使用 Docker 和 SQL Server 可用性组，还有两个额外要求。

- 映射用于副本通信的端口（默认为 5022）。 例如，指定`-p 5022:5022`作为的一部分你`docker run`命令。

- 显式设置容器主机名与`-h YOURHOSTNAME`参数`docker run`命令。 配置可用性组时使用该主机名。 如果未指定其与`-h`，它默认为容器 id。

### <a id="errorlogs"></a>SQL Server 安装程序和错误日志

你可以查看 SQL Server 安装程序和错误日志**/var/opt/mssql/log**。 如果容器未运行，请首先启动它。 然后使用交互式命令提示符来检查日志。

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

从容器内的 bash 会话运行下列命令：

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> 如果你在装载主机目录到**/var/opt/mssql**当你创建你的容器，你可以改为查看**日志**在主机上的映射路径的子目录。

## <a name="next-steps"></a>后续步骤

开始使用 Docker 上的 SQL Server 2017 容器映像浏览[快速入门教程](quickstart-install-connect-docker.md)。

另请参阅[mssql docker GitHub 存储库](https://github.com/Microsoft/mssql-docker)对资源、 反馈和已知的问题。
