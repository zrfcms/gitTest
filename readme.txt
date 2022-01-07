git add readme.txt
git modify readme.txt 1
git modify readme.txt 2

git log --pretty=oneline
git reset --hard HEAD^
git reset --hard 1094a
git reflog

在Git中，总是有后悔药可以吃的。当你用$ git reset --hard HEAD^回退到add distributed版本时，再想恢复到append GPL，就必须找到append GPL的commit id。Git提供了一个命令git reflog用来记录你的每一次命令：

Git后悔药