## 基本流程
1. git clone 复制到本地  
2. git checkout -b new-feature 建立新分支
3. 修改
4. git diff 查看修改
5. git add, git commit, git push origin new-feature 提交新分支
6. git checkout main 切换回本地main
7. git pull origin maim 同步远端main
8. git check out new-feather，git rebase main 切换到新分支后同步main分支的最新改动
9. 解决冲突
10. git push -f origin new-feather 提交新分支（此时带有new-feature和main分支的新改动）
11. pull request
12. git branch -D my-feature 删除本地的新分支（之后要把远端的新分支删除）  
13. git pull orgin main 拉取远端最新分支，为下一次修改做准备
## 注意
- 参考自[video](https://www.bilibili.com/video/BV19e4y1q7JJ)
- 接受Pr时**尽量**使用squash and merge
- **必须**先fork
