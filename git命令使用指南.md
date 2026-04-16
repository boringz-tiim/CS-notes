#Git命令使用指南
### 更新操作
```
git add .
git commit -m "更新笔记"
git push
```
### 把远程仓库拉下来进行合并然后再推送
```
git pull origin main --rebase
git push origin main
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
# Git 查找历史版本完整指南

## 一、核心结论

通过 **commit（提交记录）** 可以找到任意历史版本代码。

👉 不需要记住 commit ID，只需要通过记录查找即可。

---

## 二、查看提交记录（最常用）

### 1. 查看完整提交记录

```bash
git log
```

示例：

```bash
commit a1b2c3...
Author: xxx
Date: xxx

    完成JWT拦截器
```

---

### 2. 简洁版（推荐🔥）

```bash
git log --oneline
```

示例：

```bash
a1b2c3 完成JWT拦截器
d4e5f6 修复登录bug
g7h8i9 初始项目
```

👉 优点：一眼找到需要的版本

---

## 三、在 GitHub 上查找

进入仓库 → 点击 **Commits**

可以：

* 按时间查找
* 按提交说明查找
* 查看每次修改内容（diff）

---

## 四、按文件查找历史（很实用）

### 查看某个文件的修改记录

```bash
git log 文件名
```

示例：

```bash
git log JwtTokenAdminInterceptor.java
```

👉 只显示该文件的修改历史

---

## 五、查看代码是谁修改的（进阶）

```bash
git blame 文件名
```

作用：

* 查看每一行代码的修改人
* 查看对应的 commit

---

## 六、找回误操作（救命命令🔥）

```bash
git reflog
```

作用：

* 记录所有操作历史（包括回退、切换分支）
* 可以找回丢失的 commit

---

## 七、良好习惯（非常重要）

### ❌ 错误写法

```bash
git commit -m "修改"
```

### ✅ 正确写法

```bash
git commit -m "完成JWT拦截器token校验"
```

👉 提交信息越清晰，越容易找回代码

---

## 八、总结

👉 Git 通过 commit 记录所有代码变更历史
👉 可以通过 log / GitHub 页面查找任意版本
👉 不需要记 commit ID，只需要看提交记录即可
