### AUSU_FX505GT_EFI



###### 基本配置：

​		CPU：Intel i7-9750H (12) @ 2.60GHz  
​		GPU：Intel UHD Graphics 630  
​		GPU：Nvidia GeForce GTX 1650 (无法驱动，已屏蔽)  
​		主板：FX505GT_FX95GT (HM370芯片组)  
​		声卡：Realtek HDA 235  
​		网卡：Intel Wireless-AC 



###### OpenCore引导

​        OpenCore版本0.5.9，最高支持到Catalina 10.15.7，功能接近完美
​        功能使用正常：

   - ​    Fn + f1 - f3   声音调节
   - ​    Fn + f6 - f8  调节亮度
   -    关闭触摸板 Fn + 10 正常  ，键盘右上角开关机键下面的 PrtSc Sys Rq 键 可开关触控板
   -    Pause Break 只能 + 亮度，不能 - 亮度
   -    键盘灯按 Fn + 上下 无法使用，但是可以在睡眠模式下，根据键盘呼吸灯，来快速启动电脑，就
           可以达到关闭和打开键盘灯，有大神知道怎么控制键盘灯的也可以提出来
   -   已加载原生电源管理，显示正常
   -   触控板所有手势正常
   -   USBPorts.kext 定制USB驱动正常，如果不正常，可以百度定制，我这只是分享

---

### mac安装教程

图文教程(https://apple.sqlsec.com )，或者b站搜索飞行堡垒的安装视频，基本可安装上，下文是B站方法

---

ASUS_FX505_I7-9750H电脑BIOS设置
​        1、Logo 下按 F2
​        2、F7 进入
​        3、Boot  修改启动顺序
​        4、 Security   =>  Secure Boot =>    Secure Boot control => disabled
​        5、F10 保存

制作过程

​    1、下载镜像10.15.7（百度网盘）

​    2、写入镜像

​              1、TransMac   右键  =>  2修改  =>   右键 =>3 选镜像   =>  漫长等待写完

​              2、 balenaEthcher ,自行度程 (https://www.balena.io/etcher/)

​     3、DiskGenius 
​               1、建立一个>80 给mac存放系统（120G）

​               2、建立ESP分区 默认

​               3、硬盘需要修改成基本GPT => 磁盘 => 转换分区表类型为MBR格式，如果有标志位GPT则不需要
​      4、电脑 => 管理 => 磁盘管理 => 120GB未分配右键新建 =>看到 不要格式化这个卷 后勾选  =>  否

​      5、EFI 放入 ESP

​      6、开机 看见Logo ，按下 ESC  

​      7、选安装系统

​      8、进入磁盘工具 => 左上角选择显示所有设备

​      9、抹掉你刚才分区的磁盘 disk0S4，变成mac专用磁盘

​      10、名称随便，格式选APFS，然后抹掉，然后左上角退出磁盘，选择磁盘=>安装系统

​      11、等待过程中有重启，需要重新选择，选新增的安装选项，然后会继续安装

​      12、进入系统前的设置准备
​            1、中国大陆
​            2、语言与输入法默认
​            3、互联网，不接入互联网，三次继续
​            4、不传输
​            5、条款同意
​            6、创建名称
​            7、继续
​            8、siri 以后
​            9、外观随意
​            10、键盘按提示

​        11、EFI 放入

结束安装

---

优化：

​         1、开启任何来源： 终端 => 输入 sudo spctl --master-disable  (百度开任何来源) => 输入密码 => 回车
​                // 注意： 如果在系统偏好设置里面没有看到 任何来源 选项，则检查命令是否正确

​         2、wifi  =>  安装 HeliPort.dmg ，github 上有最新的

​         3、开机声音 OCC  打开  misc-其他  =>  关闭开始声音辅助 （EFI有设置好的就不需要关闭）

​         4、关闭跑代码         

​               1、OCC配置器 打开 config.plist 
​               2、NVRAM-随机访问器设置 
​               3、7C436110-.... 
​               4、 boot-args 的值，双击去掉  -v 参数 
​               5、保存

​          5、三码（百度）

​          6、HeliPort.dmg 设置为开机自启
​                  系统偏好设置 =>  用户与群组 => 登录项 => 下面 + 号添加HeliPort程序即可

​              8、登录Apple ID

​          8、搜狗输入法

​          9、安装西部数码盘里的NTFS for Mac ，解决移动硬盘只读不写

​          10、右上角访达 => 偏好设置 =>  通用 => 勾选所有 => 开启新.. => 自定义选择 => 边栏等自定义
​                       选择 =>高级搜索选当前文件夹，如果要全局搜可以用聚焦搜索

​          11、访达 => 显示 => 点选显示路径栏和显示状态栏

​               13、安装cmd + 鼠标，可以拖动导航栏的图标位置

​          13、鼠标触控板优化设置
​                  1、系统偏好设置 => 鼠标 => 滚动方向 => 取消勾选

​                  2、系统偏好设置 => 触控板 => 所有选项勾选 => 然后到辅助功能中 => 指针控制 => 触控板
​                        选项 =>三指拖移

​           14、键盘灯光调节 =>   睡眠下会采用呼吸灯，在暗下的时候回车，就可以关闭，反之就是打开，
​                    win下的快捷键调节不起作用，影响不大

​            15、系统偏好设置 =>  通用 => 外观自定义设置

​            16、系统偏好设置 =>  通用 => 默认浏览器选择

​            17、系统偏好设置 =>  程旭坞 => 可以自定义调节

​            18、系统偏好设置 =>  键盘 => 修饰键 => 更改键盘映射  => option 和 cmd互换             

​            19、黑苹果安装PS等其他软件

​            21、开启任何来源代码

​            2打开终端移除quarantine属性代码：sudo xattr -r -d com.apple.quarantine
​       （终端输入上面代码完最后面要加空格然后把dmg文件移到终端产生路径，输入密码后回车就可以了）   

​            23、软件安装

​                          1、网抑云音乐

​                          2、搜狗输入法

​                          3、ProperTree

​                          1、Hackintool   

​                          1、MaclASL

详解如下：安装命令行（Command Line Tools）

​                              打开终端，输入命令：xcode-select --install

​                           6、超级右键 
​                                  更新后=>设置=> 拓展=> 访达扩展勾选

​                          4、百度网盘

​                          8、screenFlow  录屏

​                          3、keka    压缩

​                          10、typora  MadrDown 文档

​                          11、Arctime 字幕

​                          12、intel Power Gadget

​                          13、mounitor control 声音调节  

​                          15、Motrix 下载工具

​                          16、小丸压制                                                          

​                          12、Google  /  Edge   /  Fixfor          

​                          18、向日葵 /  Teamviewer  / TeDesk

​                          13、讯飞听见字幕

​                          20、vscode   

​                           15、Micorsoft office
​                                    下载 => 双击打开 => 双击安装 =>   安装完成 点激活 =>                    

​                          22、lr  pr  ai ps pe au me      fxcp                

​                          23、IINA                      播放器

​                          24、record it

​                          25、snipaste

​                          26、 downie  4

​                          27、cheatsheet         

​                          28、sketch

​                          23、Permute3          格式转换

​                          24、ichm 阅读器         

​                          31、CleanMyMac       /        柠檬       

​                          32、App Cleaner & Uninstaller Pro  深度清理

​              删除软件
​                          1、如果是App store下载的软件，  直接在启动台，长按想要删除的软件，出现X 点击即可
​                          2、其他软件，打开访达 ，拖拽或者直接右键 移到废纸篓
​                          3、Clean my Mac X

