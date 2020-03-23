### Mac os 10.15 安装 iOSOpenDev

### 1.安装包管理器MacPorts
Mac上的包管理工具，类似HomeBrew的，后续使用它安装一些工具
第一种方式：通过[官网下载](https://distfiles.macports.org/MacPorts/MacPorts-2.6.2-10.15-Catalina.pkg)安装包进行安装，但是有时候会卡在安装的最后，建议使用第二种方法
![截屏2020-03-23下午11.44.09.png](https://static.objc.com/2020/3/UKtTJs6QWaEHBMBTyBxBdrXfyNtDWne0ZCOklQk8tuHhqsnbytjFTR6AzgeBwTxI "截屏2020-03-23下午11.44.09.png")
第二种方式：自己编译，通过终端执行：
```
# Download
cd /tmp
sudo curl -O https://distfiles.macports.org/MacPorts/MacPorts-2.5.4.tar.bz2
sudo tar xf MacPorts-2.5.4.tar.bz2

# Build
cd MacPorts-2.5.4/
./configure --prefix=/opt/macports-2.5.4   && echo "[ OK ]"
make   && echo "[ OK ]"
sudo make install   && echo "[ OK ]"

# Export Path or Create symlink
echo "export PATH=/opt/local/bin:/opt/local/sbin:$PATH" >> ~/.bash_profile
# or
ln -s /opt/local/bin/port /usr/local/bin/port
# 更新，如果不需要更新，此步骤可省略：
sudo port selfupdate
# 安装ffmpeg：
sudo port install ffmpeg
```

### 2.安装DPKG文件
按照DPKG用于打包.deb文件
在终端使用MacPorts安装：
```
sudo port -f install dpkg
```

### 3.安装those工具
打开终端，配置theos的环境变量，官方默认是/opt/theos
```
export THEOS=/opt/theos
```
下载兼容iosopendev的版本
```
git clone -b stableversion https://github.com/haorenqq/theos/ $THEOS
```

### 4.设置Specifications文件夹
[下载地址](https://github.com/tuxi/iOSOpenDevSpecifications)
iPhoneOS开头的四个文件放到/应用程序/Xcode/Content/Developer/Platforms/IphoneOS.platform/Developer/Library/Xcode/Specifications文件夹下（如果没有，请自己创建一个），

iPhone Simulator 开头的另外四个文件放入/应用程序/Xcode/Content/Developer/Platforms/iPhoneSimulator.platform/Developer/Library/Xcode/Specifications文件夹下(如果没有，请同样创建一个)。

另外在/应用程序/Xcode/Content/Developer/Platforms/iPhoneSimulator.platform/Developer/文件夹下创建usr文件夹，usr文件夹下再创建一个名为bin的文件夹

### 5.安装iOSOpenDev
[官方下载](http://iosopendev.com/download/)
下载完成的是.pkg文件，直接双击安装即可。
如果安装失败了？请继续以下步骤！
![截屏2020-03-24上午12.58.32.png](https://static.objc.com/2020/3/qpaNVykTZKqKcpw2c2mFqZUfpGry1avpbcKuJRzh7u7BwuPZHymu3gxlRkyzGrRy "截屏2020-03-24上午12.58.32.png")

安装失败后，我们进入系统根目录的opt文件夹，会发现已经有了iosopendevsetup文件夹，我们在iosopendevsetup/bin看到有一个脚本iod-setup。

终端运行iosopendevsetup/bin/iod-setup
```
sudo ./iod-setup base
```

指定最新xcode sdk：
```
sudo ./iod-setup sdk -sdk iphoneos
```

大功告成。启动xcode，新建工程，就可以看到iOSOpenDev了。
![截屏2020-03-24上午12.47.09.png](https://static.objc.com/2020/3/T2y2ZIrpu3MxDywN3TUPgyz3bYbeKLR6okEWmn4HiAo2KEzoGzFFTaxQJq6cOb5K "截屏2020-03-24上午12.47.09.png")

参考资料：https://www.ianisme.com/ios/2319.html
