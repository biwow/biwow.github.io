# Node.js安装 
去Node.js官网 https://nodejs.org/en/download/ 下载系统对应版本。

> wget https://nodejs.org/dist/v8.11.3/node-v8.11.3-linux-x64.tar.xz //下载

> xz -d node-v8.11.3-linux-x64.tar.xz

> tar xvf node-v8.11.3-linux-x64.tar    //解包

> mv node-v8.11.3-linux-x64 /usr/local/nodejs   //放到应用目录

> vim /etc/profile  //把下面三行放到文件最底部保存
```
export NODE_HOME=/usr/local/nodejs  
export PATH=$PATH:$NODE_HOME/bin  
export NODE_PATH=$NODE_HOME/lib/node_modules
```
> source /etc/profile  //使配置生效

> node -v  //查看版本 安装完成

# remix安装 
```
git clone https://github.com/ethereum/remix-ide
cd remix-ide
npm install
npm run prepublish
npm start
```
访问 http://IP:8080 即可