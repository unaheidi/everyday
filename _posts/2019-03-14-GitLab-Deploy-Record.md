---
layout: post
published: true
---

## GitLab部署过程的 N 个坑

最近又投入到运维的行列了。我发现自己就是个典型的劳动者，特别喜欢从事基层的工作。    
近况：GitLab忙着从V8升级到V11，有个得力的小伙跳槽谋生去了，暂时无法招聘新人。没得说，我这个3年没正经在一线服务的人，只好硬着头皮回一线啦。
   
上个月的现状：BU的业务基本走Docker化了，可我们GitLab服务的部署尚未docker化。     
本月的挑战：团队的技术骨干为GitLab整了个Docker化部署的方案，且把部署过程整理成了文档，尚未验证。    
我的任务：根据同事的文档，在测试服务器上部署公司定制的GitLab版本。    
Blog的用处：大家懂的，技术牛的人一般来说都懒得写文档，只要有写，甭管它质量如何，就算是谢天谢地了。    
            我把部署过程遇到的 N 个坑，为解决这些坑查阅过哪些资料，在这个blog里面记录一下，以便为优化部署文档做个准备。   
            
### 资料

[While doing source installation I see 'JavaScript heap out of memory'](https://gitlab.com/gitlab-org/gitlab-ce/issues/50937)  
[A Brief History of GitLab Workhorse](https://about.gitlab.com/2016/04/12/a-brief-history-of-gitlab-workhorse/)  
[mysql install](https://docs.gitlab.com/ee/install/database_mysql.html)  
[Mysql2::Error: Specified key was too long; max key length is 767 bytes: ](https://gitlab.com/gitlab-org/gitlab-ce/issues/41483)
[Gitaly](https://docs.gitlab.com/ce/administration/gitaly/)  
[gitlab-ce reset root password](https://gitlab.com/gitlab-org/omnibus-gitlab/issues/2934)  
[gitlab Import url is blocked: "Requests to the local network are not allowed"](https://gitlab.com/gitlab-org/gitlab-ce/issues/57948)  
[CentOS 7安装Ruby on Rails](https://www.jianshu.com/p/e4847f3926d1)
