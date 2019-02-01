---
layout: post
---

## 第一次注意到 Review Apps

团队有意向从 GitLab CE 的 V8 升级到 V11，查看 CI 相关文档时，发现新增了 Review Apps 的新功能。
发起Merge Request的时候，我们可以借助 Review Apps，把分支部署到动态的测试环境中。这样一来，便于
产品人员、QA和开发人员一起，及时地浏览变更的效果。

## 部署到 openshift 的例子

GitLab提供了把项目部署到 openshift 的例子。在 .gitlab-ci.yml 配置文件中用到的访问 openshift 的 Secure Variables 变量，
需要根据各自的服务和账号做设置。

为了涂省力，我在openshift online上申请了账号，希望分支构建后可以部署到 openshift online 上。然而下面三个变量该怎么设置呢？
* OPENSHIFT_SERVER
* OPENSHIFT_TOKEN
* OPENSHIFT_DOMAIN

