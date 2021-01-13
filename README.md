# 项目说明
本项目来自: https://github.com/wangziyingwen/AutoApiP

# AutoApiP
AutoApi系列：~~AutoApi~~、[AutoApiSecret](https://github.com/wangziyingwen/AutoApiSecret)、~~AutoApiSR~~、~~AutoApiS~~、[AutoApiP](https://github.com/wangziyingwen/AutoApiP)

## 置顶 ##
* **不保证续期**
* 设置了**周六日(UTC时间)不启动**自动调用,1-5每6小时自动启动一次，修改看教程

### 跳转
* AutoApiSecret：https://github.com/wangziyingwen/AutoApiSecret
* **常见错误及解决办法/更新日志**：https://github.com/wangziyingwen/Autoapi-test
* 视频教程：
   * B站：[BV185411n7Mq](https://www.bilibili.com/video/BV185411n7Mq/)

## 步骤 ##
* 准备工具：
   * E5开发者账号（非个人/私人账号）
   * rclone软件，[下载地址 rclone.org ](https://downloads.rclone.org/v1.53.3/rclone-v1.53.3-windows-amd64.zip)，(windows 64）
   * 教程图片看不到请科学上网
   
* 步骤大纲：
   * 微软方面的准备工作 （获取应用id、密码、密钥）
   * GIHTHUB方面的准备工作  （获取Github密钥、设置secret）
   * 调用API
   
#### 微软方面的准备工作 ####

* **第一步，注册应用，获取应用id、secret**

    * 1）点击打开[仪表板](https://aad.portal.azure.com/)，左边点击**所有服务**，找到**应用注册**，点击+**新注册**
    
    ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_01.png)
    
    * 2）填入名字，受支持账户类型前三任选，重定向填入 http://localhost:53682/ ，点击**注册**
    
    ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_02.png)
    
    * 3）复制应用程序（客户端）ID到记事本备用(**获得了应用程序ID**！)，点击左边管理的**证书和密码**，点击+**新客户端密码**，点击添加，复制新客户端密码的**值**保存（**获得了应用程序密码**！）
    
    ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_03.png)
    
    ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_04.png)
    
    * 4）点击左边管理的**API权限**，点击+**添加权限**，点击常用Microsoft API里的**Microsoft Graph**(就是那个蓝色水晶)，
    点击**委托的权限**，然后在下面的条例选中下列需要的权限，最后点击底部**添加权限**
    
    **赋予api权限的时候，选择以下几个（11项）**
  
          Calendars.ReadWrite、Contacts.ReadWrite、Directory.ReadWrite.All、
          Files.ReadWrite.All、MailboxSettings.ReadWrite、Mail.ReadWrite、
          Notes.ReadWrite.All、People.Read.All、Sites.ReadWrite.All、
          Tasks.ReadWrite、User.ReadWrite.All
    
    ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_05.png)
    
    ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_06.png)
     
    ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_07.png)
    
    * 5）添加完自动跳回到权限首页，点击**代表授予管理员同意**
    
    ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_08.png)
    
