hexo搭建

进入 Hexo官网，按照教程npm install 各种之后，生成Hexo工程，Hexo sever就启动起来了，同样你在服务器端也可以直接这样搞，或者本地搞定了直接rsync到服务器上去也行，又或者直接github上建一个git仓库，本地搞定了推到github，服务器端pull github上的代码就可以了。

Hexo进程守护

Node进程守护有很多工具，Forever，PM2，PM2.5 blah blah.解决的问题也是很容易讲清楚，比如：ssh登陆服务器，启动node服务，然后ssh断开连接，服务中断，网站无法访问。这里讲一下用forever 解决 Hexo 进程守护的问题，安装Forever:

$ [sudo] npm install forever -g
$ cd /path/to/your/project
$ [sudo] npm install forever-monitor
Hexo下新建一个app.js,写入下面代码：

var spawn = require('child_process').spawn;
free = spawn('hexo', ['server', '-p 4000']);/* 其实就是等于执行hexo server -p 4000*/

free.stdout.on('data', function (data) {
console.log('standard output:\n' + data);
});

free.stderr.on('data', function (data) {
console.log('standard error output:\n' + data);
});

free.on('exit', function (code, signal) {
console.log('child process eixt ,exit:' + code);
});


其实思路也很简单，大致意思就是node启动一个子进程，用forever 守护 hexo sever -p 4000这条命令（4000代表端口），关于node的child_process的相关知识，请自行baidu、google,或者去查nodejs的文档。
执行forever命令：

$ forever --minUptime 10000 --spinSleepTime 26000 start app.js
至于后面这几个minUptime、spinSleepTime可填可不填，不填默认也会有，参数的意思可以直接去forever上查询。

停止服务

这里值得注意的是你拿forever启动的服务，通过forever stopall是根本停不掉的，因为其实你执行的是hexo sever，可以通过下面的办法：

$ lsof -i:[port]
$ ps aux|grep hexo
$ kill pid(进程的id)
完...


---
第一步 nodejs
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | sh
wget -qO- https://raw.githubusercontent.com/creationix/nvm/master/install.sh | sh
nvm install stable

---

---
第二步 淘宝源
npm install cnpm -g --registry=https://registry.npm.taobao.org

---

第三步 hexo

cnpm install -g hexo-cli

安装 yelee 主题
git clone https://github.com/MOxFIVE/hexo-theme-yelee.git themes/yelee
---

第四步 shadowsocks
启动  
ssserver -p 8388 -k passwordh -m rc4-md5  -d start  
p：服务器端口  
k：认证密码  
m：加密方式  

安装  
apt-get install python-pip python-m2crypto
apt-get install -y python-setuptools
pip install --upgrade pip
pip install shadowsocks

卸载
pip uninstall shadowsocks
---

第五步 forever

cnpm install forever -g
---
// windows 安装 yarn 的方式
// https://yarnpkg.com/zh-Hans/docs/install#windows-tab
// 直接下载安装包, 双击之后下一步就可以安装

// 更改 yarn 的镜像源
yarn config set registry https://registry.npm.taobao.org


// 添加 package
// 对应 cnpm install koa
yarn add koa

// 指定版本
// 如果安装的时候 package 已经存在，只是版本不同，则会直接覆盖
yarn add koa@2

// 指定依赖类型，默认是安装到 dependencies
yarn add koa@2 --dev


// 移除 package, 不需要指定版本号
// 对应 cnpm uninstall
yarn remove koa


// 安装所有依赖
// 对应 cnpm install
// 只输入 yarn 也可以，不过不应该省略
yarn install
