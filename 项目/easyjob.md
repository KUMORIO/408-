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

## java后端各个文件之间的关系---SysMenu

>SysMenuController.java(负责接收和处理 HTTP 请求)
>
>---> SysMenuService(负责业务逻辑处理-findListByParam) 
>
>---> SysMenuServiceImpl.java(具体实现-findListByParam) 
>
>--->  sysMenuMapper(数据访问层的接口-selectList)(MyBatis 框架中接口) 
>
>--->  SysMenuMapper.xml( SQL 映射文件-selectList所对应的sql语句)

>SysMenu 根据 数据库具体表的 结构对应
>
>SysMenuQuery 用于查询

com/easyjob/mappers/SysMenuMapper.xml

```xml
    <!--实体映射-->
    <resultMap id="base_result_map" type="com.easyjob.entity.po.SysMenu">
        <!--menu_id，自增主键-->
        <id column="menu_id" property="menuId"/>
        <!--菜单名-->
        <result column="menu_name" property="menuName"/>
        <!--菜单类型 0：菜单 1：按钮-->
        <result column="menu_type" property="menuType"/>
        <!--菜单跳转到的地址-->
        <result column="menu_url" property="menuUrl"/>
        <!--上级菜单ID-->
        <result column="p_id" property="pId"/>
        <!--菜单排序-->
        <result column="sort" property="sort"/>
        <!--权限编码-->
        <result column="permission_code" property="permissionCode"/>
        <!--图标-->
        <result column="icon" property="icon"/>
    </resultMap>
左边是数据库的名称column，右边是代码中对象的名称property
```

refid是mapper.xml中定义好的

refid="base_column_list"

```xml
--->       <sql id="base_column_list">
        menu_id
        ,menu_name,menu_type,menu_url,p_id,
		 sort,permission_code,icon
    </sql>

```

```xml
    <select id="selectList" resultMap="base_result_map">
        SELECT
--->        <include refid="base_column_list"/>
        FROM sys_menu
        <include refid="query_condition"/>
        <if test="query.orderBy!=null">
            order by ${query.orderBy}
        </if>
        <if test="query.simplePage!=null">
            limit #{query.simplePage.start},#{query.simplePage.end}
        </if>
    </select>
```

具体vue里的api对应的是后端路由

用来定位后端的，具体的路由，对应后端具体的controller

```js
const api = { 
  loadRole: "/settings/loadRoles",

 loadMenu: "/settings/menuList",

 saveRoleMenu: "/settings/saveRoleMenu",

 roleDetail: "/settings/getRoleByRoleId",

 delRole: "/settings/delRole",

};
```

vue的index.js是具体的网址路由

url对应具体的vue页面

```js
import { createRouter, createWebHistory } from 'vue-router'

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/login',
      name: '登录',
      component: () => import('../views/Login.vue')
    }, {
      path: "/",
      name: "layout",
      component: () => import('../views/Layout.vue'),
      children: [{
        path: "/home",
        name: "首页",
        component: () => import('../views/home/Home.vue'),
      }, {
        path: "/content/category",
        name: "分类管理",
        component: () => import('../views/content/CategoryList.vue'),
      }, {
        path: "/content/question",
        name: "八股文管理",
        component: () => import('../views/content/QuestionList.vue'),
      }, {
        path: "/content/exam",
        name: "考题管理",
        component: () => import('../views/content/ExamQuestionList.vue'),
      }, {
        path: "/content/share",
        name: "经验分享",
        component: () => import('../views/content/ShareList.vue'),
      }, {
        path: "/app/userDevice",
        name: "设备管理",
        component: () => import('../views/app/UserDeviceList.vue'),
      }, {
        path: "/app/user",
        name: "用户管理",
        component: () => import('../views/app/UserList.vue'),
      }, {
        path: "/app/carouselList",
        name: "轮播图",
        component: () => import('../views/app/CarouselList.vue'),
      }, {
        path: "/app/feedbackList",
        name: "问题反馈",
        component: () => import('../views/app/FeedbackList.vue'),
      }, {
        path: "/app/updateList",
        name: "应用更新",
        component: () => import('../views/app/UpdateList.vue'),
      }, {
        path: "/setting/menu",
        name: "菜单管理",
        component: () => import('../views/setting/MenuList.vue'),
      }, {
        path: "/setting/role",
        name: "角色管理",
        component: () => import('../views/setting/RoleList.vue'),
      }, {
        path: "/setting/user",
        name: "系统管理",
        component: () => import('../views/setting/UserList.vue'),
      },{
        path: "/test/menu",
        name: "xxx",
        component: () => import('../components/MenuComponent.vue'),
      }]
    }
  ]
})

router.beforeEach((to, from, next) => {
  const userInfo = sessionStorage.getItem("userInfo");
  if (!userInfo && to.path != "/login") {
    router.push("/login");
  }
  next();
})

export default router

```

在具体的vite.config.js文件下，定义后端路由完整格式

http://localhost:9091/api/........

```js
  server: {
    hmr: true,
    port: 5001,
    proxy: {
      "/api": {
        target: "http://localhost:9091/",
        changeOrigin: true,
        pathRewrite: {
          "^api": "/api"
        }
      }
    }
  },
```

src\utils\Request.js中规定axios，帮前端，跟后端进行数据交互

所有使用instance，的url都要加上/api

```js
const instance = axios.create({
    baseURL: '/api',
    timeout: 10 * 1000,
});
```

**`request` 函数利用了 `instance` 发送请求**，而 `instance` 配置了请求和响应的拦截器。

**请求拦截器** 在 `request` 函数发送请求前执行，主要处理加载动画的显示。

**响应择器** 在 `request` 函数接收到响应后执行，主要处理响应数据、关闭加载动画和错误处理。

**统一处理**：通过拦截器，`request` 函数的请求和响应处理逻辑被集中管理，确保一致性和可维护性。





