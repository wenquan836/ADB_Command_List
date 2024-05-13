
#ADB命令大全
<br/>
<br/>
# 11 列出当前连接的Android设备信息<br/>
adb devices # 获取当前连接的Android设备<br/>
adb -s <device_serial_number> shell #连接某个特定的Android设备<br/>
adb shell getprop  # 查看android设备的参数信息<br/>
adb shell cat /proc/cpuinfo # 查看CPU架构信息<br/>
adb shell getprop ro.build.version.release # 查看系统Android版本信息<br/>
adb shell getprop ro.build.version.sdk # 查看系统API版本信息<br/>
adb shell df # 获取手机磁盘空间<br/>
adb shell dumpsys procstats # 获取当前内存使用信息<br/>
adb shell dumpsys gfxinfo # 获取当前的制图状态<br/>
<br/>
# 12 获取设备root权限，修改设备磁盘权限<br/>
adb root # 获取root权限<br/>
adb remount # 挂载系统文件系统为可读写状态，显示**remount succeeded**就代表命令执行成功；<br/>
<br/>
#21 安装apk文件<br/>
adb install <软件名> # 这个命令将指定的apk文件安装到设备上<br/>
adb install -r <软件名> # 替换已存在的应用程序，也就是说强制安装<br/>
adb install -l <软件名> # 锁定该应用程序<br/>
adb install -t <软件名> # 允许测试包<br/>
adb install -s <软件名> # 把应用程序安装到sd卡上<br/>
adb install -d <软件名> # 允许进行将见状，也就是安装的比手机上带的版本低<br/>
adb install -g <软件名> # 为应用程序授予所有运行时的权限<br/>
<br/>
# 22 获取安装的应用包名信息<br/>
adb shell pm list package # 列出所有的应用的包名<br/>
adb shell pm list package -s # 列出系统应用<br/>
adb shell pm list package -3 # 列出第三方应用<br/>
adb shell pm list package -f # 列出项目包名及对应的apk名及存放位置<br/>
adb shell pm list package -i # 列出应用包名及其安装来源<br/>
adb shell pm path com.ztf.coaster # 列出对应包名的apk位置<br/>
adb shell pm dump com.ztf.coaster # 列出应用的转储信息<br/>
<br/>
#23 卸载apk文件<br/>
adb uninstall <软件名> # 卸载软件<br/>
adb uninstall -k <软件名> # 卸载软件 但是保留配置和缓存文件<br/>
adb shell pm uninstall --user 0  包名 # 如果adb uninstall没有用，可以使用这个，表示删除用户空间0的应用。这跟卸载普通应用是同个方式<br/>
<br/>
<br/>
# 31 进程操作<br/>
 adb shell ps -A //显示当前正在运行的所有进程信息<br/>
 adb shell ps -A   | grep ** # 使用正则进行过滤<br/>
 adb shell kill 进程号 //结束某个进程<br/>
adb shell am force-stop 包名 //结束包名对应的进程，Android10以后的版本才可以<br/>

# 32 dumpsys 获取系统各个服务的信息<br/>
adb shell dumpsys activity //获取当前Activity的所有栈信息<br/>
adb shell dumpsys activity | grep ResumedActivity: #获取显示当前正在显示的Activity组件名称<br/>
adb shell  dumpsys activity activities //只获取当前Activity显示层级的栈信息<br/>

adb shell dumpsys window //获取当前窗口的所有栈信息<br/>
adb shell dumpsys window |grep mFocusedApp  //获取显示当前获取焦点的Window组件名称<br/>
adb shell dumpsys window windows //只获取当前窗口显示层级的栈信息<br/>

adb shell dumpsys package //获取系统中所有应用的包信息<br/>
adb shell dumpsys package 包名 //获取特定包名的包信息<br/>

# 33 Activity操作<br/>
adb shell am start 包名/.Activity (要启动的Activity) # 启动app<br/>
adb shell am start -W -n 包名/.Activity # 启动app<br/>
adb shell am start -a android.intent.action.MAIN -n --ei pid 10 --es str "helloworld"​​ # 传递key为pid数值为i整数类型0， 和key为str数值为字符串类型helloworld<br/>
adb shell am force-stop 包名 # 关闭app<br/>
adb shell pm clear 包名 #关闭app<br/>

# 34 服务操作<br/>
adb shell am startservice -n｛包(package)名｝/｛包名｝.{服务(service)名称}<br/>
adb shell am startservice -n com.android.traffic/com.android.traffic.maniservice<br/>
adb shell am start-foreground-service -n com.demo.screenrecorder/com.demo.screenrecorder.RecordService<br/>

