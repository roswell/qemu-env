ARCH=sparc
MEM=1024
HDD=hdd.qcow2
HDDSIZE=8G
ORIG_HDD=debian_etch_sparc_small.qcow2
ISOURL=https://cdimage.debian.org/mirror/cdimage/archive/4.0_r4a/sparc/iso-cd/debian-40r4a-sparc-netinst.iso
ISO=$(notdir $(ISOURL))
ZURL=https://github.com/snmsts/qemu-env/releases/download/2024.10.04/archive.7z
Z=$(notdir $(ZURL))

help:
install: $(HDD) $(ISO)
	qemu-system-$(ARCH) \
		-M SS-10 \
		-m $(MEM) \
		-hda $(HDD) -nographic \
		-drive file=$(ISO),format=raw,if=scsi,bus=0,unit=2,media=cdrom,readonly=on \
		-boot d
launch: $(HDD)
	qemu-system-$(ARCH) \
		-M SS-10 \
		-m $(MEM) \
		-hda $(HDD) -nographic

$(HDD):
	qemu-img create -f qcow2 $@ $(HDDSIZE)
$(ISO):
	curl -L -O $(ISOURL)
$(Z):
	curl -L -O $(ZURL)
extract: $(Z)
	7z x $(Z)
