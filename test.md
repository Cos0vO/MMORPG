如何从历史中恢复文件，以test.md为例：
目前已经在本地删除了test.md，完成了git commit与git push操作，推送到了远程仓库。
此时该如何恢复被删除的test.md文件？

方法一：
1、先从git log中找到之前的版本
git log -- test.md
2、拿到test.md删除前的commit的hash code
git checkout asdfxzcxvzcv23r14134 -- test.md
3、查看状态：是否有new file
git status

方法二：
从上一个提交中恢复test.md，用于即使回滚
git checkout HEAD^ -- test.md

