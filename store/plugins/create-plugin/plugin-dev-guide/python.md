# Python 插件开发指引

## 插件开发框架说明 <a id="%E6%8F%92%E4%BB%B6%E5%BC%80%E5%8F%91%E6%A1%86%E6%9E%B6%E8%AF%B4%E6%98%8E"></a>

* 开发者可以使用自己喜欢的框架开发，没有硬性要求
* 示例以源码发布包的方式来组织插件
  * 优点：跨平台，包简单小巧
  * 缺点：执行前需使用 pip 安装，当有其他第三方包依赖时，需能访问镜像源安装依赖包

**一、插件代码工程的整体结构示例如下：**

```text
|- ${你的插件标识}             # 插件包名
    |- ${你的插件标识}         # 插件包名
        |- __init__.py py     # py包标识
        |- command_line.py    # 命令入口文件
    |- python_atom_sdk        # 插件开发SDK包
    |- MANIFEST.in            # 包文件类型申明
    |- requirements.txt       # 依赖申明
    |- setup.py               # 执行包打包配置
```

**二、如何开发插件：**

> 参考 [plugin-demo-python](https://github.com/ci-plugins/plugin-demo-python)

* 创建插件代码工程

  插件代码建议统一管理。通用的开源插件可以放到 [ci-plugins](https://github.com/ci-plugins) 下

* 修改包名为有辨识度的名称，建议可以和插件标识一致
* 实现插件功能
* 规范：
  * [插件开发规范](../plugin-specification.md)
  * [插件输出规范](../plugin-output.md)

**三、如何打包发布：**

1. 进入插件代码工程根目录下
2. 执行打包命令打包

   ```text
   # 本示例以 setuptools 的 sdist 命令为例

   python setup.py sdist
   ```

3. 在任意位置新建文件夹，命名示例：release\_pkg = ${你的插件标识}\_release
4. 将步骤 2 生产的执行包拷贝到 ${release\_pkg} 下
5. 添加 task.json 文件到 ${release\_pkg} 下 task.json 见示例，按照插件功能配置。

   * [插件配置规范](../plugin-config.md)
   * task.json示例：

   ```text
   {
       "atomCode": "demo",
       "execution": {
           "language": "python",
           "packagePath": "demo-1.1.0.tar.gz",             # 发布包中插件安装包的相对路径
           "demands": [
               "pip install demo-1.1.0.tar.gz --upgrade"   # 执行 target 命令前需进行的操作，如安装依赖等
           ],
           "target": "demo"
       },
       "input": {
           "inputDemo":{
               "label": "输入示例",  
               "type": "vuex-input",
               "placeholder": "输入示例",
               "desc": "输入示例"
           }
       },
       "output": {
           "outputDemo": {
               "description": "输出示例",
               "type": "string",
               "isSensitive": false
           }
       }
   }
   ```

6. 在 ${release\_pkg} 目录下，把所有文件打成 `zip` 包即可

`zip` 包结构示例：

```text
|- demo_release.zip         # 发布包
   |- demo-1.1.0.tar.gz    # 插件执行包
   |- task.json            # 插件配置文件
```

打包完成后，在插件工作台提单发布，即可测试或发布插件

