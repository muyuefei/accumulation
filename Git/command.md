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
12. 把一个分支合并到另一个分支
    $ git merge source_branch goal_branch
13. 列出指定行之间的代码的修改记录
    $ git blame start_line,end_line <file>
    $ git log start_line,end_line:<file>
14. 提交历史进行二分查找，快速定位
    $ git bisect 
15. 查看某个文件提交历史及修改
    $ git log --online --decorate --stat -p <file>
        * --oneline: 标记把每一个提交压缩到了一行中。它默认只显示提交ID和提交信息的第一行.
        * --decorate: 标记让 git log 显示指向这个提交的所有引用（比如说分支、标签等）。
        * --stat: 显示每次提交插入多少行，减少多少行。
        * -p: 显示每次调具体修改内容
16. 提交按作者分类，显示提交信息的第一行
    $ git shortlog -n
17. 选项绘制一个 ASCII 图像来展示提交历史的分支结构。它经常和 --oneline 和 --decorate 两个选项一起使用，这样会更容易查看哪个提交属于哪个分支.
    $ git log --oneline --decorate --graph <file>
18. 自定义输出格式 --pretty=format:"<string>"
    $ git log --pretty=format:"<string>"
19. 提交历史过滤
    1. 按数量
        $ git log -n
    2. 按日期
        $ git log --before="2018-1-1" (等价于) $ git log --until="2018-1-1"
        $ git log --after="2018-1-1" (等价于) $ git log --since="2018-1-1"
    3. 按作者
        $ git log --author="muyuefei"
    4. 按提交信息
        $ git log --grep="xxx"
    5. 按文件内容
        $ git log -S "hello world" 可以用“-G <regex>" 正则表达式
    6. 按范围
        $ git log <since>..<utils> 
    7. 按分支, 包含了在branch_tow 分支而不在branch_one 分支的提交
        $ git log branch_one...branch_tow
>>>>>>> update command
