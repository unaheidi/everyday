---
layout: post
---

## 升级的意义

###  增加或优化了哪些功能点？

* 加强代码review的控制力度。

  1）除了“comment”还提供了“start discussion”发表意见的方式。
  Merge Reuest里面的discussion或者某个commit中添加的意见，不仅可以用来发表普通的评论，还可以用来当作发起正式的讨论。
  好处在于，如果代码reivew的过程中查出了问题，并且要求作者必须关注该问题，那么，这样的意见就可选择“start discussion”，
  而不要选择“comment”。在Merge Request的时候，还能设置“Only allow merge requests to be merged if all discussions are resolved”，
  这种方式下，要求所有的disscution都必须先解决掉才能完成merge。
  
  2）加强了merge的质量。
  包括上面提到的“解决掉discussion后才能merge“，”pipeline的状态为成功的才能被merge“
  
* 全面增强GitLab-CI的功能
  
  1）支持注册私有的容器跑build。
  2）