# 35 广播操作<br/>
adb shell am broadcast -a android.intent.action.BOOT_COMPLETED # 发送系统启动完毕广播<br/>
adb shell am broadcast -a android.intent.action.MEDIA_MOUNTED # 发送外部SD卡挂载广播<br/>
adb shell am broadcast -a android.intent.action.MEDIA_UNMOUNTED # 发送外部SD卡拔出广播<br/>
adb shell am broadcast -a car.meter.share.BROADCAST # 自定义录制视频广播 <br/>
adb shell am broadcast -a com.leapmotor.share.reload.BROADCAST # 自定义途记分享广播<br/>

adb shell am broadcast -a com.android.test --es test_string "this is test string" --ei test_int 100 --ez test_boolean true<br/>
--es 表示使用字符串类型参数  --ei 表示int类型参数  --ez 表示boolean类型参数  第一个为key，第二个为value<br/>

<br/>
执行结果如下，则表示广播发送成功：<br/>
<br/>
Broadcasting: Intent { act=android.intent.action.BOOT_COMPLETED }<br/>
Broadcast completed: result=0<br/>
<br/>
# 41 获取设备屏幕分辨率<br/>
adb shell wm help # 可查看所有可用的wm指令<br/>
adb shell wm size # 获取当前分辨率<br/>
adb shell wm density # 获取当前像素密度(dpi)<br/>
adb shell wm size 720*1080 #将分辨率修改为720*1080<br/>
adb shell wm density 240 # 将dpi修改为240<br/>
adb shell wm size reset # 重置分辨率<br/>
<br/>
# 42 抓取日志信息<br/>
adb logcat # 打印android的系统日志，使用ctrl+c 可停止打印<br/>
adb shell "logcat >/sdcard/log000.log"  #把日志信息保存到sd卡根目录的log000.log目录<br/>
adb logcat | grep -E "^..MyApp\|^..MyActivity" # 使用 grep 配合正则表达式进行过滤，只显示需要的输出（白名单）<br/>
adb logcat | grep -vE "^..MyApp\|^..MyActivity" # 使用 grep 配合正则表达式进行过滤，过滤不需要的输出（黑名单）<br/>
adb logcat -c && adb logcat # logcat 有缓存，如果仅需要查看当前开始的 log，需要清空之前的缓存<br/>
cat myapp.log | grep -E "^..MyApp|^..MyActivity" > newmyapp.log # 例如 log 文件为 myapp.log，要匹配 tag 为 MyApp 和 MyActivity 的输出，然后输出到 newmyapp.log<br/>
<br/>
adb logcat <tag>[:priority] tag表示标签，priority输出的级别<br/>
V —— Verbose（最低，输出得最多）<br/>
D —— Debug<br/>
I —— Info<br/>
W —— Warning<br/>
E —— Error<br/>
F —— Fatal<br/>
S —— Silent（最高，啥也不输出）<br/>
<br/>
日志默认级别是V，如果错误日志我们选择E就可以。<br/>
//格式1：打印默认日志数据<br/>
adb logcat<br/>
//格式2：需要打印日志详细时间的简单数据<br/>
adb logcat -v time<br/>
//格式3：需要打印级别为Error的信息<br/>
adb logcat *:E<br/>
//格式4：需要打印时间和级别是Error的信息<br/>
adb logcat -v time *:E<br/>
//格式5：将日志保存到电脑固定的位置，比如D:\log.txt<br/>
adb logcat -v time >D:\log.txt<br/>
<br/>
<br/>
# 43 屏幕操作<br/>
adb shell screencap -p /sdcard/screen.jpg #对屏幕进行截屏<br/>
adb shell screenrecord sdcard/record.mp4 #对屏幕进行录像<br/>
<br/>
# 44 文件拷贝<br/>
adb push <本地路径> <远程路径> # 从电脑上发送文件到设备 【adb push media /sdcard/ 把media文件夹整个拷贝到sd卡根目录】<br/>
adb pull <远程路径> <本地路径> # 从设备下载文件到电脑 【adb pull /system/media D:/ 把设备中的media目录整个拷贝到D盘】<br/>
<br/>
# 45 获取设备中数据库字段信息<br/>
adb shell settings list global  #global数据库，所有用户共用<br/>
adb shell settings list settings #settings数据库，区分用户<br/>
<br/>
PM常用指令<br/>
pm即package manager，使用pm命令可以去模拟android行为或者查询设备上的应用信息等<br/>
<br/>
命令	功能	实现方法<br/>
dump	dump信息	AM.dumpPackageStateStatic<br/>
clear	清空App数据	AMS.clearApplicationUserData<br/>
uninstall [options]	卸载应用	IPackageInstaller.uninstall<br/>
force-dex-opt	dex优化	PMS.forceDexOpt<br/>
trim-caches <目标size>	紧缩cache目标大小	PMS.freeStorageAndNotify<br/>
list packages	列举app包信息	PMS.getInstalledPackages<br/>
get-install-location	获取安装位置	PMS.getInstallLocation<br/>
path	查看App路径	PMS.getPackageInfo<br/>
install [options]	安装应用	PMS.installPackageAsUser<br/>
hide	隐藏应用	PMS.setApplicationHiddenSettingAsUser<br/>
unhide	显示应用	PMS.setApplicationHiddenSettingAsUser<br/>
enable <包名或组件名>	激活包名或组件	PMS.setEnabledSetting<br/>
disable <包名或组件名>	禁用包名或组件	PMS.setEnabledSetting<br/>
set-install-location	设置安装位置	PMS.setInstallLocation<br/>
get-max-users	最大用户数	UserManager.getMaxSupportedUsers<br/>
<br/>
# 55 调试Android系统<br/>
adb shell setprop debug.layout true # 显示UI边界<br/>
adb shell setprop debug.hwui.overdraw show # 开启调试 GPU 过度绘制<br/>
adb shell setprop debug.hwui.overdraw false # 关闭调试 GPU 过度绘制<br/>
adb shell dumpsys package queryies # 查看设备中能直接访问的App<br/>
<br/>
# 61 查询数据库<br/>
msm8953_64:/data/system # sqlite3 locksettings.db  # 打开数据库，获取数据库版本信息<br/>
SQLite version 3.9.2 2017-07-21 07:45:23 # 数据库版本信息<br/>
Enter ".help" for usage hints.<br/>
sqlite> .tables # 显示所有的表信息<br/>
android_metadata  locksettings<br/>
.mode column #列对齐命令<br/>
.header on #打开表头显示<br/>
sqlite> select * from locksettings; # 查询整个表的信息<br/>
1|lockscreen.disabled|0|1<br/>
2|migrated|0|true<br/>
3|migrated_user_specific|0|true<br/>
4|lockscreen.password_type_alternate|0|0<br/>
5|migrated_biometric_weak|0|true<br/>
6|migrated_lockscreen_disabled|0|true<br/>
7|lockscreen.enabledtrustagents|0|<br/>
8|lockscreen.password_salt|0|-970902998671653081<br/>
9|lockscreen.password_type|0|262144<br/>
10|lockscreen.profilechallenge|0|1<br/>
11|lockscreen.passwordhistory|0|<br/>
sqlite><br/>
<br/>
<br/>
# 62 查看网络信息<br/>
adb shell ping -c 4 ww.baidu.com # 测试两个网络间的连接和延迟<br/>
adb shell netstat # 网络统计，用来查看网络当前状态。<br/>
tcpdump -p -vv -s 0 -w /data/data/capture.pcap # 网络抓包，将tcpdump文件push进设备（shell下）<br/>
tcpdump -i any -s 0 -w /data/data/capture.pcap # 网络抓包，将tcpdump文件push进设备（shell下）<br/>

