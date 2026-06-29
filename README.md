```markdown
<div align="center">

# 🐧 The Ultimate Arch Linux to BlackArch Guide
### 🚀 *From Noob to Pro: A Comprehensive Journey*

<br>

<img src="https://img.shields.io/badge/Owner-Ch4120N-181717?style=for-the-badge&logo=github" alt="Owner">
<img src="https://img.shields.io/badge/Guides-Very%20Helpful-4c1?style=for-the-badge" alt="Guides">

<br>

*Transform your fresh Arch system into a powerful penetration testing powerhouse.*

</div>

---

## 🌟 About This Repository

Welcome! This repository is proudly maintained by **Ch4120N** and is dedicated to providing **very helpful guides** for the cybersecurity and Linux community. 

> **👨‍💻 Owner:** Ch4120N  
> **📖 Content:** Very helpful, step-by-step, and fully explained guides.

If you find this guide useful, please consider dropping a ⭐ on the GitHub repository to support the project!

---

## 📚 Table of Contents

<details>
<summary><b>Click to expand the Table of Contents</b></summary>

1. [🎯 Introduction: Why Arch → BlackArch?](#-introduction-why-arch--blackarch)
2. [⚠️ IMPORTANT NOTE – Read This First!](#-important-note--read-this-first)
3. [🤔 What Is a Virtual Machine?](#-what-is-a-virtual-machine)
4. [🛠️ Step 0: Setting Up a Virtual Machine](#️-step-0-setting-up-a-virtual-machine)
5. [🔥 Step 1: Boot from the Arch Linux ISO](#-step-1-boot-from-the-arch-linux-iso)
6. [🌐 Step 2: Connect to the Internet](#-step-2-connect-to-the-internet)
7. [⏰ Step 3: Update the System Clock](#-step-3-update-the-system-clock)
8. [💾 Step 4: Partition the Disk](#-step-4-partition-the-disk)
9. [🧹 Step 5: Format the Partitions](#-step-5-format-the-partitions)
10. [📂 Step 6: Mount the File Systems](#-step-6-mount-the-file-systems)
11. [📦 Step 7: Install the Base System](#-step-7-install-the-base-system)
12. [🔧 Step 8: Generate the Filesystem Table (fstab)](#-step-8-generate-the-filesystem-table-fstab)
13. [🏠 Step 9: Chroot into the New System](#-step-9-chroot-into-the-new-system)
14. [🌐 Step 10: Set the Time Zone](#-step-10-set-the-time-zone)
15. [🗺️ Step 11: Set the Locale](#️-step-11-set-the-locale)
16. [⌨️ Step 12: Set the Keyboard Layout](#️-step-12-set-the-keyboard-layout)
17. [🏷️ Step 13: Set the Hostname](#️-step-13-set-the-hostname)
18. [🔑 Step 14: Set Root Password](#-step-14-set-root-password)
19. [📡 Step 15: Network Configuration](#-step-15-network-configuration)
20. [🛠️ Step 16: Initramfs](#️-step-16-initramfs)
21. [🍔 Step 17: Install a Bootloader](#-step-17-install-a-bootloader)
22. [✅ Step 18: Exit, Unmount, and Reboot](#-step-18-exit-unmount-and-reboot)
23. [🎉 Step 19: First Boot – Login](#-step-19-first-boot--login)
24. [🧑‍💻 Step 20: Post‑Installation (User & Sudo)](#-step-20-postinstallation--user--sudo)
25. [🎨 Step 21: Install a Desktop Environment](#-step-21-install-a-desktop-environment)
26. [🖤 Step 22: Convert to BlackArch (THE MAIN GOAL)](#-step-22-convert-to-blackarch-the-main-goal)
27. [🧠 Important Notes & Final Tips](#-important-notes--final-tips)

</details>

---

## 🎯 Introduction: Why Arch → BlackArch?

**BlackArch Linux** is an elite penetration testing distribution built on top of Arch Linux, offering over 2,800 security tools. Instead of downloading the BlackArch ISO (which can be buggy or overwhelming), the **recommended way** by the BlackArch team is to install a minimal, stable Arch system and then convert it. 

**Benefits of this approach:**
- 🛡️ **Rock-solid base:** You build a stable Arch system yourself.
- 🎛️ **Full control:** You choose exactly which tools to install.
- 🪶 **Lean system:** No bloatware, only what you need.
- 🔄 **Rolling release:** Always get the latest tools via Arch's repositories.

---

## ⚠️ IMPORTANT NOTE – Read This First!

> [!WARNING]
> **I strongly recommend you install Arch Linux inside a Virtual Machine first.**  
> This way, you **won't** accidentally erase your personal files or mess up your main operating system. When you've successfully installed Arch and converted it to BlackArch in the VM at least **twice**, then you can confidently do it on a real computer.

---

## 🤔 What Is a Virtual Machine?

A **Virtual Machine (VM)** is like a "computer inside your computer". It uses software (like VirtualBox or QEMU) to create a fake PC where you can install and run operating systems without affecting your real machine. Think of it as a safe sandbox for learning and experimenting.

---

## 🛠️ Step 0: Setting Up a Virtual Machine

If you're installing on real hardware, skip this step. Otherwise, follow these instructions:

### 1. Choose Your VM Software
- **VirtualBox** (free, easy) – [Download](https://www.virtualbox.org/)
- **QEMU/KVM** (faster, more advanced) – usually preinstalled on Linux.

### 2. Create a New VM
- **Name:** Arch Linux (we'll convert to BlackArch later)  
- **Type:** Linux  
- **Version:** Arch Linux (or Other Linux 64‑bit)  
- **Memory (RAM):** At least **4 GB** (8 GB recommended for heavy tools)  
- **Hard disk:** Create a virtual disk – size **40 GB** or more (dynamic allocation is fine) because BlackArch tools can take a lot of space.  
- **Network:** Enable NAT or Bridged (NAT works out‑of‑the‑box)  

> [!TIP]
> In VirtualBox, go to **Settings → Storage** and attach the Arch ISO file to the optical drive. Then boot the VM.

---

## 🔥 Step 1: Boot from the Arch Linux ISO

1. Download the latest Arch ISO from [archlinux.org](https://archlinux.org/download/).
2. Burn it to a USB (or attach to VM) and boot from it.
3. You'll see a menu – select **"Arch Linux install medium (x86_64, UEFI)"** (or BIOS).  
4. Once booted, you'll be at a root shell prompt (`root@archiso ~ #`).  

