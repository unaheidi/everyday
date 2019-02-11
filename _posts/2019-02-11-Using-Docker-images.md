---
layout: post
---

## GitLab-CI 和 Docker

GitLab自带的CI（实际发挥作用的是 GitLab Runner 服务）可以使用（非强制） Docker Engine 来测试和构建应用。

Docker是个开源的项目，推出的服务允许我们选择基于某个image创建出一个container。这个container是一个独立的运行环境，里面有我们构建所需要的工具和应用。
当然，container里面的工具和应用其实是image定义好的，因此，选择不同的image就可以生成不同的container，而相同的image创建出多个container，
其实container内置的工具和应用是一摸一样的。

所以，采用Docker技术，可方便地、重复地生成相同的CI环境。

### CI采用docker的前提

GitLab Runner自身的服务，我们可以采用docker安装或非docker安装的方式。
而CI如果想采用dokcer来构建项目的话，必须先注册docker的runner（Register Docker Runner）。
实际上，这个注册的过程不外乎就是指定了Image和Service这些运行docker容器必须的信息罢了。
比如：
```
sudo gitlab-runner register \
  --url "https://gitlab.example.com/" \
  --registration-token "PROJECT_REGISTRATION_TOKEN" \
  --description "docker-ruby-2.1" \
  --executor "docker" \
  --docker-image ruby:2.1 \
  --docker-postgres latest \
  --docker-mysql latest

```
被注册的runner会使用ruby:2.1的image，还会运行基于postgres:latest和mysql:latest这两个services。在构建中会使用到这两个services。

### image需要注意的点

狭义的image是指Docker executor用来跑CI的。
其中pull policy：决定了image获取或更新的策略，可以在gitlab-runner/config.toml中修改，值得详细了解。

### service

service的image可以运行任何应用，但最常见的是用来跑数据库容器的。
也值得详细了解一下。

### 几个container如何方便地互访？

### 哪些不能当作service？

### 备注

本文为学习翻译稿，看一看后续可以如何使用GitLab的CI，以满足各种复杂的构建和测试环境。
