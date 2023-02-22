#### 区分不同的appid
   1. 这个很重要，安卓区分app是通过这个来判断的，就算名字不一样也是一样会默认覆盖，会导致无法生产和开发环境无法安装的问题
   2. 配置
      1. 打开android\app\build.gradle，在 buildTypes -> debug，增加 ```applicationIdSuffix ".debug"```
      2. ***注意： 运行的时候记得加上参数 react-native run-android --appIdSuffix debug
  上面参数的debug对应的是buildTypes的key***

#### 区分不同的app名称
  1. 安装npm包`react-native-config`，自行看官方文档配置
  2. 书写.env文件
   ```
   例如：
   APP_NAME=APP_NAME_PROD
   ```
   3. 编辑`main\res\values\strings.xml`
   ```xml
    <string name="app_name">@string/APP_NAME</string>
    注意： 这个APP_NAME对应的就是env文件定义的
   ```
  4. 运行时使用不同的env文件，参考：
   ```
  "adb:dev": "cross-env ENVFILE=.env.development react-native run-android --appIdSuffix debug"
  
  "adb:prod": "cd android && cross-env ENVFILE=.env.prod ./gradlew assembleRelease"

   ```