#Git命令使用指南
### 更新操作
```
git add .
git commit -m "更新笔记"
git push
```
## 一.仓库管理
### 1.初始化仓库

bash:

```
git init
```

### 2.克隆仓库

bash:

```
git clone <repository>
```

## 二.基本操作
### 1.添加文件

bash:

```
git add <file>
```

### 2.提交更改

bash:

```
git commit -m "commit message"
```

### 3.查看状态

bash:

```
git status
```

### 4.查看提交历史

bash:

```
git log
```

### 5.撤销更改

bash:

```
git reset HEAD <file>
```

### 6.删除文件

bash:

```
git rm <file>
```

### 7.分支管理

#### 7.1 创建分支

bash:

```
git branch <branch-name>
```

#### 7.2 切换分支

bash:

```
git checkout <branch-name>
```

#### 7.3 合并分支

bash:

```
git merge <branch-name>
```

#### 7.4 删除分支

bash:

```
git branch -d <branch-name>
```

### 8.远程仓库

#### 8.1 关联远程仓库

bash:

```
git remote add origin <repository>
```

#### 8.2 推送到远程仓库

bash:

```
git push -u origin master
```

#### 8.3 从远程仓库拉取

bash:

```
git pull
```

## 三.其他命令

### 1.显示当前配置

bash:

```
git config --list
```

### 2.设置用户名和邮箱

bash:

```
git config --global user.name "your name"
git config --global user.email "your email"
```

### 3.创建.gitignore文件

bash:

```
touch.gitignore
```

### 4.忽略文件

在.gitignore文件中添加需要忽略的文件或目录，如：

```
# Ignore node_modules directory
node_modules/

# Ignore all .txt files in the root directory
*.txt