> [!NOTE]
> **Pro tip:** Change the keyboard layout if needed with `loadkeys <layout>` (e.g., `loadkeys fr` for French). The default is US.

---

## 🌐 Step 2: Connect to the Internet

You **must** have an internet connection to download packages.

### 🌍 Wired Ethernet
Usually works automatically. Test with:
```bash
ping -c 3 archlinux.org
```

### 📶 WiFi
Use the interactive `iwctl` tool:
```bash
iwctl
# Inside the iwctl prompt:
device list                  # see your wireless device (e.g., wlan0)
station wlan0 scan
station wlan0 get-networks   # list available networks
station wlan0 connect "SSID" # replace SSID with your network name
# enter password if prompted
exit
```

---

## ⏰ Step 3: Update the System Clock

Ensure your system clock is accurate to prevent package signature errors:

```bash
timedatectl set-ntp true
timedatectl status   # verify it's enabled and sync'ed
```

---

## 💾 Step 4: Partition the Disk

We need to prepare the storage. First, identify your disk:

```bash
lsblk   # shows all disks and partitions
```

Your main disk might be `/dev/sda` (SATA/BIOS) or `/dev/nvme0n1` (NVMe SSD). We'll refer to it as `/dev/sdX` – **replace with your actual device**.

> [!IMPORTANT]
> **Check if you're booted in UEFI:**  
> Run `ls /sys/firmware/efi/efivars`. If the directory exists and is not empty, you're in UEFI mode (Use GPT). If it doesn't exist, you're in BIOS/Legacy mode (Use MBR).

