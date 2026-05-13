# 1 产品介绍

## 简介
从 2G 到 5G，移动通信网络经历了四代演进，网络规模和复杂度呈指数级增长。传统依赖大量人力的运维模式面临运营成本高、用户体验压力大、业务创新乏力的挑战。 2019 年起，全球领先运营商开始推动自智网络（Autonomous Network, AN）理念——让网络从"人工操作"走向"自动执行"，最终实现"自主治理"，并将网络自治水平分为L1-L5。
AN L4 的核心特征是：在特定场景下实现端到端闭环自治，而要实现 L4，就必须解决多厂商、跨层、跨域的智能体互联协作问题。当前业界虽然有通用的智能体框架（如 Google A2A 协议）和编排工具（如 LangGraph）解决智能体互联协作问题，但在通信领域应用存在网络运维安全风险、运维工程师编码复杂、运维知识和工具复用难等问题。因此，OpenAN应运而生，OpenAN是一个自智网络开源项目集，通过一系列开源项目支撑通信智能体的开发和部署，使能多厂商、跨层、跨域集成，加速自智网络迈向L4-L5。

## 核心愿景
- 端到端闭环自治网络：加速电信专属智能体的跨层、跨域对接集成和上线部署，多智能体高效编排与协同，使能全球运营商加速实现AN L4。
- 厂商中立与开放生态：基于行业标准（价值场景Solution Package、智能体互联协议等），推进厂商中立、产业共享的场景化“技能、组件、知识和实践”，围绕AN形成电信全产业合作生态，共同提升产业AN水平。
- 行业主导与未来演进：推动OpenAN成为电信行业事实标准，探索面向AN L5下一代智能化系统的集成与协作。

## 项目架构
todo

## 应用场景
todo
说明：OpenAN首次开源A2A-T，todo

# 2 软件安装指南（快速安装）

## 2.1 系统要求

本项目基于 Python 3.10 开发，编译安装前请确保目标系统满足以下要求：

### 2.1.1  操作系统

| 操作系统 | 最低版本 |
|---------|---------|
| 其他 Linux 发行版 | 内核 3.10+ |
| CentOS / RHEL | 7.0+ |
| Ubuntu | 18.04+ |
| Debian | 10+ |

### 2.1.2 编译工具链

| 工具 | 最低版本 | 推荐版本 | 查看命令 |
|-----|---------|---------|---------|
| GCC | 4.8.5 | 5.0+ | `gcc --version` |
| Make | 3.81 | 4.0+ | `make --version` |
| Glibc | 2.17 | 2.28+ | `ldd --version` |

> **说明**：Python 3.10 编译需要支持 C11 标准的编译器，GCC 5.0+ 可提供更好的优化支持。Glibc 2.17 是 Python 3.10 的最低要求，建议使用 2.28+ 以获得更好的兼容性。

### 2.1.3 验证系统环境

```bash
# 检查 GCC 版本
gcc --version

# 检查 Make 版本
make --version

# 检查 Glibc 版本
ldd --version
```

---

## 2.2 依赖安装

本项目基于 Python 3.10 开发，编译安装前请确保相关组件依赖满足以下要求：

| 组件       | 版本       | 官网下载链接                                                 |
| ---------- | ---------- | ------------------------------------------------------------ |
| Python     | >= 3.10.15 | https://www.python.org/ftp/python/3.10.15/Python-3.10.15.tgz |
| PostgreSQL | >= 16.13   | https://ftp.postgresql.org/pub/source/v16.13/postgresql-16.13.tar.gz |

> 各组件离线安装指导如下，如果系统已有组件且版本已满足则可跳过此指导步骤

### 2.2.1 Python离线安装步骤

#### 2.2.1.1 下载安装包

在可接通网络的Linux服务器上执行以下命令获取安装包，Windows系统则直接访问网页下载获取

```bash
wget https://www.python.org/ftp/python/3.10.15/Python-3.10.15.tgz
```

将 `Python-3.10.15.tgz` 传输到目标服务器。

#### 2.2.1.2 解压安装包

```bash
tar -xzf Python-3.10.15.tgz
cd Python-3.10.15
```

#### 2.2.1.3 配置安装路径

```bash
# 安装到 /usr/local/python310，避免覆盖系统Python
./configure --prefix=/usr/local/python310 --enable-optimizations
```

#### 2.2.1.4 编译安装

