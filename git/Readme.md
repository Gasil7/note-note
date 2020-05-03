## git命令

### git log

识别和检索变更历史

* git log 

> 不使用任何选项，log命令会显示SHA1（commit id）、Auther、Date、以及提交消息以倒序方式排列

* git log --patch

> 补丁，意味着会显示变更间的补丁（差异），显示类似于diff命令
* git log -n(n为数字)

> 显示最近n条提交

* git log --stat

> 会额外显示关于变更数量的统计信息（某个文件的插入行、删减行的数量）

* git log --oneline

> 会显示每个提交的提交消息的第一行，所以说我们要让自己的每一个提交消息都变得有意义