* **第二步，获取refresh_token(微软密钥)**

    * 1）解压下载好的ZIP压缩包，打开rclone.exe所在文件夹，鼠标移至空白处按住**shift**键，同时单击**鼠标右键**，弹出菜单中鼠标左键单击**在此处打开Powershell**，输入下面**修改后**的内容（或在记事本/便签中修改后全选复制，使用快捷键粘贴）：
           
          ./rclone authorize "onedrive" "应用程序(客户端)ID" "应用程序密码"
               
    * 2）按下**回车键**执行命令，会自动打开浏览器，**登入E5账号**，点击接受，成功后会显示“success!”，关闭浏览器回到Powershell窗口，会看到多了一串东西。
    * 3）在那一串东西里找到 **"refresh_token"："** ，从双引号开始选中到 **","expiry":2021** 为止（就是refresh_token后面双引号里那一串，**不要双引号**），如下图，**右键复制**保存（**获得了微软密钥**）
    
    ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_09.png)
    
 ____________________________________________________
 
 #### GITHUB方面的准备工作 ####

 * **第一步，fork[本项目](https://github.com/wangziyingwen/AutoApiP)**
 
     登陆/新建Github账号，回到本项目页面，点击右上角fork[本项目](https://github.com/wangziyingwen/AutoApiP)的代码到你自己的账号，然后你账号下会出现一个一模一样的项目，接下来的操作均在你的那个项目下进行。
     
     ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_10.png)
     
 * **第二步，新建Github密钥**
 
    * 1）进入你的个人设置页面 (**右上角头像** Settings，不是仓库里的 Settings)，选择 Developer settings -> Personal access tokens -> Generate new token

     ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_11.png)
    
     ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_12.png)
    
    * 2）设置名字为 **GH_TOKEN** , 然后**勾选repo**，点击 Generate token ，最后**复制保存**生成的Github密钥（**获得了Github密钥**，**只会显示一次**，一旦离开页面下次就看不到了！）
   
     ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_13.png)
  
 * **第三步，新建secret**
 
    * 1）依次点击**仓库页面上横栏**（靠右边）的 Setting -> 左竖栏 Secrets -> 右上角 New repository secret，新建4个secret： **GH_TOKEN、MS_TOKEN、CLIENT_ID、CLIENT_SECRET**  
   
     ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_14.png)
    
     ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_15.png)
    
     **(以下填入内容注意前后不要有空格空行)**
 
     GH_TOKEN
     ```shell
     Github密钥 (第三步获得)，例如获得的密钥是abc...xyz，则在secret页面直接粘贴进去，不用做任何修改，只需保证前后没有空格空行
     ```
     MS_TOKEN
     ```shell
     微软密钥（第二步获得的refresh_token）
     ```
     CLIENT_ID
     ```shell
     应用程序ID (第一步获得)
     ```
     CLIENT_SECRET
     ```shell
     应用程序密码 (第一步获得)
     ```
________________________________________________

#### 调用API ####
   
   * 1）点击两次右上角的星星（star）启动action,，再点击**仓库页面上横栏**的Action，选择 **Auto Api Pro** 就能看到每次的运行日志，看看运行状况

   （必需点进去Test Api看下，api有没有调用到位，有没有出错。外面的Auto Api打勾只能说明运行了（不代表成功调用），我们还需要确认api是否调用成功，就像图里的一样）
   
     ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_16.png)
     
   * 2）再点两次星星（star），如果还能成功运行就ok了（这一步是为了保证重新上传到secret的token是正确的）
 
### 教程完 ###

__________________________________________________________________________

## 额外设置 （看不懂请忽略）##
   * **定时启动修改**

   * **多账号/应用支持**
    
   * **超级参数设置**

