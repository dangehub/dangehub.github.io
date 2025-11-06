---
{"dg-publish":true,"dg-permalink":"save-my-synology","title":"黑群晖意外移除SSD读写缓存后开机，导致raid1存储空间损毁的挽救记录","dg-path":"自托管折腾/黑群晖意外移除SSD读写缓存后开机，导致raid1存储空间损毁的挽救记录.md","permalink":"/save-my-synology/","dgPassFrontmatter":true,"noteIcon":""}
---



# 参考文章
- [当 Synology NAS 出现故障时，如何使用计算机恢复数据？ - Synology 知识中心](https://kb.synology.cn/zh-cn/DSM/tutorial/How_can_I_recover_data_from_my_DiskStation_using_a_PC)
- [群晖存储空间损毁 Btrfs 数据恢复教程 | reizhi (roov.org)](https://roov.org/2017/11/btrfs-repair/)

# 过程记录

- 下载官方提供的 ubuntu 镜像，用 unraid 虚拟机安装 
- 在执行 `apt-get update` 报错，需要执行 `sudo apt-get remove libappstream4` （这一步上网去查说要卸载 xxxstream3，但是尝试卸载发现这个版本的系统里没有 3, 所以试了试 4，果然是版本号变了）
- 然后按教程安装需要的软件，安装完成后关闭虚拟机 
- 编辑虚拟机，把之前群晖的硬盘全挂载到 ubuntu 虚拟机上 ，重新开机
- `/dev/vg1/volume 1`
- `btrfs-find-root /dev/vg1/volume 1 &> /tmp/root.txt`
- ![42641.webp](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/%E8%87%AA%E6%89%98%E7%AE%A1%E6%8A%98%E8%85%BE/assets/42641.webp)
- 尝试恢复失败，为了防止对原盘产生破坏，打算先装一块盘试试能不能恢复
- 后面发现必须要将之前组 raid 的四块硬盘同时插入时才能恢复成功，于是立马下单了一块 16T 的矿盘
- 2022-01-02 17:50~20: 20，用时一个半小时，完成了大概 1.5T 的数据恢复，进度喜人，但是马上遇见了 unraid 自动重启，不知道是为什么（在恢复开始前我就很担心预期 30~70 小时的恢复过程一旦被打断，会不会发生什么问题）
- 刚刚系统重启的原因找到了![assets/阵列情况.webp](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/%E8%87%AA%E6%89%98%E7%AE%A1%E6%8A%98%E8%85%BE/assets/%E9%98%B5%E5%88%97%E6%83%85%E5%86%B5.webp)
	- 原来是之前 lexar 的那块硬盘又掉盘了，这个问题之前我也遇见过，很恼火，本来以为组了双 ssd 缓存就没问题了，不知道为什么刚刚还是掉盘了。这次为了解决问题，打算直接把 lexar 这块硬盘去掉。
- 如果需要恢复特定文件，可以参考这篇文章 [btrfs restore Linux 中的命令示例 – 极客日记 (thegeekdiary.com)](https://www.thegeekdiary.com/btrfs-restore-command-examples-in-linux/#:~:text=The%20btrfs%20restore%20command%20is%20a%20command-line%20utility,time%20and%20then%20restore%20it%20later%20if%20needed.)
- 在恢复过程中发现多次报错 ![63018-1762416042308.webp](/img/user/107-%E6%88%91%E7%9A%84%E5%88%9B%E4%BD%9C/%E6%96%87%E5%AD%97/%E5%8D%9A%E5%AE%A2%E5%8F%91%E5%B8%83/%E8%87%AA%E6%89%98%E7%AE%A1%E6%8A%98%E8%85%BE/assets/63018-1762416042308.webp)
	- 这些报错需要手动处理，中途如果没有及时发现就耽搁大量时间 
	- 去 github 上找文档 [btrfs-restore（8） — btrfs 文档](https://btrfs.readthedocs.io/en/latest/btrfs-restore.html)
	- 发现可以用`-i|--ignore-errors`来做忽略进程中的错误
	- `-v|--verbose` 可以打印恢复明细


2023-01-09 14: 20，终于完成了绝大部分的数据恢复工作，耗时 165h，恢复文件 506919 个，共计 15.1TB


接下来的工作：
1. 检查重要数据是否恢复，如个人照片
2. 将原来的 4 个盘格式化，安装到群晖上
3. 把数据拷回去
4. 把新的16T清空后做为pt专用盘