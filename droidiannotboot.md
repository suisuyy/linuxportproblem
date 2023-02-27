# porting process:
```
git clone https://gitlab.com/ubports/porting/reference-device-ports/android11/fairphone-4/fairphone-fp4.git
edit deviceinfo and dtb dtbo.img
then run
./build.sh -b bd
get boot.img and 
fastboot flash boot.img
get droidian from
https://github.com/droidian-images/droidian/releases/download/nightly/droidian-OFFICIAL-phosh-phone-rootfs-api30-arm64-nightly_20230227.zip
then flash it via twrp
finally boot
```


# problem detail
```
usbnet works,can use ssh droidian@10.15.19.82 to login
wifi not work
screen black after boot,boot,show debian logo,then black screen

lxc-ls --fancy
NAME    STATE   AUTOSTART GROUPS IPV4                  IPV6 UNPRIVILEGED 
android RUNNING 0         -      10.0.3.1, 10.15.19.82 -    false    


test_hwcomposer
test_hwcomposer: test_common.cpp:370: HWComposer* create_hwcomposer_window(): Assertion `err == 


there is no
android.service.composer 

phosh cant start,systemctl restart phosh not work,just hang
systemctl status phosh
○ phosh.service - Phosh, a shell for mobile phones
     Loaded: loaded (/lib/systemd/system/phosh.service; enabled; preset: enabled)
    Drop-In: /etc/systemd/system/phosh.service.d
             └─20-wlroots-hwc-env.conf, 30-force-user.conf, 40-droid-wait.conf, 90-wait.conf
     Active: inactive (dead)
       Docs: https://gitlab.gnome.org/World/Phosh/phosh


DEVICE=arnoz
cat /var/lib/lxc/android/rootfs/ueventd*.rc /vendor/ueventd*.rc | grep ^/dev | sed -e 's/^\/dev\///' | awk '{printf "ACTION==\"add\", KERNEL==\"%s\", OWNER=\"%s\", GROUP=\"%s\", MODE=\"%s\"\n",$1,$3,$4,$2}' | sed -e 's/\r//' >/etc/udev/rules.d/70-$DEVICE.rules
cat: '/var/lib/lxc/android/rootfs/ueventd*.rc': No such file or directory,
so cant regenerate udev rules
```

# device info
```
Device	Lenovo Xiaoxin Pad Plus
SoC	Qualcomm SM7225 Snapdragon 750G 5G
CPU	2x2.2 GHz Kryo 570 & 6x1.8 GHz Kryo 570
GPU	Adreno 619
Memory	6GB
Shipped Android version	Android 11, ZUI 12.5
Storage	128GB
Battery	Li-Po 7700 mAh, non-removable
Dimensions	258.4 x 163 x 7.9 mm
Display	2000 x 1200 pixels, 11 inches
Rear camera	8 MP
Front camera	13 MP
kernel 4.19.157


```
























