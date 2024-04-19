# SCRIPTS BOOTLOADER FOR ASUS ROUTER 使用说明

[中文](./How_to_Use_zh-CN.md) | [English](./How_to_Use_en-US.md)

## 运行环境

- [Asuswrt](https://www.asus.com.cn)：官方华硕路由器固件
- [Asuswrt-Merlin](https://www.asuswrt-merlin.net/)：享誉全球的第三方华硕路由器固件

> 警告：除上述固件外，本系统不保证兼容其它固件

## 注意事项

1. 确保用于登录路由器Web页面的用户名和密码**仅含有***大小写字母、数字、下划线*

## 在线安装

> **提示信息说明**
>
> 1. 紫底白字：安装阶段提示信息
> 2. 绿底白字：安装成功提示信息
> 3. 红底白字：安装失败提示信息
>    - 出现安装失败提示信息时，其上一行会表明出错程序及错误详情

1. 准备一个空白U盘（不小于4GB；MBR），插入路由器USB接口

2. 用ssh登陆路由器后台

   ![](./Documents_Assets/How_to_Use/install/online_step2.jpg)

3. 执行下列代码

   ```shell
   cd /tmp && wget -q -O /tmp/install_online --no-check-certificate "https://cdn.jsdelivr.net/gh/JACK-THINK/SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER@latest/script_bootloader/bin/install_online" && chmod 777 /tmp/install_online && /tmp/install_online
   cd /tmp && wget -q -O /tmp/install_online --no-check-certificate "https://cdn.jsdelivr.net/gh/xlone2001/SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER@latest/script_bootloader/bin/install_online" && chmod 777 /tmp/install_online && /tmp/install_online
   ```

   ![](./Documents_Assets/How_to_Use/install/online_step3_zh-CN.jpg)

4. 阅读提示信息，确认无误后，输入`YES`继续安装

   ![](./Documents_Assets/How_to_Use/install/online_step4_zh-CN.jpg)

5. 安装过程开始

   - 重新分区并格式化U盘

     ![](./Documents_Assets/How_to_Use/install/online_step5-1.jpg)

   - 下载安装文件

     ![](./Documents_Assets/How_to_Use/install/online_step5-2.jpg)

   - 创建安装日志

     ![](./Documents_Assets/How_to_Use/install/online_step5-3.jpg)

   - **阶段一**：设置启动参数

     ![](./Documents_Assets/How_to_Use/install/online_step5-4.jpg)

   - **阶段二**：安装系统必备程序

     - 输入并确认虚拟内存容量（在本例中，设置虚拟内存容量为512M），安装并启用

       ![](./Documents_Assets/How_to_Use/install/online_step5-5-1.jpg)
       ![](./Documents_Assets/How_to_Use/install/online_step5-5-2.jpg)

     - 安装并启用entware

       ![](./Documents_Assets/How_to_Use/install/online_step5-6.jpg)

     - 安装并启用timezone

       ![](./Documents_Assets/How_to_Use/install/online_step5-7.jpg)

     - 安装并启用dependency

       > 在此过程中，可能出现少量黄字/红字警告，这是正常现象

       ![](./Documents_Assets/How_to_Use/install/online_step5-8.jpg)

     - 安装并启用monit

       ![](./Documents_Assets/How_to_Use/install/online_step5-9.jpg)

     - 安装并启用dnsmasq.d

       ![](./Documents_Assets/How_to_Use/install/online_step5-10.jpg)

     - 安装fwd

       ![](./Documents_Assets/How_to_Use/install/online_step5-11.jpg)

     - 阶段二完成

       ![](./Documents_Assets/How_to_Use/install/online_step5-12.jpg)

   - **阶段三**：安装用户可选插件

     - 输入并确认路由器登录用户名和密码（此操作仅在首次安装时被执行）

       ![](./Documents_Assets/How_to_Use/install/online_step5-13-1.jpg)
       ![](./Documents_Assets/How_to_Use/install/online_step5-13-2.jpg)
       ![](./Documents_Assets/How_to_Use/install/online_step5-13-3.jpg)

     - 阅读插件菜单，输入插件编号，安装对应插件

       ![](./Documents_Assets/How_to_Use/install/online_step5-14.jpg)

     - 插件安装成功，安装下一个插件

       ![](./Documents_Assets/How_to_Use/install/online_step5-15.jpg)

     - 全部插件安装完毕后，输入`0`，退出安装程序并重启路由器

       ![](./Documents_Assets/How_to_Use/install/online_step5-16.jpg)

## 离线安装

1. 准备一个空白U盘（不小于4GB；MBR），插入路由器USB接口

2. 用ssh登陆路由器后台

3. 在[此处](https://github.com/JACK-THINK/SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER/wiki/使用说明索引#离线安装)下载最新版安装包，并将其上传至路由器`/tmp/home/root`

   ![](./Documents_Assets/How_to_Use/install/offline_step3_zh-CN.jpg)

4. 执行下列代码，解压安装包

   ```shell
   cd /tmp/home/root
   tar -xzvf SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER*.tar.gz
   rm -f SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER*.tar.gz
   ```

5. 执行下列代码，将文件移动至指定位置并修改程序权限

   ```shell
   mv SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER*/script_bootloader ./
   rm -rf SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER*
   chmod -R 777 script_bootloader
   cp script_bootloader/bin/prerequisite_checker /tmp
   cp script_bootloader/bin/drive_modifier /tmp
   cd /tmp
   ```

6. 执行下列代码，检查安装环境。如无输出，则表示通过

   ```shell
   /tmp/prerequisite_checker
   ```

7. 执行下列代码，重新分区并格式化U盘

   ```shell
   /tmp/drive_modifier
   ```

8. 执行下列代码，将文件移动至指定位置

   ```shell
   mv /tmp/home/root/script_bootloader /tmp/mnt/ASUS_ROUTER
   ```

9. （可选）如果需要离线安装特定版本Entware且无升级计划，可在[此处](https://github.com/JACK-THINK/SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER/wiki/使用说明索引#Entware离线库)下载Entware离线库，并将其上传至路由器`/tmp/mnt/ASUS_ROUTER/script_bootloader/usr/entware/usr/`

10. 执行下列代码，开始安装

   ```shell
   /tmp/mnt/ASUS_ROUTER/script_bootloader/bin/install
   ```

11. （可选）如果固件中没有`tee`命令，则安装程序会在输出`***** STAGE 3: INSTALL ADDONS *****`后自动退出。执行下列代码，安装插件（系统安装完成后，仍可使用该命令补装其它插件）

   ```shell
   /tmp/mnt/ASUS_ROUTER/script_bootloader/bin/addons_install
   ```

12. 全部插件安装完毕后，执行下列代码，重启路由器

   ```shell
   /tmp/sbl_restart_router
   ```

## 修改程序

阅读`/opt/script_bootloader/usr/`中各个插件的README_zh-CN.md文件，按要求对相关程序进行修改

> **注意**
>
> - 在Windows下对程序进行修改，必须将编辑器的换行符设置为`LF`，否则程序将被损坏，无法运行
> - 在Linux下对程序进行修改，无需特别设置

## 启用/禁用插件

> 本系统插件管理由两个部分组成，如下表所示：
>
> | 插件管理者                  | 插件类型                                                 | 使用说明                                                  |
> | --------------------------- | -------------------------------------------------------- | --------------------------------------------------------- |
> | list_of_user_custom_scripts | 仅需在开机时调用一次且无需监控的插件，例如修改环境变量等 | 见下文                                                    |
> | Monit进程管理系统           | 除上述类型外的全部插件                                   | [点击查看](./script_bootloader/usr/monit/README_zh-CN.md) |

1. 用ssh登陆路由器后台

   ![](./Documents_Assets/How_to_Use/services_once/step1.jpg)

2. 执行下列代码，编辑文件list_of_user_custom_scripts

   ```shell
   vim /opt/script_bootloader/bin/list_of_user_custom_scripts
   ```

   ![](./Documents_Assets/How_to_Use/services_once/step2.jpg)

   ![](./Documents_Assets/How_to_Use/services_once/step3.jpg)

3. 启用/禁用特定插件

   - 启用插件：在插件路径前删除`#`
   - 禁用插件：在插件路径前插入`#`

   ![](./Documents_Assets/How_to_Use/services_once/step4.jpg)

4. 保存并退出

   \<ESC\>→\<:\>→\<w\>→\<q\>→\<Enter\>

5. 执行下列代码，重启路由器，相应的插件将在开机时自动启动

   ```shell
   cd /tmp && /tmp/sbl_restart_router
   ```

   ![](./Documents_Assets/How_to_Use/services_once/step5.jpg)

## 在线更新

1. 用ssh登陆路由器后台

   ![](./Documents_Assets/How_to_Use/update/step1.jpg)

2. 执行下列代码更新本系统

   ```shell
   cd /tmp && /tmp/mnt/ASUS_ROUTER/script_bootloader/bin/update
   ```

   ![](./Documents_Assets/How_to_Use/update/step2.jpg)

## 在线升级

> 当Entware发布新版本时，执行升级。此操作可在保留`/tmp/mnt/ASUS_ROUTER/home`中全部文件的同时全新安装本系统

1. 用ssh登陆路由器后台

   ![](./Documents_Assets/How_to_Use/upgrade/step1.jpg)

2. 执行下列代码升级本系统

   ```shell
   cd /tmp && /tmp/sbl_upgrade
   ```

   ![](./Documents_Assets/How_to_Use/upgrade/step2.jpg)

3. 路由器重启后，执行下列代码

   ```shell
   cp -f "/tmp/mnt/ASUS_ROUTER/script_bootloader/bin/upgrade" "/tmp/sbl_upgrade" && cd "/tmp" && "/tmp/sbl_upgrade"
   ```

   ![](./Documents_Assets/How_to_Use/upgrade/step3.jpg)

4. 后续步骤同[在线安装](#在线安装)

## 离线升级

> 当Entware发布新版本时，执行升级。此操作可在保留`/tmp/mnt/ASUS_ROUTER/home`中全部文件的同时全新安装本系统

1. 用ssh登陆路由器后台

2. 在[此处](https://github.com/JACK-THINK/SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER/wiki/使用说明索引#离线升级)下载最新版离线升级包，并将其上传至路由器`/tmp/mnt/ASUS_ROUTER/home/root`

   ![](./Documents_Assets/How_to_Use/upgrade/offline_step2_zh-CN.jpg)

3. 后续步骤同[在线升级](#在线升级)

## 卸载

1. 用ssh登陆路由器后台

   ![](./Documents_Assets/How_to_Use/uninstall/step1.jpg)

2. 执行下列代码卸载本系统

   ```shell
   cd /tmp && /tmp/sbl_uninstall
   ```

   ![](./Documents_Assets/How_to_Use/uninstall/step2.jpg)

## 还原

1. 用ssh登陆路由器后台

   ![](./Documents_Assets/How_to_Use/restore/step1.jpg)

2. 执行下列代码还原本系统

   ```shell
   cp -f /tmp/mnt/ASUS_ROUTER/script_bootloader/bin/restore /tmp && cd /tmp && /tmp/restore
   ```

   ![](./Documents_Assets/How_to_Use/restore/step2.jpg)

## 重装

1. 执行[卸载](#卸载)

2. 执行[在线安装](#在线安装)

## 升级路由器固件/恢复原厂设置

1. 执行[卸载](#卸载)

2. 自动重启后，移除路由器上全部USB设备

3. 升级路由器固件/恢复原厂设置

4. 设置路由器

5. 仅将装有本系统的U盘重新插入路由器

6. 执行[还原](#还原)

7. 自动重启后，将其余USB设备重新连接至路由器