### Why `cfdisk`?
We use **`cfdisk`** instead of `fdisk` because it provides a visual, menu-driven interface that is much safer and easier for beginners. You can see your partition layout clearly and navigate with arrow keys.

### Option 1: UEFI Systems (GPT Partition Table)
Run `cfdisk /dev/sda`. If prompted for a label type, select **`gpt`**.

1. **Create EFI System Partition (ESP):**
   - Select **[ New ]** → Enter size: `512M` → Select **[ Primary ]**
   - Select **[ Type ]** → Choose `EFI System`
2. **Create Swap:**
   - Select **[ New ]** → Enter size: `4G` → Select **[ Primary ]**
   - Select **[ Type ]** → Choose `Linux swap`
3. **Create Root (`/`):**
   - Select **[ New ]** → Press <kbd>Enter</kbd> (uses all remaining space) → Select **[ Primary ]**
   - Type is already `Linux filesystem`
4. **Write Changes:**
   - Select **[ Write ]** → Type `yes` to confirm (⚠️ **This will erase data!**)
   - Select **[ Quit ]**

### Option 2: BIOS/Legacy Systems (MBR Partition Table)
Run `cfdisk /dev/sda`. If prompted for a label type, select **`dos`**.

1. **Create Boot Partition:**
   - Select **[ New ]** → Enter size: `512M` → Select **[ Primary ]**
   - Select **[ Bootable ]** (to set the boot flag)
2. **Create Swap:**
   - Select **[ New ]** → Enter size: `4G` → Select **[ Primary ]**
   - Select **[ Type ]** → Choose `Linux swap`
3. **Create Root (`/`):**
   - Select **[ New ]** → Press <kbd>Enter</kbd> (uses all remaining space) → Select **[ Primary ]**
4. **Write Changes:**
   - Select **[ Write ]** → Type `yes` to confirm (⚠️ **This will erase data!**)
   - Select **[ Quit ]**

---

## 🧹 Step 5: Format the Partitions

Now we format the partitions with the appropriate file systems.

### For UEFI (GPT):
```bash
# 1. EFI partition (must be FAT32)
mkfs.fat -F32 /dev/sda1

# 2. Swap partition
mkswap /dev/sda2 && swapon /dev/sda2

# 3. Root partition
mkfs.ext4 /dev/sda3
```

### For BIOS (MBR):
```bash
# 1. Boot partition (ext4)
mkfs.ext4 /dev/sda1

# 2. Swap partition
mkswap /dev/sda2 && swapon /dev/sda2

# 3. Root partition
mkfs.ext4 /dev/sda3
```

---

## 📂 Step 6: Mount the File Systems

For both UEFI and MBR, we mount the root partition to `/mnt` and the boot partition to `/mnt/boot`:

```bash
# Mount root partition
mount /dev/sda3 /mnt

# Create and mount boot directory
mkdir -p /mnt/boot
mount /dev/sda1 /mnt/boot
```

---

## 📦 Step 7: Install the Base System

Use `pacstrap` to install the base packages, kernel, and firmware:

```bash
pacstrap /mnt base linux linux-firmware base-devel vim nano networkmanager
```

> [!NOTE]
> **What are these packages?**
> - `base`: The minimal Arch system (shell, core utilities).
> - `linux` & `linux-firmware`: The kernel and hardware drivers.
> - `base-devel`: Essential for compiling packages (highly recommended for BlackArch).
> - `vim` & `nano`: Text editors.
> - `networkmanager`: To manage network connections post-install.

---

## 🔧 Step 8: Generate the Filesystem Table (`fstab`)

The system needs to know which partitions to mount at boot.

```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

**Verify it:** `cat /mnt/etc/fstab`. It should list your partitions with their UUIDs.

---

## 🏠 Step 9: Chroot into the New System

We now "change root" into the new installation to configure it from the inside.

```bash
arch-chroot /mnt
```

*Your prompt will change to `root@archiso / #` – you are now inside your new Arch system!*

---

## 🌐 Step 10: Set the Time Zone

List available zones and set yours:

```bash
# Example for America/New_York:
ln -sf /usr/share/zoneinfo/America/New_York /etc/localtime

# Synchronize the hardware clock
hwclock --systohc
```

