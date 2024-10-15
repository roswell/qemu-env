ARCH=ppc
MEM=2048
HDD=hdd.qcow2
HDDSIZE=22G
ISO=leopard.iso

help:
	echo check https://github.com/roswell/qemu-env/releases/tag/2024.10.15
install: $(HDD)
	qemu-system-$(ARCH) \
		-L pc-bios \
		-boot d \
		-M mac99,via=pmu \
		-m $(MEM) \
		-hda $(HDD) \
		-cdrom $(ISO)
launch:
	qemu-system-$(ARCH) \
		-L pc-bios \
		-boot c \
		-M mac99,via=pmu \
		-m $(MEM) \
		-hda $(HDD) \
		-device VGA,edid=on
$(HDD):
	qemu-img create -f qcow2 $@ $(HDDSIZE)
