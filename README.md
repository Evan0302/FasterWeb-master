# FasterWeb

![LICENSE](https://img.shields.io/github/license/yinquanwang/FasterRunner.svg)
> FasterWeb depend on FasterRunner

## 页面展示
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/登录.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/首页页面.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/项目概况.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/测试数据.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/驱动代码.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/驱动代码1.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/API模板.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/API模板1.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/测试用例.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/测试用例1.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/测试用例2.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/测试用例3.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/定时任务.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/定时任务1.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/定时任务2.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/定时任务3.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/环境变量.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/参数配置.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/参数配置1.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/域名管理.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/域名管理1.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/历史报告.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/excel报告.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/异步回执.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/弹出报告.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/测试报告页面.jpg)
![Image text](https://github.com/weirdohaibo/FasterWeb/blob/master/pageview/后台管理系统.jpg)

## Docker 部署nginx模式
``` 
1. 修改default.conf配置文件 server_name的ip(宿主机IP), 端口默认8080
2. 修改/src/restful/api.js baseUrl地址, 即为fastrunner容器运行的宿主机地址
3. 执行npm install, npm run build # 生成生产环境包
3. docker build -t fastweb:latest .    # 构建docker镜像
4. docker run -d --name fastweb -p8888:8888 --restart always fastweb:latest  # 后台运行docker容器
5. open url: http://宿主机ip:8888/fastrunner/login
``` 

## 本地开发环境部署

``` bash
1. 修改FasterWeb/src/restful/api.js的baseUrl配置为FasterRunner启动的ip:port
2. npm install 安装依赖包
3. npm run dev 开发环境启动服务
4. open url: http://localhost:8080/fastrunner/login
```

### 其他注意点：
- npm 安装太慢时参考：http://npm.taobao.org/
- 安装指定版本node: 
    1.  wget https://nodejs.org/dist/v8.11.4/node-v8.11.4-linux-x64.tar.xz
    2. tar xf  node-v8.11.4-linux-x64.tar.xz
    3. sudo ln -s /home/ebao/node-v8.11.4-linux-x64/bin/npm /usr/bin/npm 
    4. sudo ln -s /home/ebao/node-v8.11.4-linux-x64/bin/node /usr/bin/node
- 安装指定版本npm: sudo npm install -g npm@5.6.0 
