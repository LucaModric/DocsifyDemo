## 文档框架

同博客框架 WordPress、Hexo 等一样，Web 文档也有自己的框架，如比如 Java 的 Javadoc，Python 的 pydoc，以及Python-sphinx。对于 Python 有专门文档标记语言 reStructuredText（RST），常见的 Python 各种库和工具的帮助文档基本都是用 RST 所写。如 Requests、Flask、Scrapy 等。

![在这里插入图片描述](https://img-blog.csdnimg.cn/552ecc15d6dd469a990d35a3b251d09f.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2NTIxNzg1,size_16,color_FFFFFF,t_70)

不过，用 RST 编写对于已经会了 Markdown（更为流行） 的读者来说，有点浪费，而且两者的语法差异较大，容易造成记忆冲突。幸运的是有了 mkdocs，不仅能轻松制作类似 Scrapy 帮助文档的文档项目，而且支持 markdown 语法。

## 使用MkDocs

### 安装 MkDocs

```shell
pip install mkdocs
```

### 创建项目

执行下面命令就在当前目录下，生成一个 testdocs 文件夹，就是创建的文档项目

```shell
mkdocs new testdocs
```

cd命令进入文件夹，查看结构

![在这里插入图片描述](https://img-blog.csdnimg.cn/2414b736f7304e6bbf8967763545d9a5.png)

+   mkdocs.yml 为配置文件
+   docs 文件夹中为文档文件目录，文件使用 markdown 编写

### 文档预览

进入 创建的文档项目目录，执行 `mkdocs serve`：

```shell
mkdocs serve

INFO     -  Building documentation...
INFO     -  Cleaning site directory
INFO     -  Documentation built in 0.16 seconds
INFO     -  [18:16:18] Serving on http://127.0.0.1:8000/
```

将启动一个 Web 服务器，用于预览 testdocs 文件项目，效果如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/411562f0879f4d7b8557bfd67713df97.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2NTIxNzg1,size_16,color_FFFFFF,t_70)

### 进行配置

mkdocs 的配置简单明了，采用 yml 格式：

```yml
site_name: MkLorum
site_url: https://example.com/
nav:
    - Home: 'index.md'
    - About: 'markdown.md'
theme: readthedocs
```

当文档比较复杂时，可以通过嵌套的方式对 nav 进行配置，例如在 Home 下还有子菜单，menu1 和 menu2：

```yml
nav:
    - Home: 'index.md'
    - 'User Guide':
        - 'Writing your docs':
            - Menu1 : 'menu1.md'
            - Menu2 : 'menu2.md'
        - 'Styling your docs': './style/styling-your-docs.md'
    - About:
        - 'License': 'license.md'
        - 'Release Notes': 'release-notes.md'
```

效果如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/2f3c1d03b5774870b9a80a9add6e138e.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2NTIxNzg1,size_16,color_FFFFFF,t_70)

+   如果菜单名中有空格需要用引号(单双皆可)括起来
+   文档文件不要同导航结构配合，可以为导航配置相对文件路径
+   菜单层级可以无限嵌套
+   `默认情况下，即在不配置导航 (nav) 的情况下，会按照文件名，目录结构生成导航菜单`

### 更换主题

下载主题：

```shell
pip install mkdocs-material mkdocs-windmill
```

mkdocs.yml里添加:

```yml
theme:
  name: 'material'
# 也可以选bootstrap
```

其他的一些配置：

```yaml
theme:
  name: "material"
  # logo: 'images/logo.svg'
  logo:
      icon: "mkdocs"
  palette:
      primary: "black"
      accent: "deep orange"
  language: "zh"
```

material页面风格：

![在这里插入图片描述](https://img-blog.csdnimg.cn/ddb6f76840d34d1ab9286781597b689b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2NTIxNzg1,size_16,color_FFFFFF,t_70)

更多主题：[https://github.com/mkdocs/mkdocs/wiki/MkDocs-Themes](https://github.com/mkdocs/mkdocs/wiki/MkDocs-Themes)

### 一些约定

+   站点首页 默认情况下，必须创建一个 index.md 作为站点首页。同时也支持 README.md 作为首页，会将其转化为 index.html。如果 index.md 和 README.md 同时存在，将忽略 README.md
+   非 markdown 文件 markdown 文件，即扩展名为 md 的文件，会被转化为 html。非 markdown 文件，会被原封拷贝，不做任何修改
+   内部链接 如果需要引用另一个文件，只需要按照 markdown 链接的方式，连接到这个文件就可以了，例如 `[详情请参考](./detail.md)`。不要担心文件名，因为生成站点时会自动换成 html 文件路径

### 生成站点

执行`mkdocs build`命令，生成站点，点击`index.html`即可

```shell
mkdocs build
```

## 使用sphinx

### 安装sphinx和主题

```shell
pip install sphinx sphinx_rtd_theme
```

### 创建项目

创建一个文件夹后，执行命令

```shell
sphinx-quickstart
```

### 编写文档

![](https://img-blog.csdn.net/20181022165849402?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTAzODYxMjE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### 修改主题

在conf.py文件中添加这两行代码，修改主题

```python
import sphinx_rtd_theme
html_theme = 'sphinx_rtd_theme'

# 记得删除下面的html_theme = 'alabaster'
```

更多主题请参考：[https://sphinx-themes.org/](https://sphinx-themes.org/)

### 构建站点

在根目录输入命令，即可生成网站构建。在build/html目录下即可看到生成的网站

```shell
make html
```

点击index.html即可查看

![](https://img-blog.csdn.net/20181022170849771?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTAzODYxMjE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

## 使用Teadocs

[https://blog.csdn.net/qq\_37608398/article/details/90636928](https://blog.csdn.net/qq_37608398/article/details/90636928)

## docsify

[https://docsify.js.org/#/zh-cn/](https://docsify.js.org/#/zh-cn/)  
docsify是一个超级好用的文档站点生成器！特点是使用简单，跟着官网教程输入两行命令就能完成安装和生成站点了，生成的文档样式也很精简优雅，并且是响应式的，手机上看也很不错。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/f9c659046e8748e78170145726705426.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA56y85Lit5bCP5aSc6I66,size_20,color_FFFFFF,t_70,g_se,x_16)

## Dumi

[https://d.umijs.org/zh-CN](https://d.umijs.org/zh-CN)

阿里推出的文档站点生成工具，也是输入几行命令就能得到文档网站。和 docsify 不同的是，Dumi 专为 组件开发 场景而生，很适合作为组件库的文档。可以嵌入和折叠代码块、提供组件在终端中的浏览效果等，Dumi 生成的网站很精简，而且封面支持自定义特性的展示，因此也很适合作为项目或产品的官方文档。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/5da3ddec3ebd408e81ee529bd84b3264.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA56y85Lit5bCP5aSc6I66,size_20,color_FFFFFF,t_70,g_se,x_16)