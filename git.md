# git

## git 直接覆盖本地
```cmd
git fetch --all  
git reset --hard origin/master 
git pull
```

## git合并分支上指定的commit
merge 在遇到特殊情况时并不能完美支持，假设有bug需要修复但不需要全部发布，可以合并指定的commit。
假设分支结构如下：
dd2e86 - 946992 - 9143a9 - a6fd86 - 5a6057 [master]
                  \
                76cada-62ecb3-b886a0[feature]
再假设 62ecb3 的提交修复了bug，这时候可以用
cherry pick 合并单个 commit
具体操作：
```cmd
git checkout master
git cherry-pick 62ecb3
```
cherry pick 连续多个commit
cherry pick 虽好，但一次只能合并一个commit。合并多个就要用到 rebase 了。再次假设想要把 76cada 和 62ecb3 合并到 master 上。
操作:
```cmd
git checkout -b newbranch 62ecb3
git rebase —onto master 76cada^
```
76cada^ 表示从 76cada 的 commit 开始合并（作为新的commit）。这样就完成了 76cada 到 62ecb3
 合并到 master。
