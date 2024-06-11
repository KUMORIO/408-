## static

### 类方法

类方法，用static写函数，直接.名字

实例方法，要new一个对象，占用堆内存

### 代码块

只运行一次

```java
static{
    
}
```

## extends

继承表示能用别人的什么东西xing

![](./../image/java/%E8%AE%BF%E9%97%AE%E6%8E%A7%E5%88%B6.png)

## Override

注释@Override，检测函数对不对

方法重写，右键，generate，选择函数

## 访问同名字变量

name方法

this.name子类

super.name父类

## 默认的构造器

子类的无参和有参构造器，都默认先调用父类的无参构造器

子类默认第一句是super()代码

父类没有无参构造器，要自己给super传参数，例如super(a,b),给父类的有参构造器传参数

### springboot视频

[3.SpringBoot Controller_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1nV4y1s7ZN?p=3&spm_id_from=pageDriver&vd_source=81d07727a431bd6b2d07b94e67a294fc)

### jdk存放地点

>C:\Users\Lenovo\.jdks\openjdk-22.0.1

### maven地址

>一个仓库

>一个apache

### springboot热部署

保存就重新启动

1添加依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId><!---->
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
```



2更改注册表，注册表没有，去高级设置找automake，打勾



setting.json

```json
"latex-workshop.latex.tools": [
      {
        "name": "pdflatex",
        "command": "pdflatex",
        "args": [
          "-synctex=1",
          "-interaction=nonstopmode",
          "-file-line-error",
          "%DOC%"
        ]
      },
      {
        "name": "xelatex",
        "command": "xelatex",
        "args": [
          "-synctex=1",
          "-interaction=nonstopmode",
          "-file-line-error",
          "%DOC%"
        ]
      },
      {
        "name": "bibtex",
        "command": "bibtex",
        "args": [
          "%DOCFILE%"
        ]
      }
    ],
  
  
    "latex-workshop.latex.recipes": [
      {
        "name": "pdflatex",
        "tools": [
          "pdflatex"
        ]
      },
      {
        "name": "xelatex",
        "tools": [
          "xelatex"
        ]
      },
      {
        "name": "xe->bib->xe->xe",
        "tools": [
          "xelatex",
          "bibtex",
          "xelatex",
          "xelatex"
        ]
      },
      {
        "name": "pdflatex -> bibtex -> pdflatex*2",
        "tools": [
          "pdflatex",
          "bibtex",
          "pdflatex",
          "pdflatex"
        ]
      }
    ],
  
    
    "latex-workshop.latex.autoBuild.run": "never",
    "latex-workshop.synctex.afterBuild.enabled": true,
  
    "latex-workshop.view.pdf.viewer": "external",
    "latex-workshop.view.pdf.external.viewer.command": "E:\\Latex\\SumatraPDF-3.5.2-64.exe",
  
    "latex-workshop.view.pdf.external.synctex.command": "E:\\Latex\\SumatraPDF-3.5.2-64.exe",
    "latex-workshop.view.pdf.external.synctex.args": [
      "-forward-search",
      "%TEX%",
      "%LINE%",
      "-reuse-instance",
      "-inverse-search",
      "\"E:\\Microsoft VS Code\\Code.exe\" -g \"%f:%l\"",
      "%PDF%"
    ],
    "latex-workshop.view.pdf.internal.synctex.keybinding": "double-click",
    "emmet.preferences": {

    },
    "editor.mouseWheelZoom": true
```

