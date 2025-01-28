Para verificar si tu interfaz de red `eth0` está operando a 100 Mbps o 1 Gbps, puedes utilizar diferentes métodos dependiendo de las herramientas instaladas en tu sistema Linux. A continuación, se presentan varias opciones:

---

### **1. Usar `ethtool`**
`ethtool` es una herramienta común para obtener información sobre interfaces de red.

1. Instala `ethtool` si no está instalado:
   ```bash
   sudo apt update
   sudo apt install ethtool
   ```

2. Consulta la velocidad de la interfaz `eth0`:
   ```bash
   sudo ethtool eth0
   ```

3. Busca la línea que dice `Speed:` en la salida, que mostrará algo como:
   ```
   Speed: 1000Mb/s
   ```

---

### **2. Usar `/sys/class/net`**
Si no tienes `ethtool`, puedes inspeccionar directamente los archivos del sistema.

1. Verifica la velocidad con:
   ```bash
   cat /sys/class/net/eth0/speed
   ```

2. El resultado será algo como:
   ```
   1000
   ```
   Esto indica que la interfaz está operando a 1000 Mbps (1 Gbps). Si muestra `100`, está funcionando a 100 Mbps.

---

### **3. Usar `nmcli` (NetworkManager)**
Si estás usando NetworkManager, puedes obtener información con `nmcli`.

1. Ejecuta el siguiente comando:
   ```bash
   nmcli device show eth0 | grep SPEED
   ```

2. Esto mostrará algo como:
   ```
   GENERAL.SPEED:               1000
   ```

---

### **4. Verificar con `dmesg`**
Puedes inspeccionar los mensajes del sistema para ver detalles sobre la conexión de la interfaz.

1. Usa `dmesg` para buscar información sobre `eth0`:
   ```bash
   dmesg | grep eth0
   ```

2. Busca una línea que mencione la velocidad negociada, como:
   ```
   eth0: Link is Up - 1000 Mbps Full Duplex
   ```

---

### **5. Usar `ip` o `ifconfig` (sin velocidad exacta)**
Aunque estos comandos no muestran directamente la velocidad, puedes usarlos para verificar que la interfaz está activa.

1. Con `ip`:
   ```bash
   ip link show eth0
   ```

2. Con `ifconfig`:
   ```bash
   ifconfig eth0
   ```

Estos comandos te dirán si la interfaz está "UP", pero no la velocidad exacta. Usa una de las opciones anteriores para eso.

---

### **Conclusión**
El método más completo y común es usar `ethtool`. Si no está disponible, puedes usar `/sys/class/net/eth0/speed` para obtener la velocidad exacta de la interfaz.