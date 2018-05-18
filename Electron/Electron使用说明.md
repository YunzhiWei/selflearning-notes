##  <center> electron使用文档 </center>


#### 将electron集成进 react项目中
- 在项目目录下 

``` node
npm/yarn add electron --dev
```
- 安装结束后 在package.json中加入

``` json
{
    "scripts": {
            "electron-start": "electron ."
    }
} 
//用于启动ecltron项目
```

- 项目根目录下新建main.js,内容如下：


``` js

const { app, BrowserWindow } = require('electron');
//app负责管理Electron 应用程序的生命周期
//BrowserWindow类负责创建窗口

const url = require('url');
const path = require('path');

let mainWindow;

function createMainWindow(){

    mainWindow = new BrowserWindow({
        width:800,
        height:600,
    })
    
    
    //1. 根据网址加载页面
    mainWindow.loadURL("http://localhost:3001/")
    //2. 加载本地打包过的项目
    // mainWindow.loadURL(url.format({
    //     pathname:path.join(__dirname, './build/index.html'),
    //     protocol:'file:',
    //     slashes:true
    // }))

//是否开启调试 可设置开发环境变量进行判断
    mainWindow.webContents.openDevTools();

    mainWindow.on('closed',()=>{
        mainWindow = null;
    })
}

//app 
app.on('ready',() => {
    createMainWindow();
})

app.on('activate',function () {
    if (mainWindow === null){
        createMainWindow();
    }
})

```
- 在package.json中加入main入口：

``` json
{
    "main": "main.js"
}
```


- 运行程序

``` node
yarn build && yarn electron-start
```

**至此，一个简单的react和electron集成结束。**


#### electron打包

