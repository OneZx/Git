#### Showing Your Remotes

`git remote`. It lists the shortnames of each remote handle you’ve specified.
列出指定的每一个远程服务器的简写,如果已经克隆了自己的 repository,那么至少能看到`origin`,这是 clone repository 服务器的默认名字

```
$ git remote
origin
```

- `git remote -v`. 会列出 `urls` 和 `shortname of remote`

```
$ git remote -v
origin  git@github.com:OneZx/Git.git (fetch)
origin  git@github.com:OneZx/Git.git (push)
```

#### Adding Remote Repositories

- `git remote add <shortname> <url>` ,指定一个远程仓库的简写名称 shortname
- `git remote -v` 查看刚才添加的

- `git fetch <remote-name>` fetch 拉取远程仓库中有但自己没有的信息,我们可以直接使用`<remote-name>`

The command goes out to that remote project and pulls down all the data from that remote project that you don’t have yet.执行完后,将会拥有那个 repository 中所有分支的引用,可以随时合并或查看

- ps.`git fetch`会将数据拉取到本地仓库,但并不会自动合并或修改当前的工作,You have to merge it manually into your work when you’re ready.

If your current branch is set up to track a remote branch (see the next section and Git Branching for more information), you can use the `git pull` command to automatically `fetch and then merge` that remote branch into your current branch.

- `git pull`命令会`fetch`数据并且 `merge` remote branch 到 current branch,运行 git pull 通常会从最初克隆的服务器上抓取数据并自动尝试合并到当前所在的分支。

#### Pushing to Your Remotes

- `git push [remote-name] [branch-name]` 将 master 分支推送到 origin 服务器时(git clone 一个 repository 会自动设置好这两个名字)

```
$ git push origin master
```

如果在 push 之前有人 push 过了,当前推送就会被拒绝,需要先 pull 下来(fetch and merge)合并到自己的里之后才能推送

**查看 remote repository**

```
$ git remote show origin  // show <remote-name>
```

#### Renaming and Removing Remotes

- 重命名 名为 test 的远程仓库 为 haha

```
$ git remote rename test haha
```

这同样也会修改远程分支名字,那些过去引用 test/master 的现在会引用 haha/master

- 移除某个远程仓库

```
$ git remote rm <remote-name>
```

## Git Branching

#### Creating a New Branch

let's create a new bracnch called `testing`, this creates a new pointer for you to move around.
创建了一个可以移动的指针

```git
$ git branch testing
```

Git keeps a special pointer called `HEAD`, In Git, this is a pointer to the local branch you're currently on. `git branch` 命令仅仅创建了一个新分支,并不会自动切换到新分支中去,`HEAD`仍指向主分支`master`

We can easily see this by running a simple `git log` command that shows us where the branch pointers are pointing. This option is called `--decorate`

```git
$ git log --oneline --decorate
4b8a874 (HEAD -> master, origin/master, testing) add reset to specified commit
40e04a0 add remote repository command
451279f 添加撤销操作git reset
229054e git使用说明md笔记,添加部分
7186a23 git使用说明md笔记第二章
```

You can see the “master” and “testing” branches that are right there next to the f30ab commit.

#### Switching Branches

To switch to an existing branch, we run the `git checkout` command.

```bash
$ git checkout testing
```

This moves `HEAD` to point to the `testing` branch.

- ps.`HEAD` points to the `current branch`

这个时候我们已经切换到 testing 分支,如果此时我们修改文件并提交

```
$ git commit -am 'test branch'
```

那么我们的 testing 分支向前移动了,但是 master 分支没有,它仍然指向原来的对象
我们切换回`master`

```git
$ git checkout master
```

It moved the `HEAD pointer back to point to the master branch`, and it reverted the files in your working directory back to the snapshot that master points to.

- 1.`HEAD`指回 master 分支, 2.工作目录恢复成 master 分支所指向的快照内容.

#### Divergent history

···git
$ git log --oneline --decorate --graph --all
···

## Basic Branching and Merging

#### Basic branching

you can run the git checkout command with the `-b` switch:
相当于新建一个 iss53 分支, 并切换到分支上, `checkout` 检出到某个分支上(HEAD 指向它)

```
$ git checkout -b iss53

// This is shorthand for
$ git branch iss53
$ git checkout iss53
```
