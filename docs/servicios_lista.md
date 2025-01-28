Para desactivar o "bloquear" servicios relacionados con dispositivos y funcionalidades específicas en Linux (como **Bluetooth**, **Wi-Fi**, **Redes**, etc.), se utilizan módulos o servicios correspondientes. El módulo **`btusb`** es para el soporte de Bluetooth, pero cada servicio o funcionalidad tiene su propio módulo o nombre de servicio.


### **1. Bluetooth**
- **Servicio**: `bluetooth.service`
- **Módulo del kernel**: `btusb`
- **Desactivación del servicio**: 
  ```bash
  sudo systemctl stop bluetooth.service
  sudo systemctl disable bluetooth.service
  ```
- **Desactivación del módulo**:
  ```bash
  echo "blacklist btusb" | sudo tee -a /etc/modprobe.d/blacklist.conf
  ```

---

### **2. Wi-Fi**
- **Servicio**: `wpa_supplicant.service` (gestiona las conexiones Wi-Fi)
- **Módulo del kernel**: El módulo depende del chip de Wi-Fi que uses. Algunos de los módulos comunes incluyen:
  - `iwlwifi` (para tarjetas Intel)
  - `brcmsmac` (para Broadcom)
  - `ath9k` (para Atheros)
- **Desactivación del servicio**:
  ```bash
  sudo systemctl stop wpa_supplicant.service
  sudo systemctl disable wpa_supplicant.service
  ```
- **Desactivación del módulo**:
  ```bash
  echo "blacklist iwlwifi" | sudo tee -a /etc/modprobe.d/blacklist.conf  # Para tarjetas Intel
  echo "blacklist brcmsmac" | sudo tee -a /etc/modprobe.d/blacklist.conf  # Para Broadcom
  echo "blacklist ath9k" | sudo tee -a /etc/modprobe.d/blacklist.conf  # Para Atheros
  ```

---

### **3. Red Ethernet (Cableada)**
Si quieres bloquear el acceso de red por **Ethernet**, puedes hacerlo desactivando el servicio **NetworkManager** o configurando una red manualmente.

- **Servicio**: `NetworkManager.service`
- **Módulo del kernel**: No existe un módulo específico para Ethernet como en el caso de Wi-Fi, ya que las interfaces Ethernet suelen ser gestionadas automáticamente por **NetworkManager**.
- **Desactivación del servicio**:
  ```bash
  sudo systemctl stop NetworkManager.service
  sudo systemctl disable NetworkManager.service
  ```

- **Desactivación de la interfaz Ethernet**:
  Si solo deseas desactivar una interfaz Ethernet en particular (por ejemplo `eth0`), puedes usar:
  ```bash
  sudo ip link set eth0 down
  ```

---

### **4. Modem/Red Móvil (3G/4G)**
El servicio **ModemManager** gestiona las conexiones móviles.

- **Servicio**: `ModemManager.service`
- **Módulo del kernel**: Depende del dispositivo, pero generalmente el módulo utilizado para las conexiones móviles es **`cdc_acm`** para módems USB.
- **Desactivación del servicio**:
  ```bash
  sudo systemctl stop ModemManager.service
  sudo systemctl disable ModemManager.service
  ```
- **Desactivación del módulo**:
  ```bash
  echo "blacklist cdc_acm" | sudo tee -a /etc/modprobe.d/blacklist.conf
  ```

---

### **5. Samba (Red de Archivos Windows)**
Si quieres bloquear el acceso a las redes de archivos de Windows (SMB/CIFS), puedes desactivar los servicios **`smbd`** y **`nmbd`**.

- **Servicio**: 
  - `smbd.service` (gestiona las conexiones SMB)
  - `nmbd.service` (gestiona la resolución de nombres NetBIOS)
- **Desactivación del servicio**:
  ```bash
  sudo systemctl stop smbd.service
  sudo systemctl stop nmbd.service
  sudo systemctl disable smbd.service
  sudo systemctl disable nmbd.service
  ```

---

### **6. Printer (Cups)**
Si no deseas usar impresoras, puedes desactivar el servicio **CUPS**.

- **Servicio**: `cups.service`
- **Desactivación del servicio**:
  ```bash
  sudo systemctl stop cups.service
  sudo systemctl disable cups.service
  ```

---

### **7. Avahi (mDNS/DNS-SD)**
Si no necesitas la detección automática de servicios en la red local (como impresoras, compartición de archivos, etc.), puedes desactivar **avahi-daemon**.

- **Servicio**: `avahi-daemon.service`
- **Desactivación del servicio**:
  ```bash
  sudo systemctl stop avahi-daemon.service
  sudo systemctl disable avahi-daemon.service
  ```

---

### **8. Firewall (ufw)**
Si deseas bloquear el firewall (aunque no es recomendable dejarlo desactivado por razones de seguridad), puedes desactivar **ufw** (Uncomplicated Firewall).

- **Servicio**: `ufw.service`
- **Desactivación del servicio**:
  ```bash
  sudo systemctl stop ufw.service
  sudo systemctl disable ufw.service
  ```

---

### **¿Cómo conseguir el nombre de otros módulos?**

1. **Listar los módulos cargados**:
   Puedes ver todos los módulos cargados actualmente con el siguiente comando:
   ```bash
   lsmod
   ```

2. **Ver los módulos disponibles**:
   También puedes ver una lista de módulos disponibles en tu sistema:
   ```bash
   modprobe -l
   ```

3. **Buscar el nombre del módulo de un dispositivo**:
   Si quieres saber qué módulo está siendo utilizado por un dispositivo, puedes usar el comando `lspci` (para dispositivos PCI) o `lsusb` (para dispositivos USB).
   ```bash
   lspci | grep -i wireless
   lsusb
   ```

---

### **Conclusión**
Para desactivar un servicio o módulo en Linux, puedes usar:
- **`systemctl`** para desactivar servicios.
- **`modprobe`** o **`blacklist`** para desactivar módulos del kernel.

Cada servicio o módulo tiene su propio nombre, y puedes encontrar esta información usando comandos como `systemctl`, `lsmod`, `lspci`, y `lsusb`.