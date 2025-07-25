## 📡 Blueman Bluetooth Setup Guide (Linux)

### ✅ What is Blueman?

**Blueman** — це графічна утиліта для керування Bluetooth-пристроями у Linux. Вона базується на `bluez` і надає зручний інтерфейс для з'єднання, розриву, довіри й налаштування Bluetooth-пристроїв. Ідеально підходить для легких середовищ, таких як XFCE, i3, Openbox тощо.

---

### 🖥️ Step 1: Install Bluetooth Packages

#### 🐧 Arch Linux:

```bash
sudo pacman -S bluez bluez-utils blueman
```

#### 🟪 Ubuntu / Debian:

```bash
sudo apt update
sudo apt install bluez blueman
```

#### 🟥 Fedora:

```bash
sudo dnf install bluez blueman
```

> **Note:** Пакет `bluez` встановлює Bluetooth стек, а `blueman` — GUI-менеджер. У Ubuntu `bluez-utils` вбудовано в `bluez`.

---

### ⚙️ Step 2: Enable and Start Bluetooth Service

#### Arch / Fedora:

```bash
sudo systemctl enable bluetooth.service
sudo systemctl start bluetooth.service
```

#### Ubuntu / Debian:

Bluetooth-сервіс зазвичай увімкнений автоматично, але перевірити можна так:

```bash
sudo systemctl status bluetooth.service
```

---

### 📶 Step 3: Launch Blueman

Запусти Blueman Applet або Manager:

```bash
blueman-manager
```

> У GNOME Blueman може конфліктувати з `gnome-bluetooth`. Рекомендується використовувати Blueman в **XFCE, LXQt, Openbox, i3, Cinnamon, MATE**, або будь-якому іншому середовищі з tray-підтримкою.

---

### 🔒 Step 4: Unblock Bluetooth (If Needed)

```bash
rfkill list bluetooth
rfkill unblock bluetooth
```

---

### 🎧 Step 5: Connect to Bluetooth Audio Devices

#### For PulseAudio:

```bash
sudo apt install pulseaudio-module-bluetooth       # Ubuntu/Debian
sudo pacman -S pulseaudio-bluetooth                # Arch
sudo dnf install pulseaudio-module-bluetooth       # Fedora
```

Після встановлення **перезапусти PulseAudio**:

```bash
pulseaudio -k
```

#### For PipeWire users (newer systems):

```bash
# Ubuntu 22.10+, Fedora 34+, Arch
sudo apt install pipewire-audio                # Ubuntu
sudo pacman -S pipewire pipewire-pulse wireplumber   # Arch
sudo dnf install pipewire pipewire-pulseaudio        # Fedora
```

Перезапусти службу:

```bash
systemctl --user restart pipewire
```

---

### 🚀 Step 6: Autostart Blueman in Lightweight Environments

У WM, як i3, Openbox, LXQt, додай в автозапуск:

```bash
exec --no-startup-id blueman-applet &
```

Це дозволить запускати Blueman у треї при старті системи.

---

### 🧰 Step 7: Alternative CLI (Optional)

```bash
bluetoothctl
```

Всередині:

```
power on
agent on
default-agent
scan on
pair XX:XX:XX:XX:XX:XX
trust XX:XX:XX:XX:XX:XX
connect XX:XX:XX:XX:XX:XX
```

---

### 📚 Additional Resources

* Arch Wiki: [Bluetooth](https://wiki.archlinux.org/title/Bluetooth)
* Arch Wiki: [Blueman](https://wiki.archlinux.org/title/Blueman)
* Ubuntu Wiki: [Bluetooth](https://help.ubuntu.com/community/BluetoothSetup)
* Fedora Docs: [Bluetooth](https://docs.fedoraproject.org/en-US/quick-docs/bluetooth/)
* Man page: `man blueman-manager`
