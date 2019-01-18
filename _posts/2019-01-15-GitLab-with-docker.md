---
layout: post
---

## 把 GitLab 自带的 CI 捡起来

2015年到2018年之间，因为换公司的缘故，我把工作重心从持续集成的开发 -> 为更大规模研发团队提供高可用的代码服务，而恰好就在这三年之间，
GitLab 却已逐渐从代码管理中心华丽转变为了 DevOps 全流程的服务中心。

2018年下半年，当我再次把目光投向 GitLab ，欣赏着 GitLab pipeline 美丽的流水线，心动不已。
只要在 GitLab 中定义好 .gitlab-ci.yml ，把构建、检查及部署任务设置好，一旦通过前置条件，就能自动地把产品包发布到各个环境。

这种代码与 CI 一体化的做法，有哪些优点呢？无需在不同的系统中设置访问权限，不用到不同的系统中查看 CI 的结果，自主权掌握在研发手中。。。。。。
特别适合开发阶段时不时需要优化 CI 策略的场景。
 
想起这些好处，忍不住鞭策自己抓紧行动起来，赶快搭建 GitLab 的 runner 吧。

### 个人搭建步骤
* 在个人电脑上安装好 docker
* docker 设置 File Sharing（/srv/gitlab/config ，/srv/gitlab/logs，/srv/gitlab/data）
* 用 docker 搭建好 GitLab 服务
* 用 docker 搭建好 GitLab runner
* 注册 GitLab runner

### docker 命令

* 创建 container 运行 GitLab 服务 

```
docker run --detach \
	--hostname 172.17.0.1 \
	--publish 443:443 --publish 80:80 --publish 22:22 \
	--name gitlab \
	--restart always \
	--volume /srv/gitlab/config:/etc/gitlab \
	--volume /srv/gitlab/logs:/var/log/gitlab \
	--volume /srv/gitlab/data:/var/opt/gitlab \
	gitlab/gitlab-ce:latest
```

* 创建 container 运行 GitLab-runner 服务

```
docker run -d --name gitlab-runner --restart always \
  -v /srv/gitlab-runner/config:/etc/gitlab-runner \
  -v /var/run/docker.sock:/var/run/docker.sock \
  gitlab/gitlab-runner:latest

```

* 为某个 GitLab project 注册 runner

```
docker run --rm -t -i -v /srv/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner register

  Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com/):
  http://172.17.0.1/
  Please enter the gitlab-ci token for this runner:
  
  Please enter the gitlab-ci description for this runner:

  Please enter the gitlab-ci tags for this runner (comma separated):

  Registering runner... succeeded                     runner=TfUm_2zL
  Please enter the executor: docker, parallels, shell, docker-ssh+machine, kubernetes, docker-ssh, ssh, virtualbox, docker+machine:
  docker
  Please enter the default Docker image (e.g. ruby:2.1):
  gitlab
  Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded!
```

* 进入到 container中 

```
docker exec -it <container name> /bin/bash
```

* 查看 container 的日志

```
docker logs -f container_name
```

### 启动 GitLab container 报错的处理

* 文件共享的问题

```
$ docker run --detach     --hostname 172.17.0.1     --publish 443:443 --publish 80:80 --publish 22:22     --name gitlab-02     --restart always     --volume /Users/Shared/gitlab/config:/etc/gitlab     --volume /Users/Shared/gitlab/logs:/var/log/gitlab     --volume /Users/Shared/gitlab/data:/var/opt/gitlab     gitlab/gitlab-ce:latest
984166f405e804998fc93bc2f64e9ebedac313de8f519b26134841d9f0a69530
docker: Error response from daemon: Mounts denied:
The paths /Users/Shared/gitlab/logs and /Users/Shared/gitlab/config and /Users/Shared/gitlab/data
are not shared from OS X and are not known to Docker.
You can configure shared paths from Docker -> Preferences... -> File Sharing.
See https://docs.docker.com/docker-for-mac/osxfs/#namespaces for more info.
```
* 文件权限问题，详见：https://gitlab.com/gitlab-org/omnibus-gitlab/issues/2976


### 参考资料

* https://docs.gitlab.com/omnibus/docker/
* http://phase2.github.io/devtools/common-tasks/ssh-into-a-container/
* https://gitlab.com/gitlab-org/gitlab-runner/blob/master/docs/install/docker.md
* https://serverfault.com/questions/814164/connect-gitlab-and-gitlab-runner-both-in-docker (发现不用link，runner也能正常register)
  
