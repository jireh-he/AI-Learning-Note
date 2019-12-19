# Jupyter Lab学习——新一代的在线笔记本
<a href='../readme.md'>返回上页</a>

##  一. Jupyter Lab总览

新一代基于web的项目管理集成环境，功能比单纯的notebook强大，notebook笔记请从此跳转:

[notebook笔记](Jupyter-notebook.md)

以下是Jupyter Lab的界面：

![Jupyter总览](images/interface_jupyterlab.png)

集成Jupyter notebooks,文本编辑，终端和其他扩展定制插件。

* 代码控制台：可交互式执行代码
* 可在文档中执行实例代码
* 生成Dashboard仪表盘
* 支持多种文档可视化，包括Markdown等

## 二. Jupyter Lab安装和启动

***conda*** 

```bash
conda install -c conda-forge jupyterlab
```

***pip***

```bash
pip install jupyterlab
```

***docker*** 全量安装

```bash
docker pull jupyter/all-spark-notebook
```

**启动jupyter lab**

```bash
docker run -d -v /home/DockerData/lab:/home/jovyan -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes --name mylab jupyter/all-spark-notebook
```

启动从浏览器输入http://IP:8888/lab可以进入主页

## 三. Jupyter Lab的安全性，设置密码

开启Jupyter终端进入命令:

```bash
jupyter notebook --generate-config
```

生成文件$HOME/.jupyter/jupyter_notebook_config.py,编辑文件设置

> c.NotebookApp.allow_password_change = True

只要把前面的注释"#"去掉就可以。为了安全，也不要使用root启动服务：

> c.NotebookApp.allow_root = False

然后在终端执行命令生成密码

```bash
jupyter notebook password
```

密码文件保存在$HOME/.jupyter/jupyter_notebook_config.json

> {
>   "NotebookApp": {
>     "password": "sha1:e769777c596f:3438a7e84bff50a2d55922312ba2a650c95f8f47"
>   }
> }





