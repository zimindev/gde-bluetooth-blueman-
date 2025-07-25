## 📡 Blueman Bluetooth Setup Guide (Linux)

### ✅ What is Blueman?

**Blueman** is a graphical Bluetooth manager for Linux powered by BlueZ. It provides an easy way to pair, connect, trust, and manage Bluetooth devices, especially in lightweight desktop environments such as XFCE, LXQt, Openbox, or i3wm.

---

### 🖥️ Step 1: Install Required Packages

#### Arch Linux:

```bash
sudo pacman -S bluez bluez-utils blueman
```

#### Ubuntu / Debian:

```bash
sudo apt update
sudo apt install bluez blueman
```

#### Fedora:

```bash
sudo dnf install bluez blueman
```

> `bluez` provides the Bluetooth stack, `blueman` is the GUI utility. In most cases, installing `blueman` pulls in necessary dependencies.

---

### ⚙️ Step 2: Enable and Start the Bluetooth Service

#### Arch Linux / Fedora:

```bash
sudo systemctl enable bluetooth.service
sudo systemctl start bluetooth.service
```

#### Ubuntu / Debian:

Bluetooth service is usually enabled by default, but you can verify with:

```bash
sudo systemctl status bluetooth.service
```

If it's not running, start it:

```bash
sudo systemctl start bluetooth.service
```

---

### 📶 Step 3: Launch Blueman

You can launch the graphical manager with:

```bash
blueman-manager
```

Or start the applet (system tray icon):

```bash
blueman-applet &
```

> You can add this to your desktop environment's startup scripts (e.g. i3, XFCE, Openbox) for quick access.

---

### 🔒 Step 4: Unblock Bluetooth (If Needed)

If the adapter is blocked:

```bash
rfkill list bluetooth
rfkill unblock bluetooth
```

---

### 🎧 Step 5: Connect Bluetooth Audio Devices

#### For PulseAudio:

Install Bluetooth audio support:

* **Arch:**

```bash
sudo pacman -S pulseaudio-bluetooth
```

* **Ubuntu/Debian:**

```bash
sudo apt install pulseaudio-module-bluetooth
```

* **Fedora:**

```bash
sudo dnf install pulseaudio-module-bluetooth
```

Restart PulseAudio:

```bash
pulseaudio -k
```

#### For PipeWire:

If you're using PipeWire (modern replacement for PulseAudio):

* **Arch:**

```bash
sudo pacman -S pipewire pipewire-pulse wireplumber
```

* **Ubuntu:**

```bash
sudo apt install pipewire-audio
```

* **Fedora:**

```bash
sudo dnf install pipewire pipewire-pulseaudio
```

Restart user services:

```bash
systemctl --user restart pipewire
```

---

### 🚀 Step 6: Autostart Blueman in Lightweight Environments

To start the tray icon automatically (e.g., in i3wm, Openbox):

```bash
exec --no-startup-id blueman-applet &
```

Add this to your window manager's config or startup file.

---

### 🧰 Step 7: Optional – Use CLI via `bluetoothctl`

```bash
bluetoothctl
```

Inside the interactive shell:

```bash
power on
agent on
default-agent
scan on
pair XX:XX:XX:XX:XX:XX
trust XX:XX:XX:XX:XX:XX
connect XX:XX:XX:XX:XX:XX
```

Replace `XX:XX...` with your device’s MAC address.

---

### 📚 Additional Resources

* Arch Wiki – [Blueman](https://wiki.archlinux.org/title/Blueman)
* Arch Wiki – [Bluetooth](https://wiki.archlinux.org/title/Bluetooth)
* Ubuntu Help – [Bluetooth Setup](https://help.ubuntu.com/community/BluetoothSetup)
* Fedora Docs – [Bluetooth](https://docs.fedoraproject.org/en-US/quick-docs/bluetooth/)
* Man page – `man blueman-manager`
