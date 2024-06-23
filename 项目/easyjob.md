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

## 验证码

### 前端

```js
       <img
              :src="checkCodeUrl"
              class="check-code"
              @click="changeCheckCode"
            />
                  
//验证码
const checkCodeUrl = ref(null);
const changeCheckCode = () => {
  checkCodeUrl.value = `${api.checkCode}?time=${new Date().getTime()}`;
};

```

### 后端

```java
// 导入所需的包
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

// 使用Spring的注解来映射请求路径
@RequestMapping("/checkCode")
public void checkCode(HttpServletResponse response, HttpSession session) throws IOException {
    // 创建一个验证码图片对象，参数依次为：宽度、高度、字符数、干扰线数量
    CreateImageCode vCode = new CreateImageCode(130, 38, 5, 10);
    
    // 设置响应头，告诉浏览器不缓存这个响应
    response.setHeader("Pragma", "no-cache");
    response.setHeader("Cache-Control", "no-cache");
    response.setDateHeader("Expires", 0);
    
    // 设置响应内容类型为JPEG图片
    response.setContentType("image/jpeg");
    
    // 获取生成的验证码字符串
    String code = vCode.getCode();
    
    // 将验证码字符串存储到会话中，以便后续验证使用
    session.setAttribute(Constants.CHECK_CODE_KEY, code);
    
    // 将验证码图片写入HTTP响应的输出流中，返回给客户端
    vCode.write(response.getOutputStream());
}

```



## 输入网址

```txt
http://127.0.0.1:9091/api/login?phone=18688886666&password=47ec2dd791e31e2ef2076caf64ed9b3d&checkCode=vzquw
```

# 八股文管理

## 批量发布

### 前端代码

#### src\views\content\QuestionList.vue

template

```html
<el-button

​         :disabled="selectRowList.length == 0"

​         type="primary"

​         @click="postQuestionBatch"

​         v-has="proxy.PermissionCode.question.post"

​         \>批量发布

</el-button>
```

js

```js
const selectRowList = ref([]);
const rowSelected = (rows) => {
  selectRowList.value = rows.map((item) => {
    return item.questionId;
  });
};
```



```js
const postQuestionBatch = (params, url) => {
  proxy.Confirm(`确定要发布这${selectRowList.value.length}条记录吗？`, () => {
    postQuestionDone(selectRowList.value.join(","));
  });
};

const postQuestionDone = async (questionIds) => {
  let result = await proxy.Request({
    url: api.postQuestion,
    params: {
      questionIds,
    },
  });
  if (!result) {
    return;
  }
  proxy.Message.success("发布成功");
  loadDataList();
};
```

#### logic:

selectRowList -->获取 questionIds-->post请求到api.postQuestion-->后端

### 对应后端代码

#### com/easyjob/controller/QuestionInfoController.java

```java
 @RequestMapping("/postQuestion")
    @GlobalInterceptor(permissionCode = PermissionCodeEnum.QUESTION_POST)
    public ResponseVO postQuestion(@VerifyParam(required = true) String questionIds) {
        updateStatus(questionIds, PostStatusEnum.POST.getStatus());
        return getSuccessResponseVO(null);
    }
```



​        
