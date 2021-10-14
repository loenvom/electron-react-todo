# Release

> A ToDo App based on node, electron, react. Code in typescript.

## 配置项目

主要涉及到项目的初始化，不关注项目的具体实现代码， 但是更加注重对于项目的配置，
希望通过这个方法来提示开发中的体验，也更加规范。

### 配置自动重启和热加载

这里涉及到两个概念，一种是在开发的过程中项目的功能实现代码发生了更新那么就是使用热加载，也就不需要也不应该重启项目。
另外一种是项目的配置文件发生了改变那么仅使用热更新是无法使最新的配置生效的，这个时候就需要自动重启上场了。
解释完两者的区别，再来看看两者的实现方式。

#### 自动重启

使用了 nodemon 这一个库，安装方式 👇🏻

```shell
npm install nodemon --save-dev # 安装 nodemon 作为开发依赖项
```

在安装完成之后，我们在工程的根目录下创建一个名为 nodemon.json 文件，该命名为 nodemon 默认访问的配置文件，如果有需要的话也可以使用 `--config filename` 的方式来使用其他命名的配置文件，一下是 nodemon 的相关配置。

```json
// 整体的配置文件如下
{
  // 表示观察，或者说纳入监控的文件/文件路径，当检测到这些文件的变化的时候，将执行重启命令
  "watch": [
    "./*.json",
    "./src/main.ts"
  ],
  // 重启命令的定义
  "exec": "electron .",
  // 纳入监管的文件拓展名
  "ext": "json,ts",
  // 注入的环境变量
  "env": {
    "ENV": "develop"
  }
}
```

#### 热加载

使用了 electron-reload 这个库，安装方式 👇🏻

```shell
npm install electron-reload --save-dev # 安装 electron-reload 作为开发依赖项
```

使用方法，在 main.ts 也是就是项目的启动入口文件当中添加如下代码。

```typescript
try {
  require('electron-reload')(path.join(__dirname)); // 引入模块，配置监视范围 
} catch (err) {
	
}
```







