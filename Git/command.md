# git 常用命令

***

1.  添加远程仓库 
    $git remote add 项目git地址
2.  diff 
    1. 提交之前，与最后一次提交记录做比较，修改内容
        *. $ git diff HEAD 在add前后都可用
        *. $ git diff --staged 在add后使用
    2. 比较两个分支
        *. $ git diff <branch1>...<branch2.
3. 删除远程仓库文件，但在本地保留
    $ git rm --cached <file>
4. 重命名
    $ git mv <file-original> <file-renamed>
5. 列出文件的提交记录
    $ git log --follow <file>
6. 列出提交内容
    $ git show <commit>
7. 撤销到某次提交记录，但在本地保留
    $ git reset <commit>
8. 撤销提交的文件
    $ git reset <file>
9. 放弃所有历史记录并将其更改回指定的提交
    $ git reset --hard <commit>
10. 列出所有ignore 文件
    $ git ls-files --other --ignored --exclude-standard
11. stash
    1. 临时存储所有修改的跟踪文件
        $ git stash
    2. 列出所有临时存储记录
        $ git stash list
    3. 恢复最后一次临时存储
        $ git stash pop
    4. 放弃最近临时存储
        $ git stash drop
    5. 清空临时存储
        $ git stash clean
12.

