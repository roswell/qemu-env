ARCH=aarch64
MEM=1024
HDD=hdd.qcow2
HDDSIZE=8G
#http://ftp.jaist.ac.jp/pub/raspberrypi/raspios_armhf/images/raspios_armhf-2020-08-24/2020-08-20-raspios-buster-armhf.zip
#http://ftp.jaist.ac.jp/pub/raspberrypi/raspios_armhf/images/raspios_armhf-2024-07-04/2024-07-04-raspios-bookworm-armhf.img.xz
URL=https://downloads.raspberrypi.com/raspios_lite_armhf/images/raspios_lite_armhf-2024-07-04/2024-07-04-raspios-bookworm-armhf-lite.img.xz
XZ=$(notdir $(URL))
IMG=$(basename $(XZ))
FAT=0.fat
KERNEL=kernel7.img
DTB=bcm2709-rpi-2-b.dtb

ZURL=https://github.com/snmsts/qemu-env/releases/download/2024.10.06/archive.7z
Z=$(notdir $(ZURL))

help:
	echo $(IMG)
install: $(KERNEL) $(DTB) $(IMG)
	qemu-system-$(ARCH) \
	-m $(MEM) \
	-M raspi2b \
	-kernel $(KERNEL) \
	-dtb $(DTB)  \
	-drive format=raw,file=$(IMG) \
	-append "console=ttyAMA0 root=/dev/mmcblk0p2 rw rootwait rootfstype=ext4 dwc_otg.fiq_fsm_enable=0 bcm2708_fb.fbwidth=1280 bcm2708_fb.fbheight=720" \
	-serial stdio \
	-no-reboot \
	-device usb-kbd \
	-device usb-tablet \
	-device usb-net,netdev=net0 \
	-netdev user,id=net0,hostfwd=tcp::2222-:22

launch: install
$(XZ):
	curl -L -O $(URL)
$(IMG):
	$(MAKE) $(XZ)
	unxz $(XZ)
	$(MAKE) resize
resize:
	qemu-img resize $(IMG) $(HDDSIZE)
$(FAT): $(IMG)
	7zz x -y $(IMG) $@ && touch $@
$(KERNEL):
	#$(MAKE) $(FAT)
	#7zz x -y $(FAT) $@ && touch $@
	curl -L -O https://github.com/roswell/qemu-env/releases/download/2024.10.06/kernel7.img
$(DTB):
	#$(MAKE) $(FAT)
	#7zz x -y $(FAT) $@ && touch $@
	curl -L -O https://github.com/roswell/qemu-env/releases/download/2024.10.06/bcm2709-rpi-2-b.dtb
$(Z):
	curl -L -O $(ZURL)

extract: 
	$(MAKE) $(Z)
	7z x $(Z)
	rm $(Z)
