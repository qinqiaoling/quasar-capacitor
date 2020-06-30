# Quasar App (capacitordemo)

A Quasar Framework app

## Install the dependencies
```bash
yarn
```

### Start the app in development mode (hot-code reloading, error reporting, etc.)
```bash
quasar dev
```


### Build the app for production
```bash
quasar build
```
### 移除某一个quasar模块
```bash
quasar mode remove capacitor
```
### 添加某一个quasar模块
```bash
quasar mode add capacitor
```

### Customize the configuration
See [Configuring quasar.conf.js](https://quasar.dev/quasar-cli/quasar-conf-js).

### qusar [capacitor文件配置说明](https://segmentfault.com/a/1190000013755356)
    1.capacitor命令编译打包apk
	    注意：使用quasar框架打包quasar build -m capacitor -T [android|ios]
		会在src-capacitor\android\app\build\outputs\apk\release目录下生成一个app-release-unsigned.apk，这就完成了一个简单的打包，但是，上面生成的是一个测试的apk，没有任何签名信息，不能上架到各大应用平台，下面来讲一下打包一个有签名的apk。
		apk签名：
			1.第一步
				quasar build -m capacitor -T [android|ios]
				会在src-capacitor\android\app\build\outputs\apk\release目录下生成一个app-release-unsigned.apk。
			2.第二部
				在src-capacitor目录打开cmd命令运行命令keytool -genkeypair -alias name.keystore -keyalg RSA -validity 4000 -keystore name.keystore
				执行以上命令后，会要求填写密码口令，单位信息等等，这里需要记住录入的密码，因为最后编译apk的时候还需要用到，在所有的选项都录入完后，按回车，会在项目的根目录下生成一个name.keystore的签名文件，里面就包含刚刚录入的一些信息。
				会在根目录下生成一个name.keystore,这是apk独有的签名证书,如下图(命令中的name.keystore中的name是签名文件的名字，这里可以任意取名，我习惯用name.keystore)
			3.第三部
				将src-capacitor目录下生成一个android-release-unsigned.apk重命名为name_unsigned.apk(我为了与name.keystore对应)，并将它和根目录下的name.keystore放在同一目录下
			4.第四部
				在src-capacitor这个文件夹下，运行命令jarsigner -verbose -keystore name.keystore -signedjar name.apk name_unsigned.apk name.keystore,输入之前签名的录入的密码(我自己测试输入密钥口令123456)，经过编译，会生成最后的签名版本 name.apk.
				jarsigner -verbose:签名命令标识符。
				-keystore:后面跟着的是你签名使用的密钥文件(keystore)的绝对路径。
				-signedjar:此后有三个参数：
				参数一:签名后生成的apk文件所要存放的路径。
				参数二:未签名的apk文件的存放路径。
				参数三:你的证书名称，通俗点说就是你keystore文件的别名

