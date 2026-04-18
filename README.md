# Kodachi Live Login Bypass
Fix for Kodachi Linux live login issue by enabling autologin via system configuration changes.

![Linux](https://img.shields.io/badge/Linux-Kodachi-blue)
![Status](https://img.shields.io/badge/status-working-success)

## 🛠️ Kodachi Autologin Fix

### 📌 Overview

This repository documents a workaround for a login issue in Kodachi Linux live environment, where the system does not accept the correct password during boot.

The solution involves modifying system configuration files to enable automatic login, allowing access to the system and continuation of the installation process.

---

## ❗ Problem

When booting into Kodachi live mode (I tryed with balena etcher, ventoy and rufus):

* The system prompts for a password
* The correct password is rejected (r@@t00)
* User is unable to access the desktop environment

This effectively blocks further usage or installation.

---

## 🔍 Possible Cause

This behavior may be related to:

* Misconfigured display manager
* Authentication issues in the live environment
* Bugs in specific Kodachi builds

*(Exact root cause may vary depending on version, I used the linux-kodachi-xfce-9.0.1-amd64 version)*

---

## ✅ Solution (Autologin Workaround)

The issue can be bypassed by enabling autologin through system configuration in GNU.

### Steps:

1. Boot into recovery or root shell (via GRUB)
2. In kodachi login we have option to enter in file config pressing E (you will be able to edit the file directly using this option)
3. Locate the options "random.trust_cpu=off"; "random.trust_bootloader=off" and "noautologin"
4. Change to "random.trust_cpu=on"; "random.trust_bootloader=on" and "autologin"
Note: If you will install Kodachi using the native installer change the screen lock configs, if you dont do that the system will request for login and you will need to repeat the process (believe, i forgot this on first time)

Example: (complete file)

```bash
setparams 'Kodachi Live [*]'

      set gtfpayload=keep
      linux     /live/vmlinuz-6.12.74+deb13+1-amd64 boot=live components noeject hostname=kodachi slab_nomerge init_on_alloc=1 vsycall=none random.trust_cpu=off random.trust_bootloader=off username=kodachi noautologin ---
      initrd    /live/initrd.img-6.12.74+deb13+1-amd64
```

How it should look after

```bash
setparams 'Kodachi Live [*]'

      set gtfpayload=keep
      linux     /live/vmlinuz-6.12.74+deb13+1-amd64 boot=live components noeject hostname=kodachi slab_nomerge init_on_alloc=1 vsycall=none random.trust_cpu=on random.trust_bootloader=on username=kodachi autologin ---
      initrd    /live/initrd.img-6.12.74+deb13+1-amd64
```

5. Save and exit (Ctrl + X and F10)
#### WARNING - DONT REBOOT THE SISTEM (If you reboot the system, it will rewrite the configuration.)

## ⚠️ Security Warning

Enabling autologin:

* Bypasses authentication
* Reduces system security
* Should only be used as a temporary workaround

Do **not** use this configuration in production or sensitive environments.

---

## 🧪 Tested On

* Kodachi Linux (Live USB via Balena Etcher)
* Samsung BAR Plus 256 GB – 400 MB/s USB 3.1 Flash Drive
* Boot via GRUB
* Issue reproduced and fixed successfully

---

## 🤝 Contributing

If you encountered the same issue or found a different fix, feel free to open an issue or submit a pull request.
