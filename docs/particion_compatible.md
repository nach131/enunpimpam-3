Para compartir un disco de 1 TB entre **Linux** y **macOS** de manera que ambos sistemas operativos puedan **leer y escribir** en él, debes elegir un formato de partición que sea compatible con ambos. Aquí te explico las opciones más comunes y recomendadas:

---

### 1. **exFAT**
- **Compatibilidad**:
  - **Linux**: Soporte nativo en la mayoría de distribuciones modernas (requiere el paquete `exfat-utils` o `exfat-fuse`).
  - **macOS**: Soporte nativo desde macOS 10.6.5 (Snow Leopard) en adelante.
  - **Windows**: Soporte nativo.
- **Ventajas**:
  - No tiene límites de tamaño de archivo ni de partición.
  - Es ligero y rápido.
  - Ideal para discos externos que se usarán en múltiples sistemas operativos.
- **Desventajas**:
  - No soporta permisos de archivos ni enlaces simbólicos (algo que no es crítico para discos de almacenamiento).
  - No es ideal para sistemas de arranque o uso interno.

**Recomendación**: **exFAT** es la mejor opción si solo necesitas compartir datos entre Linux y macOS.

---

### 2. **FAT32**
- **Compatibilidad**:
  - **Linux**: Soporte nativo.
  - **macOS**: Soporte nativo.
  - **Windows**: Soporte nativo.
- **Ventajas**:
  - Ampliamente compatible con casi todos los sistemas operativos.
- **Desventajas**:
  - Límite de 4 GB por archivo.
  - Límite de 2 TB por partición (aunque en la práctica, se recomienda usar solo hasta 1 TB).
  - No soporta permisos de archivos ni enlaces simbólicos.

**Recomendación**: Usa FAT32 solo si necesitas compatibilidad con dispositivos muy antiguos. Para un disco de 1 TB, **exFAT** es una mejor opción.

---

### 3. **HFS+ (macOS Extended)**
- **Compatibilidad**:
  - **macOS**: Soporte nativo (lectura y escritura).
  - **Linux**: Soporte de lectura y escritura con el paquete `hfsprogs` o `hfsutils`.
- **Ventajas**:
  - Soporta permisos de archivos y enlaces simbólicos.
  - Es el formato nativo de macOS.
- **Desventajas**:
  - No es ideal para Linux, ya que requiere software adicional.
  - No es compatible con Windows de forma nativa.

**Recomendación**: Usa HFS+ solo si trabajas principalmente en macOS y ocasionalmente en Linux.

---

### 4. **APFS (Apple File System)**
- **Compatibilidad**:
  - **macOS**: Soporte nativo (lectura y escritura).
  - **Linux**: Soporte limitado (solo lectura con herramientas como `apfs-fuse`).
- **Ventajas**:
  - Es el sistema de archivos moderno de macOS, optimizado para SSD.
  - Soporta características avanzadas como snapshots y cifrado.
- **Desventajas**:
  - No es compatible con Linux de forma nativa.
  - No es compatible con Windows.

**Recomendación**: No es una buena opción para compartir entre Linux y macOS.

---

### 5. **NTFS**
- **Compatibilidad**:
  - **Windows**: Soporte nativo (lectura y escritura).
  - **macOS**: Soporte de solo lectura nativo. Escritura requiere software adicional como `Paragon NTFS` o `Tuxera NTFS`.
  - **Linux**: Soporte de lectura y escritura con el paquete `ntfs-3g`.
- **Ventajas**:
  - Soporta archivos grandes y particiones grandes.
- **Desventajas**:
  - No es ideal para macOS sin software adicional.

**Recomendación**: No es la mejor opción para compartir entre Linux y macOS.

---

### 6. **Ext4 (con soporte en macOS)**
- **Compatibilidad**:
  - **Linux**: Soporte nativo (lectura y escritura).
  - **macOS**: Soporte de solo lectura nativo. Escritura requiere software adicional como `ext4fuse` o `Paragon ExtFS`.
- **Ventajas**:
  - Es el sistema de archivos predeterminado en muchas distribuciones de Linux.
  - Soporta archivos grandes y particiones grandes.
- **Desventajas**:
  - No es compatible con macOS de forma nativa.

**Recomendación**: No es ideal para compartir entre Linux y macOS.

---

### Resumen de opciones

| Formato  | Linux (R/W) | macOS (R/W) | Windows (R/W) | Límite de archivo | Límite de partición |
|----------|-------------|-------------|---------------|-------------------|---------------------|
| **exFAT** | Sí (con paquetes) | Sí | Sí | Sin límite | Sin límite |
| **FAT32** | Sí | Sí | Sí | 4 GB | 2 TB |
| **HFS+**  | Sí (con paquetes) | Sí | No (con software) | Sin límite | Sin límite |
| **APFS**  | No (solo lectura) | Sí | No | Sin límite | Sin límite |
| **NTFS**  | Sí (con paquetes) | Sí (con software) | Sí | Sin límite | Sin límite |
| **Ext4**  | Sí | Sí (con software) | No | Sin límite | Sin límite |

---