---

## 🗺️ Step 11: Set the Locale

Edit `/etc/locale.gen` to uncomment your preferred locale (e.g., `en_US.UTF-8 UTF-8`):

```bash
nano /etc/locale.gen   # Remove the '#' in front of your language
```

Generate the locales:
```bash
locale-gen
```

Create `/etc/locale.conf` to set the system language:
```bash
echo "LANG=en_US.UTF-8" > /etc/locale.conf
```

---

## ⌨️ Step 12: Set the Keyboard Layout (Optional)

If you need a non‑US layout, create `/etc/vconsole.conf`:

```bash
echo "KEYMAP=us" > /etc/vconsole.conf   # replace 'us' with your layout (e.g., fr, de)
```

---

## 🏷️ Step 13: Set the Hostname

Choose a cool name for your computer (e.g., `blackarch-box`):

```bash
echo "blackarch-box" > /etc/hostname
```

Edit `/etc/hosts` to map the hostname:
```bash
nano /etc/hosts
```
Add these lines:
```text
127.0.0.1   localhost
::1         localhost
127.0.1.1   blackarch-box.localdomain   blackarch-box
```

---

## 🔑 Step 14: Set Root Password

```bash
passwd
```
*Enter a strong password. Note: You won't see characters as you type!*

---

## 📡 Step 15: Network Configuration

Enable the NetworkManager service so it starts automatically after boot:

```bash
systemctl enable NetworkManager
```

---

## 🛠️ Step 16: Initramfs

For a standard installation, the default initramfs is fine. Just rebuild it to be safe:

```bash
mkinitcpio -P
```

---

## 🍔 Step 17: Install a Bootloader

This is critical to boot your new system. We'll cover **GRUB** for UEFI and BIOS.

### 🟢 For UEFI Systems

```bash
# 1. Install GRUB and EFI boot manager
pacman -S grub efibootmgr

# 2. Install GRUB to the EFI directory
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB

# 3. Generate the GRUB configuration file
grub-mkconfig -o /boot/grub/grub.cfg
```

### 🔵 For BIOS/Legacy Systems

```bash
# 1. Install GRUB
pacman -S grub

# 2. Install GRUB to the Master Boot Record (replace /dev/sda with your disk)
grub-install --target=i386-pc /dev/sda

# 3. Generate config
grub-mkconfig -o /boot/grub/grub.cfg
```

---

## ✅ Step 18: Exit, Unmount, and Reboot

```bash
# Exit the chroot environment
exit

# Unmount all partitions
umount -R /mnt

# Reboot the system
reboot
```

> [!TIP]
> **Remove the installation media** (ISO/USB) when the machine restarts, or change the boot order in your BIOS/VM settings to boot from the hard disk.

---

## 🎉 Step 19: First Boot – Login

After reboot, you'll see the GRUB menu. Select Arch Linux and boot. You'll be greeted with a login prompt:

```text
blackarch-box login:
```
Login as `root` with the password you set in Step 14.

---

## 🧑‍💻 Step 20: Post‑Installation (User & Sudo)

For security, you should **not** use `root` daily. Create a regular user:

```bash
# Create user and add to 'wheel' group
useradd -m -G wheel -s /bin/bash your_username

# Set password for the new user
passwd your_username
```

**Give sudo privileges:**
```bash
pacman -S sudo
EDITOR=nano visudo
```
Find the line `%wheel ALL=(ALL:ALL) ALL` and **uncomment it** (remove the `#`). Save and exit.

Now log out (`exit`) and log in as your new user.

---

## 🎨 Step 21: Install a Desktop Environment (Optional)

Now you have a working Arch system, but it's command‑line only. To install a graphical interface (highly recommended for BlackArch tools), pick one:

| Desktop Environment | Command to Install | Display Manager |
| :--- | :--- | :--- |
| **KDE Plasma** | `sudo pacman -S plasma-meta kde-applications-meta` | `sddm` |
| **GNOME** | `sudo pacman -S gnome gnome-extra` | `gdm` |
| **XFCE** (Lightweight) | `sudo pacman -S xfce4 xfce4-goodies` | `lightdm` |

