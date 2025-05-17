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
---------------------------------------------------------------------------------------
如何管理.assert等超过100MB的大文件？以LightData.assert为例
在push本地的资源时，发现报错：xxx文件为105MB，超过了100MB上限
此时需要使用git-lfs对大文件进行管理，正常的使用方式是添加一个.gitattributes文件，然后将需要的文件后缀名与git-lfs关联。
但是，git-lfs的免费额度有上限。因此我只能单独处理大文件LightData。
修改了.gitattribute后,我尝试重新上传，但是并没有成功。
原因是git的提交历史中有大文件，因此需要使用git-filter-repo对提交的历史记录进行删除。
# git filter-repo --strip-blobs-bigger-than 100M
# git push --force
但是在安装git-filter-repo时我遇到了问题：
即使我已经将文件移动到了PATH：/usr/local/bin/系统仍然无法找到git-filter-repo
我使用命令ls -l后才发现，原来是文件的权限问题。自己创建的文件只有rw写权限，而想要它能被系统执行，则还需要赋予它x的执行权限：
chmod +x git-filter-repo
----------------------------------------------------------------------------------------