```bash
make -j 4
sudo make altinstall
```

#### 2.2.1.5 创建软链接

```bash
# 创建python3软链接
sudo ln -sf /usr/local/python310/bin/python3 /usr/local/bin/python3

# 创建pip3软链接
sudo ln -sf /usr/local/python310/bin/pip3 /usr/local/bin/pip3
```

#### 2.2.1.6 验证安装

```bash
python3 --version   # 应输出 Python 3.10.15
pip3 --version
```

#### 2.2.1.7 注意事项

- 安装路径 `/usr/local/python310` 不影响系统自带Python
- 软链接放在 `/usr/local/bin`，优先级低于 `/usr/bin`
- 系统自带的 `python` 或 `python2` 命令保持不变

### 2.2.2 PostgreSQL离线安装步骤

#### 2.2.2.1 下载安装包

在可接通网络的Linux服务器上执行以下命令获取安装包，Windows系统则直接访问网页下载获取

```bash
wget https://ftp.postgresql.org/pub/source/v15.6/postgresql-15.6.tar.gz
```

将 `postgresql-15.6.tar.gz` 传输到目标服务器。

#### 2.2.2.2 解压安装包

```bash
tar -xzf postgresql-15.6.tar.gz
cd postgresql-15.6
```

#### 2.2.2.3 配置安装路径

```bash
# 安装到 /usr/local/pgsql
./configure --prefix=/usr/local/pgsql --without-readline
```

常用配置选项：
- `--prefix=/usr/local/pgsql`: 指定安装路径
- `--with-openssl`: 启用SSL支持
- `--with-readline`: 启用readline支持（默认启用）
- `--with-zlib`: 启用zlib支持（默认启用）

#### 2.2.2.4 编译安装

```bash
make -j 4
sudo make install
```

#### 2.2.2.5 创建postgres用户

```bash
sudo useradd postgres
```

#### 2.2.2.6 创建数据目录并授权

```bash
sudo mkdir -p /usr/local/pgsql/data
sudo chown -R postgres:postgres /usr/local/pgsql/data
```

#### 2.2.2.7 初始化数据库

```bash
su - postgres # 切换至postgres用户
/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
```

#### 2.2.2.8 启动PostgreSQL服务

```bash
# 切换至postgres用户
su - postgres

# 前台启动
/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
/usr/local/pgsql/bin/pg_ctl -D /usr/local/pgsql/data -l /usr/local/pgsql/data/logfile start

# 添加系统环境变量
echo "export PATH=/usr/local/pgsql/bin:\$PATH" >> ~/.bashrc
source ~/.bashrc

# 确认启动成功
psql -l

# 检查版本
/usr/local/pgsql/bin/psql --version

# 连接数据库
/usr/local/pgsql/bin/psql -c "SELECT version();"
```

退出`postgres`用户可输入`exit`

#### 2.2.2.9 配置systemd服务（可选）

```bash
sudo tee /etc/systemd/system/postgresql.service << EOF
[Unit]
Description=PostgreSQL 16 Database Server
After=network.target

[Service]
Type=forking
User=postgres
Group=postgres
Environment=PGDATA=/usr/local/pgsql/data
ExecStart=/usr/local/pgsql/bin/pg_ctl start -D /usr/local/pgsql/data -l /usr/local/pgsql/data/logfile
ExecStop=/usr/local/pgsql/bin/pg_ctl stop -D /usr/local/pgsql/data
ExecReload=/usr/local/pgsql/bin/pg_ctl reload -D /usr/local/pgsql/data
PIDFile=/usr/local/pgsql/data/postmaster.pid
TimeoutSec=300

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable postgresql
sudo systemctl start postgresql
```

#### 2.2.2.10 创建数据库和用户

```bash
# 切换至postgres用户
su - postgres

# 进入sql交互界面
psql
```

在psql中执行：

```sql
CREATE USER registry_user WITH ENCRYPTED PASSWORD 'your_password' CREATEDB;
```

#### 2.2.2.11 配置远程访问（使用root用户）

编辑 `/usr/local/pgsql/data/pg_hba.conf`，在末尾添加：

```bash
# 添加允许远程连接
host    all             all             0.0.0.0/0               scram-sha-256
```

编辑 `/usr/local/pgsql/data/postgresql.conf`：

```bash
# 修改监听地址
listen_addresses = '*'
```

重启服务：