**Enable the display manager** (example for SDDM):
```bash
sudo systemctl enable sddm
```
Then reboot. You'll get a beautiful graphical login!

---

## 🖤 Step 22: Convert to BlackArch (THE MAIN GOAL)

Now that you have a fully functional Arch Linux system, it's time to transform it into BlackArch.

### 🤔 Why Convert Instead of Installing BlackArch ISO?

| Aspect | Converting Arch → BlackArch | Installing BlackArch ISO |
| :--- | :--- | :--- |
| **Stability** | 🟢 You get a stable Arch base you built yourself | 🔴 ISOs can sometimes suffer from bugs |
| **Control** | 🟢 You control every package and config | 🔴 Pre-configured with tools you may never use |
| **Flexibility** | 🟢 Install only the tools you need | 🔴 Full ISO (~22 GB) installs everything |
| **Learning** | 🟢 You understand exactly what's on your system | 🔴 You inherit someone else's choices |

### 🚀 Step‑by‑Step Conversion

> [!WARNING]
> Make sure you have sufficient disk space (at least 20 GB free) and a stable internet connection.

#### 1. Download and Run the BlackArch Strap Script

```bash
# Download the strap script
curl -O https://blackarch.org/strap.sh

# Verify the SHA1 sum (Optional but recommended for security)
echo "5ea40d49ecd00f61b0de78d19a6372d754a371c0 strap.sh" | sha1sum -c

# Make it executable
chmod +x strap.sh

# Run it with sudo
sudo ./strap.sh
```

#### 2. Update Your System

```bash
sudo pacman -Syyu
```

#### 3. Verify the Repository

```bash
# List all available BlackArch packages
pacman -Sl blackarch | head -20

# List all BlackArch tool categories
pacman -Sg | grep blackarch
```

### 🛠️ Installing BlackArch Tools (The Right Way)

#### ❌ Option 1: Install ALL Tools (NOT Recommended)
```bash
sudo pacman -S blackarch
```
> *This will install over 2,800 tools, consume ~22 GB, and make updates a nightmare.*

#### ✅ Option 2: Install by Category (⭐ Highly Recommended)
BlackArch tools are organized into categories. Install only what you need:

```bash
# List all categories
pacman -Sg | grep blackarch

# Install a specific category (e.g., web exploitation tools)
sudo pacman -S blackarch-webapp

# Install wireless tools
sudo pacman -S blackarch-wireless
```

**Common Categories:**
- `blackarch-webapp` – Web application penetration testing
- `blackarch-wireless` – Wireless network auditing
- `blackarch-exploitation` – Exploitation frameworks (Metasploit, etc.)
- `blackarch-forensic` – Forensics and data recovery
- `blackarch-reversing` – Reverse engineering (radare2, Ghidra)
- `blackarch-crypto` – Cryptography tools

#### 🎯 Option 3: Install Individual Tools
```bash
# Search for a tool
pacman -Ss burpsuite

# Install a specific tool
sudo pacman -S burpsuite
```

---

## 🧠 Important Notes & Final Tips

- 💾 **Always backup important data** before partitioning.
- 📖 **Arch Wiki & BlackArch Wiki** are your best friends if you get stuck.
- 🔄 **Update often:** `sudo pacman -Syu` keeps your system and tools fresh.
- 🚫 **Don't use `archinstall`** – this guide teaches you the manual way so you understand every piece of your system.
- ⚖️ **Ethical Use:** Remember that these tools are for legitimate security testing and educational purposes only. Always obtain proper authorization before testing any network or system.

---

<div align="center">

## 🔚 Conclusion

You've done it! 🎉  
You've not only installed Arch Linux from scratch but also transformed it into a fully functional **BlackArch** penetration testing environment. Pat yourself on the back – this is a huge achievement.

<br>

**Happy Hacking (Ethically)! 🐧💻🔒**

<br>

*Maintained with ❤️ by **Ch4120N** on GitHub*  
*If this guide helped you, please ⭐ the repository!*

</div>