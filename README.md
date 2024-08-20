Fork From：[tech-shrimp/docker_image_pusher: 使用Github Action将国外的Docker镜像转存到阿里云私有仓库，供国内服务器使用，免费易用](https://github.com/tech-shrimp/docker_image_pusher)

使用 Github Action 将国外的 Docker 镜像转存到阿里云私有仓库，供国内服务器使用，免费易用

- 支持DockerHub, gcr.io, k8s.io, ghcr.io等任意仓库
- 支持最大40GB的大型镜像
- 使用阿里云的官方线路，速度快

## 配置阿里云

登录阿里云容器镜像服务： https://cr.console.aliyun.com/

**新建命名空间：**

![image-20240820135000743](https://pic-bed-1256249917.cos.ap-chengdu.myqcloud.com/uPic/image-20240820135000743.png)

**设置固定密码：**

![image-20240820134544958](https://pic-bed-1256249917.cos.ap-chengdu.myqcloud.com/uPic/image-20240820134544958.png)

## 配置 Github Action 变量

![image-20240820121528773](https://pic-bed-1256249917.cos.ap-chengdu.myqcloud.com/uPic/image-20240820121528773.png)

设置以下四个变量，在第一步配置阿里云就已经获取了

```markdown
- ALIYUN_REGISTRY
- ALIYUN_NAME_SPACE
- ALIYUN_REGISTRY_USER
- ALIYUN_REGISTRY_PASSWORD
```

源代码查看：

> [flyeric0212/aliyun-docker-image-mirror (github.com)](https://github.com/flyeric0212/aliyun-docker-image-mirror)

可以直接 fork 项目，修改 images.txt 文件，替换成你想要 mirror 的 docker 镜像。

## Github Action 运行

提交代码后，会自动构建。

![image-20240820135354128](https://pic-bed-1256249917.cos.ap-chengdu.myqcloud.com/uPic/image-20240820135354128.png)

## 查看阿里云镜像

![image-20240820134021900](https://pic-bed-1256249917.cos.ap-chengdu.myqcloud.com/uPic/image-20240820134021900.png)

![image-20240820134106804](https://pic-bed-1256249917.cos.ap-chengdu.myqcloud.com/uPic/image-20240820134106804.png)

![image-20240820134209689](https://pic-bed-1256249917.cos.ap-chengdu.myqcloud.com/uPic/image-20240820134209689.png)