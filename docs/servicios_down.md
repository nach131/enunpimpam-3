Aquí te explico qué hace cada uno de los servicios que mencionas y cómo puedes desactivar permanentemente el servicio **Bluetooth**.

### **Explicación de cada servicio activo:**

1. **avahi-daemon.service**
   - **Descripción**: Este servicio gestiona el protocolo mDNS/DNS-SD (Multicast DNS/DNS Service Discovery), que se usa para permitir la detección automática de servicios en redes locales (como compartir impresoras, archivos, etc.).
   - **Propósito**: Hacer que dispositivos y servicios en la red local puedan encontrar otros dispositivos sin necesidad de configuración manual.

2. **bluetooth.service**
   - **Descripción**: Este servicio gestiona el soporte de Bluetooth en el sistema, permitiendo la conexión y comunicación con dispositivos Bluetooth como auriculares, teclados, ratones, etc.
   - **Propósito**: Proporcionar soporte para la tecnología Bluetooth en tu sistema.
   - **Acción para apagar**: Como solicitas, puedes desactivar este servicio.

3. **cron.service**
   - **Descripción**: Cron es un servicio que ejecuta tareas programadas en segundo plano. Permite que se ejecuten scripts o comandos a intervalos regulares.
   - **Propósito**: Programar tareas periódicas como copias de seguridad, actualizaciones automáticas, entre otras.

4. **dbus.service**
   - **Descripción**: D-Bus (intercomunicación entre procesos) es un sistema de mensajería que permite a las aplicaciones comunicarse entre sí.
   - **Propósito**: Facilitar la comunicación entre aplicaciones y servicios en el sistema.

5. **getty@tty1.service**
   - **Descripción**: Este servicio maneja las terminales virtuales (tty). Proporciona un login en la terminal cuando inicias sesión de forma física (por ejemplo, en el terminal de texto en modo consola).
   - **Propósito**: Permitir iniciar sesión en las terminales (tty) del sistema.

6. **ModemManager.service**
   - **Descripción**: Este servicio gestiona dispositivos de módems (típicamente módems USB o internos) y gestiona la conexión a redes móviles.
   - **Propósito**: Controlar dispositivos de módem y administrar conexiones móviles, como 3G/4G.

7. **NetworkManager.service**
   - **Descripción**: NetworkManager es una herramienta para gestionar conexiones de red en Linux, incluyendo redes Wi-Fi, Ethernet y VPN.
   - **Propósito**: Manejar las conexiones a internet, redes locales y conexiones VPN.

8. **nmbd.service**
   - **Descripción**: El servicio NMB (NetBIOS) de Samba gestiona el nombre NetBIOS y la localización de recursos compartidos en la red. Es parte de Samba.
   - **Propósito**: Permite que dispositivos en la red local encuentren máquinas y recursos compartidos, como impresoras o directorios.

9. **polkit.service**
   - **Descripción**: Polkit (PolicyKit) es un sistema que define políticas de autorización para controlar el acceso a ciertas acciones del sistema, como la instalación de paquetes o la administración de usuarios.
   - **Propósito**: Gestionar permisos y políticas de seguridad.

10. **smbd.service**
    - **Descripción**: El servicio SMB de Samba permite compartir archivos e impresoras entre sistemas Windows y Linux.
    - **Propósito**: Permitir el acceso a recursos compartidos desde sistemas Windows.

11. **ssh.service**
    - **Descripción**: El servicio SSH (Secure Shell) proporciona acceso remoto seguro a tu máquina.
    - **Propósito**: Permitir la administración remota de tu sistema de manera segura.

12. **systemd-journald.service**
    - **Descripción**: Este servicio gestiona el registro y almacenamiento de logs (registros del sistema) en tu sistema.
    - **Propósito**: Manejar los logs del sistema, que pueden ser útiles para depurar y hacer seguimiento de eventos.

13. **systemd-logind.service**
    - **Descripción**: Este servicio se encarga de la gestión de sesiones de usuario, como los inicios de sesión y cierres de sesión.
    - **Propósito**: Manejar las sesiones de usuarios, la creación de los espacios de usuario y el control de las políticas de energía (hibernación, suspensión, etc.).

14. **systemd-timesyncd.service**
    - **Descripción**: Este servicio sincroniza la hora del sistema con servidores NTP (Network Time Protocol).
    - **Propósito**: Mantener la hora del sistema sincronizada con los servidores de tiempo.

15. **systemd-udevd.service**
    - **Descripción**: Este servicio es responsable de la gestión de dispositivos. Detecta y maneja la conexión y desconexión de dispositivos hardware en el sistema.
    - **Propósito**: Gestionar dispositivos conectados (USB, discos duros, etc.).

16. **triggerhappy.service**
    - **Descripción**: Este servicio gestiona los eventos de teclas de acceso rápido o hotkeys, como las teclas de volumen, brillo, etc.
    - **Propósito**: Permitir la captura y el manejo de teclas de acceso rápido.

17. **user@1000.service**
    - **Descripción**: Este servicio se refiere a la sesión de usuario con UID 1000 (probablemente tu cuenta de usuario). 
    - **Propósito**: Manejar las sesiones de usuario, sus configuraciones y procesos.

18. **wpa_supplicant.service**
    - **Descripción**: Este servicio gestiona las conexiones Wi-Fi. Es responsable de la autenticación y conexión a redes Wi-Fi.
    - **Propósito**: Gestionar las conexiones inalámbricas.

---

### **Desactivar permanentemente el servicio Bluetooth**

Para **desactivar permanentemente** el servicio **Bluetooth** en tu sistema, puedes seguir estos pasos:

1. **Desactivar el servicio Bluetooth temporalmente**:
   Puedes detener el servicio para que no se inicie hasta el próximo reinicio con el siguiente comando:
   ```bash
   sudo systemctl stop bluetooth.service
   ```

2. **Deshabilitar el servicio Bluetooth permanentemente**:
   Para evitar que se inicie automáticamente al arrancar el sistema:
   ```bash
   sudo systemctl disable bluetooth.service
   ```

   Esto desactivará el servicio **Bluetooth** de manera permanente (no se iniciará al reiniciar el sistema).

3. **Verificar que el servicio esté deshabilitado**:
   Puedes confirmar que el servicio ha sido deshabilitado correctamente con:
   ```bash
   systemctl is-enabled bluetooth.service
   ```
   Si muestra **`disabled`**, el servicio está deshabilitado.

4. **Opcional: Impedir que el módulo Bluetooth se cargue en el arranque**:
   Si también deseas evitar que el módulo de hardware Bluetooth se cargue en el arranque, puedes agregar una regla para deshabilitarlo. Añade una línea al archivo de configuración de `modprobe`:
   ```bash
   echo "blacklist btusb" | sudo tee -a /etc/modprobe.d/blacklist.conf
   ```

Esto deshabilitará el soporte de Bluetooth en tu máquina tanto a nivel de servicio como a nivel de hardware.