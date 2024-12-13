#                  配置Plist文件实现在线安装IPA详细教程

**教程简介：**

1、利用 itms-services 和 plist 文件，在线下载安装 ipa 文件。

1. itms-services

itms-services 是苹果为iOS企业用户提供的无线分发安装方式所使用的协议协议，使用这种方式发布应用不需要通过App Store或者 iTunes的情况下将APP直接通过下载链接给用户下载安装。

2. plist

   ```plist
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
   <plist version="1.0">
   <dict>
      <key>items</key>
      <array>
          <dict>
              <key>assets</key>
              <array>
                  <dict>
                      <key>kind</key>
                      <string>software-package</string>
                      <key>url</key>
                      <string>https://下载的域名/下载的ipa.ipa</string>
                  </dict> 
              </array>
              <key>metadata</key>
              <dict>
                  <key>bundle-identifier</key>
                  <string>（app唯一识别标志，不同会被识别为不同app）</string>
                  <key>bundle-version</key>
                  <string>0.0.0.1（替换为版本号）</string>
                  <key>kind</key>
                  <string>software</string>
                  <key>subtitle</key>
                  <string>应用名称</string>
                  <key>title</key>
                  <string>应用名称</string>
              </dict>
          </dict>
      </array>
   </dict>
   </plist>
   
   ```

   

2、直接跳转【设置-通用-描述文件】，信任证书。



首先需要**特别注意**：

1、ipa 的下载地址放到 plist 的文件中，链接指定 plist（格式见下文）

2、plist 的**链接必须是 https** （SSL加密）的，而且**必须是公网**，自签名及免费的 https 不可用。

3、链接格式要求一定是符合苹果规范的，`itms-services://?action=download-manifest&url=https://****/***.plist`



#### 下载安装ipa：

1、使用该地址链接格式为 `https://xxxx/用户名/项目名/master/xxxx.plist`

2、提示“**https://xxxx**”要安装“**XXXXX**”，点击安装即可在线下载安装 ipa 。

1. html网页链接或者二维码

实现在线下载ipa方法其实很简单.首先需要一个html网页，Safari 浏览器访问然后点击链接下载。iOS7之后，plist的链接必须是https的，ipa的链接可以是https/http均可，网页html里面，链接 a 标签，按如下所示即可：

```html
<a href="itms-services://?action=download-manifest&url=https://xxx.com/app.plist" id="text">安装 app</a>  
```



