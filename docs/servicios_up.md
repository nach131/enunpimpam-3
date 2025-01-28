En Linux, puedes utilizar varios comandos para ver los servicios activos. Aquí tienes algunas formas comunes de hacerlo dependiendo del sistema de inicialización utilizado (principalmente **`systemd`**, que es el más común en distribuciones modernas):

---

### **1. Usando systemd**
Si tu sistema usa `systemd`, puedes usar los siguientes comandos:

#### **a) Mostrar todos los servicios activos**
```bash
systemctl list-units --type=service --state=running
```

Este comando mostrará una lista de los servicios que están actualmente activos y en ejecución.

#### **b) Ver todos los servicios (activos, inactivos, fallidos, etc.)**
```bash
systemctl list-units --type=service
```

Esto incluirá todos los servicios, independientemente de su estado.

#### **c) Filtrar un servicio específico**
Si deseas verificar el estado de un servicio específico (por ejemplo, `ssh`):
```bash
systemctl status ssh
```

#### **d) Servicios habilitados para iniciar al arranque**
Para listar los servicios configurados para iniciarse automáticamente en el arranque:
```bash
systemctl list-unit-files --type=service --state=enabled
```

---

### **2. Usando `service` (sistemas más antiguos o compatibilidad)**
Algunas distribuciones aún soportan el comando `service`:
```bash
service --status-all
```

Este comando mostrará una lista de servicios con un símbolo al lado:
- `[ + ]`: Activo.
- `[ - ]`: Inactivo.
- `[ ? ]`: Estado desconocido.

---

### **3. Verificar con `ps` o `top`**
Si quieres ver qué procesos están ejecutándose (incluidos servicios), puedes usar comandos como:

#### **a) Listar procesos en ejecución**
```bash
ps aux
```
Esto muestra todos los procesos activos en el sistema.

#### **b) Usar `htop`**
Si tienes `htop` instalado, puedes usarlo para navegar fácilmente entre los procesos:
```bash
htop
```

#### **c) Buscar un servicio específico**
Por ejemplo, para buscar si `nginx` está corriendo:
```bash
ps aux | grep nginx
```

---

### **4. Ver registros del sistema**
A veces, los registros del sistema contienen información sobre los servicios que están activos. Puedes usar:
```bash
journalctl -xe
```

---

### **5. Alternativa con `chkconfig` (sistemas más antiguos)**
En distribuciones más antiguas como **CentOS 6** o sistemas basados en SysVinit, puedes usar:
```bash
chkconfig --list
```

---

### Resumen rápido
El comando más común y útil en sistemas modernos:
```bash
systemctl list-units --type=service --state=running
```

Esto te dará una visión clara de los servicios activos en tu sistema. Si necesitas más ayuda, ¡puedes preguntarme! 😊