# 100 监听手机事件<br/>
adb shell getevent<br/>
<br/>
<br/>
其中以003 0035和003 0036 开头的两条数据0x170和0x38E就是我们需要的x和y坐标了<br/>
<br/>
# 101 模拟点击<br/>
 模拟点击[x,y]坐标<br/>
adb shell input mouse tap x y<br/>
<br/>
# 102 模拟滑动和模拟长按<br/>
 从（x1，y1）滑动到（x2，y2）<br/>
adb shell input swipe x1 y1 x2 y2 <br/>
<br/>
<br/>
 因为没有专门模拟长按的动作，所以我们使用滑动来模拟长按<br/>
 滑动初始位置与结束位置一致，且时间设置为500毫秒<br/>
adb shell input swipe 300 300 300 300 500<br/>

# 103 模拟输入<br/>
 输入‘string’<br/>
adb shell input text 'string'<br/>
<br/>
注：需要先定位到对应的输入框，才可输入成功<br/>

# 104 模拟按键<br/>
 模拟back 按键<br/>
adb shell input keyevent  4<br/>
<br/>
这里给出一个常用的keyevent code:<br/>
<br/>
按键	按键Code码	描述<br/>
KEYCODE_UNKNOWN	0	<br/>
KEYCODE_SOFT_LEFT	1	<br/>
KEYCODE_SOFT_RIGHT	2	<br/>
KEYCODE_HOME	3	home键<br/>
KEYCODE_BACK	4	back键<br/>
KEYCODE_CALL	5	<br/>
KEYCODE_ENDCALL	6	<br/>
KEYCODE_0	7	<br/>
KEYCODE_1	8	<br/>
KEYCODE_2	9	<br/>
KEYCODE_3	10	<br/>
KEYCODE_4	11	<br/>
KEYCODE_5	12	<br/>
KEYCODE_6	13	<br/>
KEYCODE_7	14	<br/>
KEYCODE_8	15	<br/>
KEYCODE_9	16	<br/>
KEYCODE_STAR	17	<br/>
KEYCODE_POUND	18	<br/>
KEYCODE_DPAD_UP	19	<br/>
KEYCODE_DPAD_DOWN	20	<br/>
KEYCODE_DPAD_LEFT	21	<br/>
KEYCODE_DPAD_RIGHT	22	<br/>
KEYCODE_DPAD_CENTER	23	<br/>
KEYCODE_VOLUME_UP	24	<br/>
KEYCODE_VOLUME_DOWN	25	<br/>
KEYCODE_POWER	26	电源键<br/>
KEYCODE_CAMERA	27	<br/>
KEYCODE_CLEAR	28	<br/>
KEYCODE_A	29	<br/>
KEYCODE_B	30	<br/>
KEYCODE_C	31	<br/>
KEYCODE_D	32	<br/>
KEYCODE_E	33	<br/>
KEYCODE_F	34	<br/>
KEYCODE_G	35	<br/>
KEYCODE_H	36	<br/>
KEYCODE_I	37	<br/>
KEYCODE_J	38	<br/>
KEYCODE_K	39	<br/>
KEYCODE_L	40	<br/>
KEYCODE_M	41	<br/>
KEYCODE_N	42	<br/>
KEYCODE_O	43	<br/>
KEYCODE_P	44	<br/>
KEYCODE_Q	45	<br/>
KEYCODE_R	46	<br/>
KEYCODE_S	47	<br/>
KEYCODE_T	48	<br/>
KEYCODE_U	49	<br/>
KEYCODE_V	50	<br/>
KEYCODE_W	51	<br/>
KEYCODE_X	52	<br/>
KEYCODE_Y	53	<br/>
KEYCODE_Z	54	<br/>
KEYCODE_COMMA	55	<br/>
KEYCODE_PERIOD	56	<br/>
KEYCODE_ALT_LEFT	57	<br/>
KEYCODE_ALT_RIGHT	58	<br/>
KEYCODE_SHIFT_LEFT	59	<br/>
KEYCODE_SHIFT_RIGHT	60	<br/>
KEYCODE_TAB	61	<br/>
KEYCODE_SPACE	62	<br/>
KEYCODE_SYM	63	<br/>
KEYCODE_EXPLORER	64	<br/>
KEYCODE_ENVELOPE	65	<br/>
KEYCODE_ENTER	66	<br/>
KEYCODE_DEL	67	<br/>
KEYCODE_GRAVE	68	<br/>
KEYCODE_MINUS	69	<br/>
KEYCODE_EQUALS	70	<br/>
KEYCODE_LEFT_BRACKET	71	<br/>
KEYCODE_RIGHT_BRACKET	72	<br/>
KEYCODE_BACKSLASH	73	<br/>
KEYCODE_SEMICOLON	74	<br/>
KEYCODE_APOSTROPHE	75	<br/>
KEYCODE_SLASH	76	<br/>
KEYCODE_AT	77	<br/>
KEYCODE_NUM	78	<br/>
KEYCODE_HEADSETHOOK	79	<br/>
KEYCODE_FOCUS	80	Camera*focus<br/>
KEYCODE_PLUS	81	<br/>
KEYCODE_MENU	82	<br/>
KEYCODE_NOTIFICATION	83	<br/>
KEYCODE_SEARCH	84	<br/>
KEYCODE_MEDIA_PLAY_PAUSE	85	<br/>
KEYCODE_MEDIA_STOP	86	<br/>
KEYCODE_MEDIA_NEXT	87	<br/>
KEYCODE_MEDIA_PREVIOUS	88	<br/>
KEYCODE_MEDIA_REWIND	89	<br/>
KEYCODE_MEDIA_FAST_FORWARD	90	<br/>
KEYCODE_MUTE	91	<br/>
<br/>
# 105 adb shell input<br/>
Usage: input [<source>] <command> [<arg>...]<br/>
<br/>
The sources are:<br/>
      dpad<br/>
      keyboard<br/>
      mouse<br/>
      touchpad<br/>
      gamepad<br/>
      touchnavigation<br/>
      joystick<br/>
      touchscreen<br/>
      stylus<br/>
      trackball<br/>
<br/>
The commands and default sources are:<br/>
      text <string> (Default: touchscreen)<br/>
      keyevent [--longpress] <key code number or name> ... (Default: keyboard)<br/>
      tap <x> <y> (Default: touchscreen)<br/>
      swipe <x1> <y1> <x2> <y2> [duration(ms)] (Default: touchscreen)<br/>
      draganddrop <x1> <y1> <x2> <y2> [duration(ms)] (Default: touchscreen)<br/>
      press (Default: trackball)<br/>
      roll <dx> <dy> (Default: trackball)<br/>