#### 定时启动修改 ####
   
   我设定的周一至周六每天指定的几个时间自动运行一次（周日休息），每次调用5轮（点击右上角星星/star也可以立马调用一次），你们自行斟酌修改（我也不知道保持活跃要调用多少次、多久）：

  * 定时自动启动修改地方：在.github/workflow/autoapi.yml（只修改这一个）文件里，最短每5分钟一次。
   
   可使用[cron定时任务生成器](http://www.toolzl.com/tools/croncreate.html)生成一个，建议在线编辑autoapi.yml文件，注意不要删除引号，替换完成需要删减一些内容，鼠标移至该处会有时间提示，前后适当删减即可得到Github可正常识别使用的Cron定时文件内容，最后保存提交即可！
   
     ![image](https://tu.tusu.ml/image/github/E5AutoApiPro_17.png)
    
#### 多账号/应用支持 ####

   如果想输入第 2/N 账号或应用，请按上述先获取到第 2/N 个应用的 **应用程序ID**、**应用程序密码**、**微软密钥refresh_token** 三个值，再按以下步骤：
 
   * 1）**增加 secret** 。依次点击**仓库页面上横栏**（靠右边）的 Setting -> 左竖栏 Secrets -> 右上角 New repository secret，根据需要新建secret：
 
   APP_NUM
   ```shell
   账号/应用数量（现在例如是2，3个就是3，日后如果要增加请删掉后再新建APP_NUM）
   ```
   
   然后添加具体的账号/应用参数：（三个参数为一组，更改后面数字即可）
   
          	第2个账号：
          MS_TOKEN_2
          CLIENT_ID_2
          CLIENT_SECRET_2
          	第10个账号：
          MS_TOKEN_10
          CLIENT_ID_10
          CLIENT_SECRET_10
   
   * 2）修改.github/workflows/里的两个yml文件（**超过5个（>5）账号需要更改，5个及以下（≤5）直接忽略这一步**）
    
   yml文件根据注释看着改就行，已经写入5个账号模板了，跟着复制粘贴很简单的（没有找到比较好的自动方案）
  
#### 超级参数设置 ####
 
   runapi.py 文件第11行有个config_list，里面是以下参数配置
     
   · 轮数：
              
          就是一次运行要跑多少轮api，也就是启动一次会重复跑几圈
    
   · 是否启动随机时间（默认关闭）：
            
          这个是每一轮结束，要不要等一个随机时间再开始调用下一轮。后面两个参数就是生成随机时间的，例如设置600，1200，就会延时600-1200s之间。
    
   · 是否开启随机api顺序（默认开启）：
            
          不开启就是初版10个api，固定顺序。开启就是28个api抽12个随机排序。
    
   · 是否开启各api延时（默认关闭）：
            
          这个是每个api之间要不要开启延时。后面两参数参考“随机时间”
    
   · 是否开启各账号延时（默认关闭）：
   
          这个是每个账号/应用之间要不要开启延时。后面两参数参考“随机时间”
    
   （延时的设置是会延长运行时间的，全关闭大概每次运行1min，开启就会适当延长）
 
    
—————完—————

          wangziyingwen
        
—————完—————

# 注意
## 声明
   * 本项目来自: https://github.com/wangziyingwen/AutoApiP
   * 同AutoApi系列：~~AutoApi~~、[AutoApiSecret](https://github.com/wangziyingwen/AutoApiSecret)、~~AutoApiSR~~、~~AutoApiS~~、[AutoApiP](https://github.com/wangziyingwen/AutoApiP)

   * [Releases](https://github.com/Hovthen/E5AutoApiPro/releases)中为大佬两个版本备份，版本号为打包日期！

## 更多推荐
   * 1） [Outlook.api续订程序](https://e5.qyi.io/)
      * 同时您也可以使用[续订程序](https://e5.qyi.io/)，使用Github账号登录，填入一些必备参数成功运行后就不用管了。（~~不会真的有人看到这还不知道怎么获取参数吧？不会连Github账号都没有吧？~~）
   * 2） [OneIndex](https://github.com/TheZihanGu/oneindex-tzg)
      * 由于原作者删库，可以使用相关项目。我使用的是[oneindex-tzg](https://github.com/TheZihanGu/oneindex-tzg)
   * 3） [OneManager](https://github.com/qkqpttgf/OneManager-php)
      * 我使用的是[OneManager-PHP](https://github.com/qkqpttgf/OneManager-php)，配置说明非常详细。
   * 4） [Freenom](https://www.freenom.com/zh/index.html?lang=zh)
      * 你可能需要一个比较短的域名用作后缀，可以使用免费的tk、ml...等域名
      * 请勿使用任何上网工具，否则极易申请失败。申请前建议安装浏览器扩展[Gooreplacer](https://microsoftedge.microsoft.com/addons/detail/gooreplacer/cidbonnpjopamnhfjdgfcmjmlmehjnej)。
      
            www.google.com/recaptcha
            重定向到：
            recaptcha.net/recaptcha
      
   * 5） [DNSPod](https://console.dnspod.cn/)
      * 我还是更喜欢用腾讯的DNSPod来管理域名DNS，当然包括免费的tk、ml...
      * Freenom免费域名记录生效会特别慢，不必怀疑，等待1~5分钟即可。

如果有空，不妨多来[我的辣鸡网站](https://www.hovthen.com)转转。
Email：me@hovthen.com
