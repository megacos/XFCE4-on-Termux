# XFCE4-on-Termux
menginstall xfce desktop di android melalui termux

# XFCE4-on-Termux
menginstall xfce desktop di android melalui termux
## 1. instal termux
unduh dan install termux melalui [github](https://github.com/termux/termux-app/releases "pergi ke github repo termux") atau [f-droid](https://f-droid.org/packages/com.termux "pergi ke f-droid termux")
## 2. update termux
```markdown
pkg update
```
## 3. install xfce desktop
```markdown
pkg install xfce4
```
## 4. install termux x11
install termux x11 baik di termux maupun di android
**_instal x11 di termux_**
```markdown
pkg install termux-x11-nightly
```
**_install di android_**
unduh dan install melalui [github](https://github.com/termux/termux-x11/releases), sesusikan dengan versi processor anda, jika bingung pilih universal saja
## 5. settings termux
ini aku kurang paham fungsinya apa, jadi mau diskip juga gpp

edit properties termux 
```markdown
nano ~/.termux/termux.properties
```
cari `General` set dan enable "`allow-external-apps = true`" , enable nya dengan hapus tanda `#`

## 6. set android limit process
pertama cari tahu process limit hp anda melalu termux
```markdown
sudo /system/bin/dumpsys activity settings | grep max_phantom_processes
```
jika hasilnya `4096` itu bagus tapi klo `32` mari kita buka limitnya wkwkwk
```markdown
sudo /system/bin/device_config put activity_manager max_phantom_processes 4096
```

## 7. setup X11 server
buat koneksi antara graphic server dengan android termux-x11
```markdown
export XDG_RUNTIME_DIR=${TMPDIR}
```
kemudian
```markdown
termux-x11 :0 &
```

## 8. jalankan xfce4
ketik ini dan buka termux-x11 di android
```markdown
env DISPLAY=:0 xfce4-session
```
**selamat anda sudah bisa menjalan linux gui di Android !! :)**
## bashscript untuk memulai xfce
jika semua langkah sudah anda lakukan, anda dapat memulai xfce melalui script, karena setiap termux memulai dari awal, anda harus memulai dari menghubungkan server ke android untuk mempersingkatnya buatlah script seperti ini
```markdown
#!/bin/bash
sudo /system/bin/device_config put activity_manager max_phantom_processes 4096
export XDG_RUNTIME_DIR=${TMPDIR}
termux-x11 :0 &
sleep 2s
env DISPLAY=:0 xfce4-session
```
simpan dan beri nama apapun misalnya `mulai.sh` kemudian buka terminal di directory file tersebut dan ketik ketik `chmod u+x mulai.sh`
