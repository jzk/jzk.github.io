## 创建新Post

可以用下面的命令：
`hexo new post 250319_医生说我没有ADHD`

也可以直接clone一个现有的post的md文件


## Stress Free的publish过程

我本地的定时运行的`~/backup_repos.sh`脚本，会自动push change。push好change后，这个Repo的Github Action会自动build和deploy，整个过程只需1-2分钟，https://jzk.github.io/ 的内容就会更新完毕。