# 准备事项
这是一篇前端页面指南, 不包含树莓派的初始配置. 那玩意我还没写. 

找到树莓派的 IP 本机地址. 通过 `ssh` 或者树莓派终端输入 `ifcon../fig` 可以容易地找到其地址
```
eth0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether dc:a6:32:f1:4c:1d  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 818491  bytes 165738595 (158.0 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 818491  bytes 165738595 (158.0 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.43.61  netmask 255.255.255.0  broadcast 192.168.43.255
        inet6 2408:8448:4401:35f4:70d1:1bc:3d5c:9354  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::b5c0:5824:dabe:3cbc  prefixlen 64  scopeid 0x20<link>
        ether dc:a6:32:f1:4c:1e  txqueuelen 1000  (Ethernet)
        RX packets 7160  bytes 550756 (537.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 11789  bytes 10105102 (9.6 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
如上面的输出, 得到内网地址为 `192.168.43.61`, 则在树莓派同一局域网环境下用任何现代浏览器 (如 Chrome, Edge, Firefox 或 Safari 浏览器) 访问 `http://192.168.43.61:8081` 即可登录到前端交互页面. 

![登陆页面](../fig/login.png)

点击登录即可登录到管理页面. 

# 地图
## 新建地图
若是首次使用该系统, 需要新建一张地图方便之后的演习调用

![新建地图](../fig/new_map.png)

新建地图需要以下信息

- **名称** 地图的名称
- **图片** 需要作为地图背景的图片; 只能上传 `jpg` 或者 `png` 格式的图片
- **左上角的纬度** 一个长方形的地图通过左上角的经纬度和右下角的经纬度便可以确定地图的位置
- **左上角的经度** 
- **右下角的纬度** 
- **右下角的经度** 
- **备注** 备注信息

## 管理地图
在此页面可以查看和删除已经设置好的地图

![管理地图](../fig/map_man.png)


# 演习
## 新建方案
新建演习需要以下信息

![新建演习](../fig/new_train_sch.png)

- **演习名称** 该演习方案的名称
- **演习地图** 该演习方案所使用的地图
- **演习地图** 该演习方案所使用的地图
- **红方人员** 该演习中红方人员的详细信息
  - **姓名** 该人员在演习系统中显示的姓名
  - **性别** 该人员在演习系统中显示的性别
  - **年龄** 该人员在演习系统中显示的年龄
  - **所属单位** 该人员在演习系统中显所属单位
  - **人员编号** 该人员在演习系统的人员编号, 范围为 0 到 65535, 必须与**设备固件中记录的人员编号**一致
  - **设备编号** 该人员在演习系统的设备编号, 格式为 64 bit EUI (Extended Unique Identifier), 必须与**设备固件中记录的设备编号**一致
- **蓝方人员** 该演习中蓝方人员的详细信息, 具体参照上方*红方人员*的说明
- **演习模式** 保留位, 目前无实际作用

## 方案管理
可以查看已经创建好的方案, 并且执行

- **开始演习** 开始一个未开始的演习, 将给所有终端节点发送演习开始信号, 并且跳转至*当前演习*页面
- **加载正在进行的演习** 若要在一个新的设备观看已经进行的演习, 或者在不小心关闭浏览器之后恢复对演习情况的观看, 则需要点击该按钮. 否则*当前演习*页面中的地图将不会加载
- **删除** 删除该演习方案

## 当前演习
在该页面中可以观察已经开始的演习

> 若地图加载不出来, 见[常见错误](#常见错误)

若出现「是否开始录屏」的提示, 根据自身需求选择即可

> 若没有出现「是否开始录屏」的提示, 而是出现了「错误，请检查浏览器是否设置正确。录屏功能将被禁用」, 见[常见错误](#常见错误). 若不需要录屏则可以忽视该提示. 

![是否开始录屏](../fig/if_record.png)

若要截取整个屏幕, 请选择整个屏幕

![全屏录制](../fig/what_to_record.png)

若仅仅要求截取标签页内内容, 请选择 Chrome 标签页

![标签页录制](../fig/what_to_record_tab.png)

![当前演习界面](../fig/view.png)

点击**演习结束**可以查看战局的统计信息并且结束整个演习. 如果演习时间较长，上传视频需要一定时间，需要耐心等待. 

![演习结束](../fig/end_training.png)


## 演习回放
若开启了录屏功能, 则可以在此处看到演习的录屏回放和战局的统计信息. 

![演习回放](../fig/record_his.png)

# 常见错误

## 「当前演习」界面地图加载不出来
到*方案管理*页面点击**加载正在进行的演习**按钮重新加载即可

## 录屏功能将被禁用
若使用 Chrome 浏览器, 可以在地址栏输入`chrome://flags/#unsafely-treat-insecure-origin-as-secure`

![录屏设置](../fig/chrome_setting.png)

在其中输入[准备事项](#准备事项)中的地址, 允许 http 调用录屏 API. 

或者也可以换用其他浏览器如 Firefox. 