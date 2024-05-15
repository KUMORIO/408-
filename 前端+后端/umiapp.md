## umi

  App running at:

  - Local:   http://localhost:8000 (copied to clipboard)
  - Network: http://192.168.56.1:8000

![kkk](C:/Users/Lenovo/Pictures/Snipaste_2023-11-21_15-22-52.png)

配置过程
>[快速上手 (umijs.org)](https://v3.umijs.org/zh-CN/docs/getting-started)
>
>

## umi路由配置效果

### 子路由

+ 路由配置

```react
  routes: [
    { path: '/', component: '@/pages/index' },
    {path:'/user',
      component:'@/layouts/index',
      routes:[
        {path:'/user/one',component:'@/pages/index'},
        {path:'/user/two',component:'@/pages/user'},
      ]},
  ],
```

+ pages\index.tsx

```typescript
import styles from './index.less';

export default function IndexPage() {
  return (
    <div>
      <h1 className={styles.title}>Page index</h1>
    </div>
  );
}
```

+ layouts\index.tsx

```typescript
import React from 'react';

const Index = (props:any) => {
    return (
        <div>
            <h2>Header</h2>
            {props.children}
            <h2>Footer</h2>
        </div>
    );
};

export default Index;

```

+ 效果图片

![](C:/Users/Lenovo/Pictures/%E8%B7%AF%E7%94%B1one.png)



![](C:/Users/Lenovo/Pictures/%E8%B7%AF%E7%94%B1two.png)

### 重定向-redirect

```typescript
{path:'/list',redirect:'/user/one'},
```

![image-20231121170626211](C:/Users/Lenovo/AppData/Roaming/Typora/typora-user-images/image-20231121170626211.png)

## 换源

![image-20231128100535006](C:/Users/Lenovo/AppData/Roaming/Typora/typora-user-images/image-20231128100535006.png)