### Recomendación final
Para un disco de 1 TB que se usará entre **Linux** y **macOS**, la mejor opción es **exFAT**. Es compatible con ambos sistemas operativos, no tiene límites de tamaño de archivo y es fácil de configurar.

#### Pasos para formatear en exFAT:
1. **En macOS**:
   - Abre la aplicación "Utilidad de Discos".
   - Selecciona el disco y haz clic en "Borrar".
   - Elige el formato **exFAT** y dale un nombre.
   - Haz clic en "Borrar".

2. **En Linux**:
   - Instala el soporte para exFAT:
     ```bash
     sudo apt update
     sudo apt install exfat-utils
     ```
   - Usa `gparted` o `mkfs.exfat` para formatear el disco en exFAT.

¡Con esto tendrás un disco compatible para ambos sistemas! 😊Para particionar y formatear un disco en **exFAT** usando `fdisk` en Linux, sigue estos pasos. Te guiaré desde la identificación del disco hasta la creación de la partición y el formateo en exFAT.

---

### 1. **Identificar el disco**
Primero, identifica el disco que deseas particionar. Usa el comando `lsblk` o `fdisk -l` para listar los discos conectados:

```bash
lsblk
```

O:

```bash
sudo fdisk -l
```

Busca el nombre del disco (por ejemplo, `/dev/sdb`). Asegúrate de seleccionar el disco correcto, ya que **todos los datos se perderán** durante este proceso.

---

### 2. **Abrir `fdisk`**
Una vez identificado el disco, abre `fdisk` para comenzar a particionar:

```bash
sudo fdisk /dev/sdb
```

Reemplaza `/dev/sdb` con el nombre de tu disco.

---

### 3. **Crear una nueva tabla de particiones**
Si el disco no tiene una tabla de particiones o deseas eliminar las particiones existentes, sigue estos pasos:

1. Presiona `o` para crear una nueva tabla de particiones vacía (MBR).
   - Si prefieres usar GPT en lugar de MBR, presiona `g` en lugar de `o`.

2. Presiona `Enter` para confirmar.

---

### 4. **Crear una nueva partición**
Ahora crea una nueva partición:

1. Presiona `n` para crear una nueva partición.
2. Selecciona el tipo de partición:
   - `p` para una partición primaria.
   - `e` para una partición extendida (rara vez necesaria).
3. Elige el número de partición (por ejemplo, `1`).
4. Especifica el primer sector (presiona `Enter` para usar el valor predeterminado).
5. Especifica el último sector (presiona `Enter` para usar todo el espacio disponible).

---

### 5. **Cambiar el tipo de partición**
Por defecto, `fdisk` crea particiones con el tipo `Linux`. Para usar exFAT, cambia el tipo de partición:

1. Presiona `t` para cambiar el tipo de partición.
2. Selecciona la partición que acabas de crear (por ejemplo, `1`).
3. Introduce el código `7` para cambiar el tipo a `HPFS/NTFS/exFAT`.

---

### 6. **Guardar los cambios**
Guarda los cambios y sal de `fdisk`:

1. Presiona `w` para escribir los cambios en el disco.
2. Presiona `Enter` para confirmar.

---

### 7. **Formatear la partición en exFAT**
Ahora que has creado la partición, debes formatearla en exFAT. Para ello, usa el comando `mkfs.exfat`:

1. Instala `exfat-utils` si no lo tienes instalado:
   ```bash
   sudo apt update
   sudo apt install exfat-utils
   sudo apt install exfatprogs -y
   ```

2. Formatea la partición:
   ```bash
   sudo mkfs.exfat /dev/sdb1
   ```

   Reemplaza `/dev/sdb1` con el nombre de la partición que creaste.

---

### 8. **Verificar el formato**
Puedes verificar que la partición se ha formateado correctamente usando `lsblk` o `blkid`:

```bash
lsblk -f
```

O:

```bash
sudo blkid /dev/sdb1
```

Deberías ver algo como esto:

```
/dev/sdb1: UUID="XXXX-XXXX" TYPE="exfat"
```

---

### Resumen de comandos

1. Identificar el disco:
   ```bash
   lsblk
   ```

2. Abrir `fdisk`:
   ```bash
   sudo fdisk /dev/sdb
   ```

3. Crear una nueva tabla de particiones:
   - Presiona `o` (para MBR) o `g` (para GPT).

4. Crear una nueva partición:
   - Presiona `n`, luego sigue las instrucciones.

5. Cambiar el tipo de partición:
   - Presiona `t`, selecciona la partición y usa el código `7`.

6. Guardar los cambios:
   - Presiona `w`.

7. Formatear en exFAT:
   ```bash
   sudo mkfs.exfat /dev/sdb1
   ```

---

### Notas adicionales
- **Backup**: Asegúrate de hacer una copia de seguridad de los datos antes de particionar y formatear.
- **Montar la partición**: Después de formatear, puedes montar la partición en Linux usando:
  ```bash
  sudo mount /dev/sdb1 /mnt
  ```
  Reemplaza `/mnt` con el directorio de montaje que prefieras.

¡Y eso es todo! Ahora tienes un disco particionado y formateado en exFAT, listo para usar en Linux y macOS. 😊