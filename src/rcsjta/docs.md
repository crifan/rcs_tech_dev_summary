# rcsjta资料

rcsjta有一些资料和文档

* 其中适合入手学习的是
  * Home · android-rcs/rcsjta Wiki
    * https://github.com/android-rcs/rcsjta/wiki
* 其中适合开发入手的是
  * rcsjta/DevEnv.md at wiki · android-rcs/rcsjta
    * https://github.com/android-rcs/rcsjta/blob/wiki/DevEnv.md

### RCS协议栈开通服务Provisioning

在能使用RCS服务之前，需要设置基本的参数，才能`开通服务`=`Provisioning`

可以参考：

rcsjta/Provisioning.md at wiki · android-rcs/rcsjta

https://github.com/android-rcs/rcsjta/blob/wiki/Provisioning.md

去搞清楚有哪些基本参数，以及分别设置好，才可以进行后续RCS功能演示。

#### 开通服务的模板

Provisioning templates · android-rcs/rcsjta Wiki

https://github.com/android-rcs/rcsjta/wiki/Provisioning-templates

相关协议标准：

* Albatros RCS 5.1 standard
* Blackbird RCS 5.2 standard

此处是手动的manual provisioning：

* Albatros template
  * template-ota_config-Albatros.xml
    * https://github.com/android-rcs/rcsjta/blob/tapi_0.9.0/data/provisioning_templates/albatros/template-ota_config-Albatros.xml
  * 参数
    * ConRef, Private_User_Identity, Public_user_identity_List, Home_network_domain_name, LBO_P-CSCF_Address, Public_user_identity, Realm, UserName, UserPwd, conf-fcty-uri, exploder-uri
* Blackbird template
  * template_config-Blackbird.xml
    * https://github.com/android-rcs/rcsjta/blob/tapi_0.9.0/data/provisioning_templates/blackbird/template_config-Blackbird.xml
  * 参数
    * ConRef, Private_User_Identity, Public_user_identity_List, Public_user_identity, Home_network_domain_name, LBO_P-CSCF_Address, Realm, UserName, UserPwd, ftHTTPCSURI, ftHTTPCSUser, ftHTTPCSPwd, conf-fcty-uri

### 测试RCS协议栈

如果想要测试RCS协议栈本身，可以参考

rcsjta/TestStack.md at wiki · android-rcs/rcsjta

https://github.com/android-rcs/rcsjta/blob/wiki/TestStack.md

需要：

* IMS平台
  * 选择：作者有 Telco平台，如果你没有，可以安装第三方IMS平台
    * 用kamailio作为P/I/S-CSCF
      * http://www.kamailio.org/
    * 用bind作为DNS服务器
    * 用FHoSS作为HSS
      * http://www.openimscore.org/docs/FHoSS/index.html
  * 如何设置搭建
    * Setup Kamailio IMS Servers (P-CSCF / I-CSCF / S-CSCF) | LM Tools
      * https://lmtools.com/node/76
    * tutorials:ims:installation-howto [Kamailio SIP Server Wiki]
      * http://www.kamailio.org/wiki/tutorials/ims/installation-howto
* AS=Application Server=应用程序服务器
  * 用于：
    * IM=Instant Message=即时消息 服务
      * 1对1消息
      * 组聊
      * 文件传输
  * 说明
    * 其他服务 不需要AS
      * Capabilities=能力？
      * 视频/图片/地理位置共享
      * MM 会话
  * 如何选择AS？
    * 目前没有开源的AS可用
      * 不过也可以测试1对1聊天和文件传输
        * 原设备设为 active mode=主动模式
        * 目的设备设为 passive mode=被动模式

### RCS一些实现细节

#### 部分核心功能实现代码

想要了解部分RCS核心功能的具体实现代码，可以参考

rcsjta/CodeSamples.md at wiki · android-rcs/rcsjta

https://github.com/android-rcs/rcsjta/blob/wiki/CodeSamples.md

其中给出了演示相关api如何使用的部分核心代码实现。

