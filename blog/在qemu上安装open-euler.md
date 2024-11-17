---
date: 2024-11-14
---

参考文章：

- 24.03LTS的文档： https://docs.openeuler.org/en/docs/24.03_LTS/docs/Installation/RISC-V-QEMU.html
- 23年9月的安装博文： https://www.openeuler.org/en/blog/phoebe/2023-09-26-Run-openEuler-RISC-V-On-Qemu.html
- 
# 大致流程

- 安装qemu
- 下载系统镜像和EFI固件，risv和arm架构基本都需要EFI固件才能启动系统
- 创建虚拟硬盘
- 命令行启动，把上面的文件穿进去，带上一大堆配置

# 安装 qemu

文档建议安装qemu8以上的版本。
我是wsl上的ubunutu22lts， ~~直接apt安装了， 直接装的太老了是`6.2.0`。~~
~~我需要编译安装一个8.1以后的qemu。~~
废那事，我下载Windows版本的qemu了，版本是8.1.0 (v8.1.0-12034-g129566d84e)。

# 下载镜像

```bash
# EFI Firmware
wget https://mirrors.jxust.edu.cn/openeuler/openEuler-24.03-LTS/virtual_machine_img/riscv64/RISCV_VIRT_CODE.fd
wget https://mirrors.jxust.edu.cn/openeuler/openEuler-24.03-LTS/virtual_machine_img/riscv64/RISCV_VIRT_VARS.fd

# 操作系统镜像
wget https://mirrors.jxust.edu.cn/openeuler/openEuler-24.03-LTS/virtual_machine_img/riscv64/openEuler-24.03-LTS-riscv64.qcow2.xz

# 启动脚本
wget https://mirrors.jxust.edu.cn/openeuler/openEuler-24.03-LTS/virtual_machine_img/riscv64/start_vm.sh

# 解压
tar xf openEuler-24.03-LTS-riscv64.qcow2.xz
```

# 启动模拟器
Windows下要翻译一下他的bash脚本，删除随机数设备，把内存改小，不然报错`qemu-system-riscv64: qemu_fdt_add_subnode: Failed to create subnode /memory@80000000: FDT_ERR_EXISTS`
能跑的版本是：

```bat
qemu-system-riscv64 ^
  -machine virt,pflash0=pflash0,pflash1=pflash1,acpi=off ^
  -smp 4 -m 6G ^
  -object memory-backend-ram,size=3G,id=ram1 ^
  -numa node,memdev=ram1 ^
  -object memory-backend-ram,size=3G,id=ram2 ^
  -numa node,memdev=ram2 ^
  -blockdev node-name=pflash0,driver=file,read-only=on,filename="RISCV_VIRT_CODE.fd" ^
  -blockdev node-name=pflash1,driver=file,filename="RISCV_VIRT_VARS.fd" ^
  -drive file=1.qcow2,format=qcow2,id=hd0 ^
  -device virtio-vga ^
  -device virtio-blk-device,drive=hd0,bootindex=1 ^
  -device virtio-net-device,netdev=usernet ^
  -netdev user,id=usernet,hostfwd=tcp::"12055"-:22 ^
  -device qemu-xhci -usb -device usb-kbd -device usb-tablet
```

# 运行

默认密码：openEuler12#$
下载的镜像没有装图形界面，要切换到serial0才有输出，快捷键<kbd>Ctrl+Alt+3</kbd>。
![[Pasted image 20241116211740.png]]
系统启动成功后换Windows Terminal运行`ssh -p12055 root@localhost`进去操作了。
# 安装图像界面
这次要开发个GUI的app，要安装图形界面。
现在的 [文档](https://docs.openeuler.org/zh/docs/22.09/docs/desktop/%E5%AE%89%E8%A3%85DDE.html) 里面四种桌面环境，DDE的安装的命令最少了试试。