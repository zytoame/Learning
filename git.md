
上传步骤
- git init
<<<<<<< HEAD
- git status
- git add .
- git commit -m "提交的注释"
=======
- git add .
- git commit -m "Initial commit"
>>>>>>> 336dda0a7bd2fa0ce0eb3bf30bfa41f2dd45d9b8
- git remote add origin https://github.com/yourusername/your-repo.git
- git branch -m master main  # 重命名本地分支
- git push -u origin main
- 
上传大于100MB大文件到github上可以参考网站：blog.csdn.net/wzk4869/article/details/131661472


- **删除已提交的 `build/` 文件**（如果不想保留历史记录）：
    git rm -r --cached build/  # 从 Git 中移除，但保留本地文件
    git commit -m "移除 build 目录"
    git push origin main

touch .gitignore
notepad .gitignore  # 用记事本打开
```notepad
# 忽略 build 目录
build/
*.obj
*.pdb
*.ilk

# 忽略系统文件
.DS_Store
Thumbs.db

# 忽略 IDE 配置文件
.vscode/
.idea/
```
 **让 Git 生效**
如果之前已经提交了本应忽略的文件（如 `build/`），需要从 Git 缓存中移除：
```
git rm -r --cached build/  # 移除 build 目录的跟踪
git add .gitignore         # 添加 .gitignore
git commit -m "更新 .gitignore，忽略 build 目录"
git push origin main       # 同步到远程
```