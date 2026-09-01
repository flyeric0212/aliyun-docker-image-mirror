

# Docker Image Mirror 工具

这个工具用于将 Docker 镜像从公共仓库拉取并推送到阿里云容器镜像服务。支持本地运行和 GitHub Actions 集成。

## 功能特点

- 支持从公共仓库拉取 Docker 镜像并推送到阿里云容器镜像服务
- 支持处理重名镜像，自动添加命名空间前缀
- 支持指定平台架构的镜像
- 支持本地运行和 GitHub Actions 集成
- 提供 Bash 脚本和 Python 两种实现方式

## 配置说明

工具需要以下配置参数：

- `ALIYUN_REGISTRY`: 阿里云容器镜像服务地址
- `ALIYUN_NAME_SPACE`: 阿里云容器镜像命名空间
- `ALIYUN_REGISTRY_USER`: 阿里云容器镜像服务用户名
- `ALIYUN_REGISTRY_PASSWORD`: 阿里云容器镜像服务密码

### 阿里云配置
登录阿里云容器镜像服务： https://cr.console.aliyun.com/

**新建命名空间：**

![image-20240820135000743](images/01.png)

**设置固定密码：**

![image-20240820134544958](images/02.png)


### 本地配置

1. 复制 `.env.example` 文件为 `.env`：

```bash
cp .env.example .env
```

2. 编辑 `.env` 文件，填入您的实际配置：

```
ALIYUN_REGISTRY=registry.cn-hangzhou.aliyuncs.com
ALIYUN_NAME_SPACE=your-namespace
ALIYUN_REGISTRY_USER=your-username
ALIYUN_REGISTRY_PASSWORD=your-password
```

### GitHub Actions 配置

在 GitHub 仓库中设置以下 Secrets：

- `ALIYUN_REGISTRY`
- `ALIYUN_NAME_SPACE`
- `ALIYUN_REGISTRY_USER`
- `ALIYUN_REGISTRY_PASSWORD`

![image-20240820121528773](images/03.png)


## 镜像列表

在 `images.txt` 文件中列出需要镜像的 Docker 镜像，每行一个。支持以下格式：

```
# 基本格式
nginx
mysql:8.0.37

# 带命名空间的镜像
halohub/halo:2.20

# 私有仓库镜像
k8s.gcr.io/kube-state-metrics/kube-state-metrics:v2.0.0

# 指定架构的镜像
--platform=linux/arm64 xiaoyaliu/alist
```

可以直接 fork 项目，修改 images.txt 文件，替换成你想要 mirror 的 docker 镜像。


## 使用方法

### Bash 脚本版本

```bash
# 确保已安装 Docker 且脚本有执行权限
chmod +x docker-mirror.sh

# 运行脚本
./docker-mirror.sh
```

### Python 版本

```bash
# 安装依赖，根据本地实际情况使用 pip 或者 pip3
pip3 install -r requirements.txt

# 运行脚本
python3 docker_mirror.py
```

或者，您可以将脚本安装为可执行命令：

```bash
# 安装到当前环境
pip3 install -e .

# 运行命令
docker-mirror
```

## GitHub Actions 集成

工具已经集成到 GitHub Actions 工作流中。当推送到 main 分支或手动触发工作流时，将自动运行镜像任务。

![image-20240820135354128](images/04.png)

## 查看镜像结果
![image-20240820134021900](images/05.png)

![image-20240820134106804](images/06.png)

![image-20240820134209689](images/07.png)


## 开发说明

### 依赖管理

Python 版本使用 pip 进行依赖管理：
- 所有依赖都列在 `requirements.txt` 文件中
- 使用 `pip3 install -r requirements.txt` 安装依赖

### 贡献指南

1. Fork 本仓库
2. 创建您的特性分支 (`git checkout -b feature/amazing-feature`)
3. 提交您的更改 (`git commit -m 'Add some amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 打开一个 Pull Request

## 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件