```bash
# 使用systemctl重启（推荐）
sudo systemctl restart postgresql

# 或重启数据库配置
su - postgres -c "/usr/local/pgsql/bin/pg_ctl -D /usr/local/pgsql/data restart"
```

#### 2.2.2.12 注意事项

- PostgreSQL 默认使用端口 5432
- 生产环境请务必修改默认密码
- 配置防火墙规则限制数据库访问
- 建议定期备份数据库

---

## 2.3 注册中心服务离线安装步骤

### 2.3.1 准备安装包

下载注册中心源码：[registry-center-main-a2a1.0-20260430-release.zip](https://pan.quark.cn/s/4506a90cd7fc)

下载离线服务依赖包：[wheels.zip](https://pan.quark.cn/s/957150b18c0a)

在目标服务器的临时目录下创建`/registry-center`文件夹，将 registry-center 源码和离线服务依赖包传输到该目录下：

```bash
mkdir /tmp/registry-center
cd /tmp/registry-center
unzip registry-center-main-a2a1.0-20260430-release.zip
unzip wheels.zip -d ./registry-center-main-a2a1.0-20260430-release
```

### 2.3.2 创建虚拟环境

```bash
cd registry-center-main-a2a1.0-20260430-release

# 使用已安装的Python 3.10创建虚拟环境
python3 -m venv venv --copies
```

### 2.3.3 激活虚拟环境

```bash
# 激活虚拟环境
source venv/bin/activate
```

激活后，命令行前缀会显示 `(venv)`。

### 2.3.4 离线安装依赖

```bash
# 从wheels文件夹离线安装所有依赖
pip install --no-index --find-links=wheels/ -r ./requirements.txt
```

### 2.3.5 服务安装配置（可选）

可在`./etc/systemd/deploy.conf`文件中配置服务部署目录等，离线安装模式下可不修改此配置文件

```bash
vi ./etc/systemd/deploy.conf

# Registry Center 部署配置
# Copyright (c) 2026 Huawei Technologies Co., Ltd.

# 部署目录（服务安装位置）
INSTALL_DIR=/OpenA2A-T/registry-center

# Python路径（留空则用  INSTALL_DIR/venv/bin/python3）
PYTHON_PATH=

# 服务名称
SERVICE_NAME=registry-center

# 是否自动安装依赖，离线状态下需自行准备依赖包，设置为false；为true时将使用pip命令下载安装依赖包
INSTALL_DEPS=false
```

> 退出vi：按下Esc按键，输入:wq!


### 2.3.6 修改数据库连接配置

修改注册中心配置文件： `./etc/conf/persistence.conf`

- 修改`postgresql.host`为数据库所在节点IP

- 修改`postgresql.port`为postgresql数据库端口号，默认为`5432`

- 用户名`postgresql.username`、密码`postgresql.password`按照数据库实际设置的情况进行修改

### 2.3.7 给脚本添加可执行权限

```bash
# 给脚本添加可执行权限
chmod +x ./bin/*.sh
```

### 2.3.8 安装服务到指定目录

```bash
# 安装服务到步骤3.5中指定的INSTALL_DIR目录
sudo ./bin/install_service.sh install

# 执行成功后将回显成功信息：
# Installing the project to /OpenA2A-T/registry-center...
# Files copied successfully
# Deploy Configuration:
#   Install Dir: /OpenA2A-T/registry-center
#   Python Path: /OpenA2A-T/registry-center/venv/bin/python3
#   Install Deps: false
# 
# Using Python: /OpenA2A-T/registry-center/venv/bin/python3
# Python 3.10.15
# Service installed successfully!
```

### 2.3.9 初始化服务配置

```bash
# 进入服务安装目录
cd /OpenA2A-T/registry-center

# 初始化服务配置
./venv/bin/python3 -m agent_registry.init
```

服务默认支持HTTPS和AgentCard签名及验签能力，**首次启动可选择关闭，后续按需执行此章节进行配置**

```bash
是否开启HTTPS enable_https (y/n, 默认: true): n
是否需要提供注册中心签名配置 registry.sign.enabled (y/n, 默认: true): n
是否开启验签能力 signature_validation_enabled (y/n, 默认: true): n

==================================================
持久化存储配置
==================================================

请选择存储模式 persistence.mode (file/postgresql, 默认: postgresql): file

配置已完成，已保存在 /OpenA2A-T/registry-center/etc/conf/server.conf
```

### 2.3.10 启动服务和状态管理

```bash
# 启动服务
systemctl start registry-center

# 查看服务状态
systemctl status registry-center

# 停止服务
systemctl stop registry-center
```

### 2.3.11 服务状态日志查看

```bash
# 查看所有日志
journalctl -u registry-center

# 实时追踪日志
journalctl -u registry-center
```

### 2.3.12 卸载服务

```bash
# 从安装目录卸载服务
sudo ./bin/install_service.sh uninstall
```

---

## 2.4 编排中心服务离线安装步骤

### 2.4.1 准备安装包

下载注册中心源码：[orchestration-center-main-a2a1.0-20260430-release.zip](https://pan.quark.cn/s/346356c6a6aa)

下载离线服务依赖包：[wheels.zip](https://pan.quark.cn/s/7488f63ec3f6)

在目标服务器的临时目录下创建`/orchestration-center`文件夹，将 orchestration-center 源码和离线服务依赖包传输到该目录下：

```bash
mkdir /tmp/orchestration-center
cd /tmp/orchestration-center
unzip orchestration-center-main-a2a1.0-20260430-release.zip
unzip wheels.zip -d ./orchestration-center-main-a2a1.0-20260430-release
```

### 2.4.2 创建虚拟环境

```bash
cd orchestration-center-main-a2a1.0-20260430-release

# 使用已安装的Python 3.10创建虚拟环境
python3 -m venv venv --copies
```

### 2.4.3 激活虚拟环境

```bash
# 激活虚拟环境
source venv/bin/activate
```

激活后，命令行前缀会显示 `(venv)`。

### 2.4.4 离线安装依赖

```bash
# 从wheels文件夹离线安装所有依赖
pip install --no-index --find-links=wheels/ -r ./requirements.txt
```

### 2.4.5 服务安装配置（可选）

可在`./etc/systemd/deploy.conf`文件中配置服务部署目录等，离线安装模式下可不修改此配置文件

```bash
vi ./etc/systemd/deploy.conf

# Orchestration Center 部署配置
# Copyright (c) 2026 Huawei Technologies Co., Ltd.

# 部署目录（服务安装位置）
INSTALL_DIR=/OpenA2A-T/orchestration-center

# Python路径（留空则用  INSTALL_DIR/venv/bin/python3）
PYTHON_PATH=

# 服务名称
SERVICE_NAME=orchestration-center

# 是否自动安装依赖，离线状态下需自行准备依赖包，设置为false；为true时将使用pip命令下载安装依赖包
INSTALL_DEPS=false
```

> 退出vi：按下Esc按键，输入:wq!

### 2.4.6 修改数据库连接配置

修改编排中心配置文件： `./etc/conf/db_config.conf`

- 修改`host`为postgressql数据库所在节点IP

- 修改`port`为postgressql数据库端口号，默认为`5432`

- 用户名`user`密码、`password`按照数据库实际设置的情况进行修改

### 2.4.7 给脚本添加可执行权限

```bash
# 给脚本添加可执行权限
chmod +x ./bin/*.sh
```

### 2.4.8 安装服务到指定目录

```bash
# 安装服务到步骤4.5中指定的INSTALL_DIR目录
sudo ./bin/install_service.sh install

# 执行成功后将回显成功信息：
# Installing the project to /OpenA2A-T/orchestration-center...
# Files copied successfully
# Deploy Configuration:
#   Install Dir: /OpenA2A-T/orchestration-center
#   Python Path: /OpenA2A-T/orchestration-center/venv/bin/python3
#   Install Deps: false
# 
# Using Python: /OpenA2A-T/orchestration-center/venv/bin/python3
# Python 3.10.15
# Service installed successfully!
```

### 2.4.9 初始化服务配置（需配置数据库）

```bash
# 进入服务安装目录
cd /OpenA2A-T/orchestration-center

# 初始化服务配置，可配置服务端口，是否启用HTTPS等
vi ./etc/conf/server.conf
```

服务默认支持HTTPS能力，**首次启动可选择关闭，后续按需执行此章节进行配置**

```bash
# 设置enable_https=false
:wq!
```

### 2.4.10 启动服务和状态管理

```bash
# 启动服务
systemctl start orchestration-center

# 查看服务状态
systemctl status orchestration-center

# 停止服务
systemctl stop orchestration-center
```

### 2.4.11 服务状态日志查看

```bash
# 查看所有日志
journalctl -u orchestration-center

# 实时追踪日志
journalctl -u orchestration-center
```

### 2.4.12 卸载服务

```bash
# 从安装目录卸载服务
sudo ./bin/install_service.sh uninstall
```

---

# 3 快速入门
![photo](figures/registry-center.png)

注册中心是一个专注于Agent统一管理的服务，支持用户将来自不同厂商的Agent进行集中注册与管理，实现多源Agent的可控接入与维护。主要功能包括：

- **注册AgentCard**：支持将不同厂商的Agent注册到中心，统一纳管。
- **查询AgentCard列表**：根据指定条件查询符合条件的AgentCard列表。
- **查询指定AgentCard**：按AgentCard名称和组织精确查找唯一的AgentCard实例。
- **更新指定AgentCard**：更新指定AgentCard的信息。
- **删除指定AgentCard**：删除不再使用的AgentCard。
- **按语义检索AgentCard**：根据自然语言语义检索相匹配的AgentCard。

通过这些功能，注册中心可以帮助用户高效整合、维护与发现各类 Agent，为上层编排与协同提供基础能力。

编排中心是一个面向多智能体（Agent）协作的可视化编排平台，支持通过图形化工作流设计器定义 Agent 之间的调用关系与执行流程。后端基于 Python 框架解析流程并驱动 Agent 协同工作，帮助用户高效构建、管理和运行复杂的 Agent 协作流程。主要功能包括：

- **PSOP 管理**：支持工作流（PSOP）的列表查看、详情查询、保存与删除操作。
- **PDF 解析**：提供 PDF 文件内容解析能力，为后续流程设计提供数据支持。
- **智能规划**：根据用户需求自动生成工作流规划，降低编排门槛。
- **Agent 管理**：获取全量 AgentCard 列表，便于了解可用能力与调用方式。
- **自然语言生成 PSOP**：通过自然语言意图直接生成可执行的编排流程。
- **意图检索 PSOP**：根据自然语言描述，检索匹配的历史工作流。
- **实时流程执行**：支持以流式方式启动 PSOP 执行，并实时推送运行进展，便于监控与调试。
## 3.1 环境准备

在开始之前，请确保您的开发环境满足以下要求：

| 依赖项 | 版本要求     | 用途 |
| --- |----------| --- |
| Node.js | &gt;= 20.19 | 编排中心前端 |
| Python | &gt;= 3.10 | 注册中心与编排中心后端 |

## 3.2 启动服务
### 3.2.1 启动注册中心服务
启动方式见注册中心的用户指南或Readme文档
### 3.2.2 启动编排中心后端服务
启动方式见编排中心的用户指南或Readme文档
### 3.2.3 启动编排中心前端界面
启动方式见编排中心的用户指南或Readme文档
## 3.3 启动示例 Agent
为了快速体验完整流程，可以启动项目自带的示例 Agent 服务
```bash
cd {项目路径}/orchestration-center/samples
python start_agents_server.py
```
该脚本会：

- 向注册中心注册多个示例 Agent
- 启动对应的 Agent 服务，供编排中心调用
## 3.4 核心流程验证
完成上述步骤后，您可以按照以下流程体验 OpenAN 的核心能力：

![photo](figures/workflow.png)

### 3.4.1 访问编排中心界面

打开浏览器访问 `http://localhost:3003`

### 3.4.2 配置服务地址

点击界面右上角的齿轮图标，将后端 IP 和端口修改为编排中心后端的实际地址，保存。

### 3.4.3 查看 Agent 库

左侧展示从注册中心获取的所有 Agent，可通过名称或功能进行搜索。

### 3.4.4 创建工作流
点击 `+` 按钮，选择创建方式：

| 方式 | 操作说明 |
| --- | --- |
| PDF 导入 | 上传 PDF 文件，系统自动解析并生成 PSOP |
| 手动编排 | 将 Agent 卡片拖拽到画布，通过连线定义执行顺序 |
| 自然语言生成 | 输入业务意图描述，后台自动编排生成 PSOP |
- (具体创建流程见编排中心用户指南)
### 3.4.5 执行工作流
- 输入用户意图，点击“检索工作流”按钮
- 选择匹配的 PSOP
- 点击 `▶` 按钮执行，右侧区域实时显示执行过程
