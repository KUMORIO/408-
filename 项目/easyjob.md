# 项目构建

### 用nvm控制node.js版本

C:\Program Files\nodejs

nvm list available  

nvm install 16.20.0           

nvm use 16.20.0                

### 更换缓存，镜像源

```c
sudo npm -g install npm@16.20.0
nvm install 16.20.0           
npm cache clean --force
npm config set registry https://registry.npmmirror.com
npm config get proxy
npm install npm@8.19.4 -g
npm install -g npm@8.19.4
```

npx -p npm@6 npm install -g npm@8.19.4

### 步骤1

npm init vite@latest easyjob-front-admin

### 步骤2

cd easyjob-front-admin

### 步骤3

npm install axios echarts element-plus js-md5 sass sass-loader suneditor vue-cookies vue-router --save

npm cache verify = npm cache clean --force

### 代码位置

E:\Vue\brush-question-app\brush-question-app

### 数据库建立

表名称easy_job



```sql
CREATE TABLE `sys_account` (
  `user_id` int(11) NOT NULL AUTO_INCREMENT COMMENT '用户ID',
  `phone` varchar(11) DEFAULT NULL COMMENT '手机号',
  `user_name` varchar(20) DEFAULT NULL COMMENT '用户名',
  `password` varchar(32) DEFAULT NULL COMMENT '密码',
  `position` varchar(150) DEFAULT NULL COMMENT '职位',
  `status` tinyint(1) DEFAULT '1' COMMENT '状态 0:禁用 1:启用',
  `roles` varchar(100) DEFAULT NULL COMMENT '用户拥有的角色，多个用逗号隔开',
  `create_time` datetime DEFAULT NULL COMMENT '创建时间',
  PRIMARY KEY (`user_id`),
  UNIQUE KEY `idx_phone` (`phone`)
) ENGINE=InnoDB AUTO_INCREMENT=1000000 DEFAULT CHARSET=utf8mb4 COMMENT='账号信息';

```



mvn clean install -U

# 项目架构

# login模块

## 输入网址

```txt
http://127.0.0.1:9091/api/login?phone=18688886666&password=47ec2dd791e31e2ef2076caf64ed9b3d&checkCode=vzquw
```



