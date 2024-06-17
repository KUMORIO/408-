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

