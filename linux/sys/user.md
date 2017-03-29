## 建用户：
adduser name
passwd name

## 建工作组
groupadd group-name

## 新建用户同时增加工作组
useradd -g group-name name

## 显示用户信息
id user
cat /etc/passwd

## 删除用户
userdel name
