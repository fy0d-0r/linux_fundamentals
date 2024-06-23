# CPU (Model, Core, Thread, Cache size, Clock speed)

`cat /proc/cpuinfo`

# RAM (Capacity, DDR, Speed MT/s, Manufacturer, BANK Location)

`sudo dmidecode --type 17`

# Graphic Card (Model, GPU, VRAM, Core Clock Speed, GDDR)
`sudo hwinfo --gfxcard`
`sudo lshw -C display`

## Check VRAM Information

For AMD
```
lspci -D
cat /sys/bus/pci/devices/${pci_slot}/mem_info_vram_total
```
For Nvidia
```
nvidia-smi
LANG=C nvidia-smi --query-gpu=memory.total --format=csv,noheader,nounits
```


```
https://stackoverflow.com/questions/77708142/how-can-i-fetch-vram-and-gpu-cache-size-in-linux
```

For AMD
```
radeontop
DRI_PRIME=1 glxgears
```

Monitor GPU Performance 

# PCIe

`lspci`

# DISPLAY (Resolution, Refresh Rate, Panel Type (TN,OLED,LCD), 

# MOTHERBOARD

# POWER SUPPLY and POWER SAVING MODE



# Audio


# Operating System Informations 

`uname -a`

`cat /etc/os-release`

`neofetch`

`screenfetch`

# UTILITIES
hwinfo
hardinfo
pulseaudio-utils
mesa-utils for glxgears