使用打包工具：
electron-packager,
electron-forge,
electron-builder（目前主要用的这个打包工具，因为可以配合自家的electron-updater来做自动更新，当然mac电脑还可以通过安装wine来打包win,[wine安装教程](https://www.davidbaumgold.com/tutorials/wine-mac/)）

- 安装

```js
yarn add electron-builder --dev
//这里需要注意要用 --save-dev，如果直接用--save， 打包会报错

```

- 配置package.json


-
<b>!!! TODO 目前非签名版本可以根据文末的build进行配置。后期追加签名版本配置
</b>
-

```js

//最好包含这几项 name, description, version and author
{
    "version": "1.0.0",
    "name":"myElectronApp",
    "description": "a electron with react",
    "author": "cajan",
    
    "build": {
       "appId": "your.id",
       "mac": {
            "target":[
                "dmg",
                "zip"
            ],
            "category": "",
            "type": "distribution",
            "identity": "",
            "provisioningProfile": "",
            "icon": "assets/icon/icon.icns",
            "publish": [{
                "provider": "generic",
                "url": "http://127.0.0.1:8081/dist/mac"
                      }] 
          },
       "win": {
         "publish": ["github", "bintray"]
       }
     },
     
    "scripts": {
       "pack": "electron-builder --dir",
       "dist": "electron-builder",
       "postinstall": "electron-builder install-app-deps"

     }
}



```

- package中关键字段解释

>appId:
一般类似于app开发中，iOS的bundle id 很热android中的包名

>target:
1.mac
default, dmg, mas, mas-dev, pkg, 7z, zip, tar.xz, tar.lz, tar.gz, tar.bz2, dir. 
默认为dmg和zip
2.win
nsis, nsis-web (Web installer), portable (portable app without installation), appx, msi, squirrel, 7z, zip, tar.xz, tar.lz, tar.gz, tar.bz2, dir. AppX package can be built only on Windows 10.
默认exe,

>category: 
应用类型 相关设置可以在 
[苹果官方文档中查看](https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/LaunchServicesKeys.html#//apple_ref/doc/uid/TP40009250-SW8)

>identity:
身份信息

>provisioningProfile:
签名证书文件/ absolute or relative to the app root.

>type:
"distribution" | "development"
 // Whether to sign app for development or for distribution.

>icon :
应用icon配置

>publish:
publish中的内容是 自动更新时用的,[相关配置](https://www.electron.build/configuration/publish)


更多的相关配置也可以看官方文档，[electron-builder](https://github.com/electron-userland/electron-builder)
To ensure your native dependencies are always matched electron versio

```json
"postinstall": "electron-builder install-app-deps"
//确保本地依赖总是matched electron版本
```

- 运行程序
yarn dist / npm run dist

--

##!!! TODO 
**mac和win证书相关配置还未涉及，后续添加相关配置**

--


#### 自动更新

- 安装
`npm install --save electron-updater`

- 使用
本例在main.js中操作

```js

const  { app, Menu, BrowserWindow, dialog} = require('electron');

const { autoUpdater } = require("electron-updater");


function sendStatusToWindow(text) {
    log.info(text);
    mainWindow.webContents.send('message', text);
}

// 监听 正在检查是否有新更新
autoUpdater.on('checking-for-update', () => {
    sendStatusToWindow('Checking for update...');
})

//设置是否自动下载更新文件
autoUpdater.autoDownload = false;

//监听有可用更新  可以弹窗提示用户有新版本需要更新，让用户自己选择是否需要更新

//弹窗给用户选择
autoUpdater.on('update-available', (ev, info) => {
    dialog.showMessageBox({
        type: 'info',
        title: '信息',
        message: "有新版本可供更新，是否更新?",
        buttons: ['是', '否']
    }, index => {
        if(index === 0) {
            autoUpdater.downloadUpdate();
        }
    });
});



//监听是无可用更新
autoUpdater.on('update-not-available', (ev, info) => {
    sendStatusToWindow('Update not available.');
})


//监听更新错误
autoUpdater.on('error', (ev, err) => {
    sendStatusToWindow('Error in auto-updater.');
})

//监听下载进度
autoUpdater.on('download-progress', (ev, progressObj) => {
    sendStatusToWindow('Download progress...');
})

//下载结束
autoUpdater.on('update-downloaded', (ev, info) => {
    // Wait 5 seconds, then quit and install
    // In your application, you don't need to wait 5 seconds.
    // You could call autoUpdater.quitAndInstall(); immediately

    sendStatusToWindow('Update downloaded; will install in 5 seconds');

    setTimeout(function() {
        autoUpdater.quitAndInstall();
    }, 5000)
})


app.on('ready',() => {

    createWindow();
    
    //也可以通过其他方式触发检查更新
    //setFeedURL 等同于package.json中设置的url
    autoUpdater.setFeedURL("http://127.0.0.1:8081/dist");
    autoUpdater.checkForUpdates();
        
})

```


> - 如果mac打包的没有签名，那么在自动更新的时候会报“ Could not get code signature for running application”错误。


win用builder打包的时候第一次可能会出现，
packing XXXXX 
and 1 more ，然后卡住。
这个时候需要做的是耐心等待，我的电脑是安装了n遍才安装成功。
这是因为win打包需要winCodeSign, nsis, nsis-resources这三个包，

如果等不急也可以[去找找](https://github.com/electron-userland/electron-builder-binaries/releases),
然后解压到本地相关目录，
例如：winCodeSign
/private/var/root/Library/Caches/electron-builder/winCodeSign（这个目录不同的电脑可能是不一样的）


- 打包成功后把打包的dist文件夹内的内容拷贝到升级目录下，然后再次打开electron app检查更新即可。 //更新的原理是对比 last_xx.yml/last_xx.json 中的版本号，然后下载同目录下的相应版本进行升级。




----

## electron在本项目中的相关配置

因为未涉及到签名问题，本项目中package.json   build的相关配置：

```json

//extends 设置为 null，否则在打包的时候可能会出现打包的时候xxx找不到的问题。可能是路径配置有问题。
//官方解释 extends: - The name of a built-in configuration preset or path to config file (relative to project dir). Currently, only react-cra is supported.

//If react-scripts in the app dependencies, react-cra will be set automatically. Set to null to disable automatic detection.


"build": {
    "extends": null,
    "publish": [
      {
        "provider": "generic",
        "url": "http://127.0.0.1:8081/dist"
      }
    ],
    "appId": "cn.notone.demo.electron",
    "mac": {
      "category": "your.app.category.type",
      "target": [
        "zip",
        "dmg"
      ]
    }
  },
  
  "dependencies": {
    "antd": "^3.5.0",
    "babel-plugin-import": "^1.7.0",
    "csvtojson": "^1.1.9",
    "electron-log": "^2.2.14",
    "electron-updater": "^2.21.10",
    "json2csv": "^4.1.2",
    "react": "^16.3.2",
    "react-app-rewired": "^1.5.2",
    "react-dom": "^16.3.2",
    "react-router-dom": "^4.2.2",
    "react-scripts": "1.1.4"
  },
  "scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test --env=jsdom",
    "eject": "react-app-rewired eject",
    "electron-start": "npm run build && electron .",
    "electron-build": "node_modules/.bin/build --win --mac --x64 --ia32",
    "dist": "electron-builder",
    "postinstall": "install-app-deps"
  },
  "devDependencies": {
    "electron": "^2.0.0",
    "electron-builder": "^20.11.1",
    "http-server": "^0.11.1"
  }

```



- 导入导出相关方法
新建electron-lib.js

```js

//需要安装依赖， 
// json转csv
//npm install json2csv --save  
// csv转json
// npm install csvtojson --save 

import {isEmpty} from "./Lib";

import { message } from 'antd';
const { remote } = window.require('electron');

const fs = remote.require('fs');
const path = require('path');
const Json2csvParser = require('json2csv').Parser;
const csv = require('csvtojson');


//保存json内容为csv文件 参数：保存路径、列名（需要更json的key对应）、要保存的json
export function writeCsvFormatFileWithPathAndData(filePath,fields,payload) {

    if(isEmpty(payload)||isEmpty(filePath)) return;
    const json2csvParser = new Json2csvParser({ fields });
    const csv = json2csvParser.parse(payload);

    fs.writeFile(filePath,csv,'utf8',(suc,err)=>{
    
        if (err) throw err;

        message.success('文件保存成功!');
    });
}

// 通过路径读取csv文件
export  function readCSVFileWithPath(filePath) {

    let filePromise = new Promise(function (resolve, reject) {

        fs.readFile(filePath, 'utf8', (err, data) => {
            if (err) reject (err);
            // console.log("readFile-",data);

            let jsonArr = [];
            csv({flatKeys:true})
                .fromString(data)
                .on('json',(jsonObj)=>{
                    
                    jsonArr.push(jsonObj);
                })
                .on('done',(err)=>{
                    
                    resolve (jsonArr);
                })
            ;
        });
    });

    return filePromise;
}


```

- 在saga中使用

```js

import { isElectron } from "../Lib";


//导出
export function* watchContentsExport() {


    yield takeEvery(contentsActios.CONTENT_EXPORT, function*({ payload }) {

        if (!isElectron()) return;
        
        //这里判断如果是electron环境才会引入electron-lib中的方法，如果直接在顶部引用，在网页上打开react项目，会报错 TypeError: window.require is not a function ；
        const writeCsvFormatFileWithPathAndData = require('../electron-lib').writeCsvFormatFileWithPathAndData;

        if (payload.length==0){

            notification.error({
                message:"请选择导出数据！",
                placement: 'topRight',
            });
            return;
        }
        console.log("watchContentsExport:",payload);
        // const fildes =['id','created_by','created_when','updated_by','name','type','description','_ex_info_.title','_ex_info_.content'];
        //保存的csv文件会根据fildes里面的字段为key来取json中对应的value
        const fildes =['path','name','type','_ex_info_'];
        writeCsvFormatFileWithPathAndData('./demo.csv',fildes,payload);
    })
}

export function* watchContentsInport(dispatch) {

    while(true) {

        const { payload } = yield take(contentsActios.CONTENT_INPORT);
        if (!isElectron()) return;
        const readCSVFileWithPath = require('../electron-lib').readCSVFileWithPath;
        const csvResult = yield readCSVFileWithPath(payload).then(function (result) {
            console.log("watchContentsInport-----:",result);
            return result;
        }).catch(function (err) {
            console.log("watchContentsInport-----:",err);
        })

        let handleArr = csvResult;
        if (csvResult.length>20){
            notification.info({message:"文件过大，只上传前20条"});
            handleArr = csvResult.splice(0,20);
        }

        yield put(contentsActios.create(handleArr));

    }

}
```


- lib.js中的 isElectron 方法

```js

//判断是否是 isElectron 环境
export function isElectron() {

    // Renderer process
    if (typeof window !== 'undefined' && typeof window.process === 'object' && window.process.type === 'renderer') {
        return true;
    }
// Main process
    if (typeof process !== 'undefined' && typeof process.versions === 'object' && !!process.versions.electron) {
        return true;
    }
// Detect the user agent when the `nodeIntegration` option is set to true
    if (typeof navigator === 'object' && typeof navigator.userAgent === 'string' && navigator.userAgent.indexOf('Electron') >= 0) {
        return true;
    }
}

```



-------
tips: 
>react项目build后，如果打开空白，在package.json中加上
``   "homepage":"./" ``