相关的几种典型的功能：

* 聊天=IM=Chat
* 文件传输=FT=File Transfer
* Video=视频
* Image=图片
* Geoloc=地理位置
* Extensions=扩展（功能）

### 兼容性测试

此处RCS功能实现方式和演示方式是基于Android的app的

而在Android中实现了RCS功能后，需要进行：兼容性测试

可以参考：

rcsjta/TestHarness.md at wiki · android-rcs/rcsjta

https://github.com/android-rcs/rcsjta/blob/wiki/TestHarness.md

去操作。

此处的自动化测试套件允许：

* 验证API签名
  * 检测一个设备，是否兼容对应的API（签名）
    * 目前有几种
      * Albatros
      * Blackbird
      * Crane
  * 从贴图的细节看，的确好像是：测试API是否兼容 如果不兼容，会失败，无法通过测试
    * API参考定义 都放在xml中：res/xml/
      * 从别处拷贝的：rcsjta/doclava/reference/current.xml
* 验证内容提供者content providers
  * 验证可操作性（读/写）、多列？等

> 注：
>
> [兼容性测试套件  |  Android 开源项目  |  Android Open Source Project](https://source.android.com/compatibility/cts)
>
> 兼容性测试套件 (CTS) 是一个免费的商业级测试套件，可在此处下载。CTS 代表兼容性的“机制”

### 扩展

官网文档

rcsjta/Extensions.md at wiki · android-rcs/rcsjta

https://github.com/android-rcs/rcsjta/blob/wiki/Extensions.md

介绍了：

* extension=扩展
  * 起源
    * 此开源项目最开始就引入了extension扩展机制，支持部署新的RCS/IMS服务
  * 现状
    * 目前已被GSMA采用放入RCS 5.2中
      * 详见
        * specification中的RCS Extensibility部分
  * 此处
    * Capability API：声明有哪些扩展
    * Multimedia Session API：实现扩展的功能

### 安全模型

rcsjta/SecurityModel.md at wiki · android-rcs/rcsjta

https://github.com/android-rcs/rcsjta/blob/wiki/SecurityModel.md

除了本身安卓的sign外，还会有tag的sign等过程，包括安装期间和使用期间，都会有权限校验的。

用于校验的工具：

* PorteCle
  * http://portecle.sourceforge.net
    * Portecle is a user friendly GUI application for creating, managing and examining keystores, keys, certificates, certificate requests, certificate revocation lists and more.
* keytool
  * android JDK中的工具
* iaritool
  * RCS的工具
  * 源码位置：rcsjta/tools/security/tag-auth-util
    * 最新源码：
      * 没有
        * ![rcsjta_src_no_iaritool](../../assets/img/rcsjta_src_no_iaritool.png)
      * 只有代码中有些iari相关代码
        * ![rcsjta_only_have_iari](../../assets/img/rcsjta_only_have_iari.png)
      * 算了，等用到再说。
        * 或许最新android studio中已无需此工具了

### 证书

Certificates · android-rcs/rcsjta Wiki

https://github.com/android-rcs/rcsjta/wiki/Certificates

* provisioning DM server
* File Transfer content servers of the OrangeLabs integration platforms

自己实现了https的校验证书后，需要安装到安卓设备中

* 1. Provisioning server
  * DM server certificate
    * https://github.com/android-rcs/rcsjta/blob/tapi_0.9.0/data/certificates/provisioning/dmserver_ofr.cer
* 2. File Transfer content servers
  * NSN 7.2 + RCS8
    * https://github.com/android-rcs/rcsjta/blob/tapi_0.9.0/data/certificates/filetransfer/Cert_RCS8_NSN_7_2.crt
  * NSN 9.2 + RCS14
    * https://github.com/android-rcs/rcsjta/blob/tapi_0.9.0/data/certificates/filetransfer/CertRCS14NSN92.crt

> 注意：
> 
>虽然这几个文件都是存在的。不过注意到了是旧的tag：0.9.0
>
> 最新版中，没有data目录了，这几个文件都不存在了

