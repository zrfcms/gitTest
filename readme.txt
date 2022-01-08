git ls-files -v -o#显示未跟踪的文件
git ls-files -v#显示跟踪的文件

git config user.name 
git config user.email 

git add readme.txt
git modify readme.txt 1
git modify readme.txt 2

初始化一个Git仓库，使用git init命令。
添加文件到Git仓库，分两步：
使用命令git add <file>，注意，可反复多次使用，添加多个文件；
使用命令git commit -m <message>，完成。

要随时掌握工作区的状态，使用git status命令。
如果git status告诉你有文件被修改过，用git diff可以查看修改内容。

git log --pretty=oneline
HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
在Git中，总是有后悔药可以吃的。当你用$ git reset --hard HEAD^回退到add distributed版本时，再想恢复到append GPL，就必须找到append GPL的commit id。Git提供了一个命令git reflog用来记录你的每一次命令：

所以，git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。

no changes added to commit (use "git add" and/or "git commit -a")
第二次的修改没有被提交？
别激动，我们回顾一下操作过程：
第一次修改 -> git add -> 第二次修改 -> git commit
你看，我们前面讲了，Git管理的是修改，当你用git add命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，git commit只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。

那怎么提交第二次修改呢？你可以继续git add再git commit，也可以别着急提交第一次修改，先git add第二次修改，再git commit，就相当于把两次修改合并后一块提交了：
第一次修改 -> git add -> 第二次修改 -> git add -> git commit
好，现在，把第二次修改提交了，然后开始小结。

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。
场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。


第1步：创建SSH Key
看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有
$ ssh-keygen -t rsa -C "youremail@example.com"
你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。




…or create a new repository on the command line
echo "# gitTest" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/zrfcms/gitTest.git
git push -u origin main

…or push an existing repository from the command line
git remote add origin https://github.com/zrfcms/gitTest.git
git branch -M main
git push -u origin main

由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令
从现在起，只要本地作了提交，就可以通过命令
git push origin main


OpenSSL SSL_read: Connection was reset, errno 10054
Solution1: （原因）自己配置的用户名，邮箱可能输入错误了。
查看用户名，邮箱
git config user.name
git config user.email</code>
修改，用户名，邮箱
git config --global user.name "xxx"
git config --global user.email "xxx"
移除仓库，重新添加
git remote rm origin
git remote add origin https://github.com/XXX

Solution2: 修改解除SSL认证。
在Git Bash中输入以下命令：
git config --global http.sslVerify "false"

Solution3: （原因）文件太大了。
改为500MB，在Git Bash中输入以下命令：
git config http.postBuffer 5242880003

Solution4: （原因）更新DNS缓存。
在cmd中输入以下命令：
ipconfig /flushdns

Failed to connect to github.com port 443 after 21091 ms: Timed out
git config --global --unset https.proxy

git config --global --unset https.proxy
git config --global http.sslVerify "false"
ipconfig /flushdns
git push origin main

删除远程库
如果添加的时候地址写错了，或者就是想删除远程库，可以用git remote rm <name>命令。使用前，建议先用git remote -v查看远程库信息：
$ git remote -v
origin  git@github.com:michaelliao/learn-git.git (fetch)
origin  git@github.com:michaelliao/learn-git.git (push)

然后，根据名字删除，比如删除origin：
$ git remote rm origin
此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。

要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
关联一个远程库时必须给远程库指定一个名字，origin是默认习惯命名；关联后，使用命令git push -u origin master第一次推送master分支的所有内容；此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；


git clone git@github.com:zrfcms/gitTest.git
push check1
push check2
push check3
push check4

git config --global --unset https.proxy
git config --global http.sslVerify "false"
ipconfig /flushdns
git push origin main
push check5

git config --global --unset https.proxy
ipconfig /flushdns
git config --global http.sslVerify "false"
git push origin main
push check6

git commit -am "push check7"
git config --global http.sslVerify "false"
ipconfig /flushdns
git config --global --unset https.proxy
git push origin main

git commit -am "push check8"
ipconfig /flushdns
git config --global http.sslVerify "false"
git config --global --unset https.proxy
git push origin main

git commit -am "push check9"
git config --global --unset https.proxy
ipconfig /flushdns
git config --global http.sslVerify "false"
git config --global --unset https.proxy
git push origin main

git commit -am "push check10"
git config --global --unset https.proxy
ipconfig /flushdns
git config --global http.sslVerify "false"
git config --global --unset https.proxy
git push origin main


git commit -am "xiaomi git push origin master"
git remote add origin https://github.com/zrfcms/gitTest.git
git config --global --unset https.proxy
ipconfig /flushdns
git config --global http.sslVerify "false"
git config --global --unset https.proxy
git push origin main

git pull
git commit -am "dell1080 commit"


问题：Failed to connect to github.com port 443: Timed out
这这个问题的原因可能是 ssh的公钥没有配置好；

修改 C:\code\Git\etc\ssh\ssh_config的配置即可

Host github.com
User git
Hostname ssh.github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_ed25519
Port 443

其中的 IdentityFile ~/.ssh/id_ed25519 需要换成自己的公钥路径；

做完以上步骤后就可以用git bash更新代码了；

git pull
git commit -am "xiaomi commit2"
git commit -am "xiaomi commit3"
git push origin main


git pull
git commit -am "dell1080 commit2"
git commit -am "dell1080 commit3"
git push origin main

empty ssh
empty ssh2

ssh-keygen -t rsa -C

ssh-keygen -t rsa -C "zrfcms@buaa.edu.com"
ssh-keygen -t rsa -C "zrfcms@gmail.com"