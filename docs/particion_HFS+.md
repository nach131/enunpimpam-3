Para crear un disco de 1 TB que sea compatible con macOS utilizando `fdisk`, necesitas configurarlo con el esquema de partición correcto y un sistema de archivos compatible. macOS utiliza principalmente el sistema de archivos **APFS** o **HFS+ (Mac OS Extended)** y el esquema de partición **GPT (GUID Partition Table)**.

Sin embargo, **`fdisk` no es ideal para gestionar particiones GPT**, ya que está diseñado para MBR. Para GPT, es mejor usar `parted` o `gptfdisk` (`gdisk`) en lugar de `fdisk`. Dicho esto, aquí están los pasos usando `fdisk` y una mejor alternativa con `parted`.

---

### **1. Verificar el disco disponible**
Antes de crear las particiones, identifica el disco en el que quieres trabajar:

```bash
sudo fdisk -l
```

Busca el disco de 1 TB (por ejemplo, `/dev/sdX`). **Asegúrate de que el disco seleccionado es el correcto**, ya que todos los datos en él serán eliminados.

---

### **2. Crear particiones con `fdisk` (MBR, no recomendado para macOS)**
Si necesitas usar `fdisk` y no puedes usar `parted`, sigue estos pasos:

1. Inicia `fdisk`:
   ```bash
   sudo fdisk /dev/sdX
   ```
   Reemplaza `/dev/sdX` con el disco correcto.

2. Elimina todas las particiones existentes (opcional, si hay particiones previas):
   - Presiona `d` para borrar particiones. Repite hasta que todas estén eliminadas.

3. Crea una nueva partición primaria:
   - Presiona `n` para crear una partición.
   - Elige `p` (partición primaria).
   - Presiona `Enter` para usar el número de partición predeterminado.
   - Presiona `Enter` para aceptar el primer sector predeterminado.
   - Presiona `Enter` para aceptar el último sector (usar todo el espacio).

4. Cambia el tipo de partición:
   - Presiona `t` para cambiar el tipo.
   - Escribe `af` para seleccionar el código de HFS+ (Apple HFS).

5. Guarda los cambios y sal:
   - Presiona `w` para escribir los cambios y salir.

6. Formatea la partición con HFS+:
   ```bash
   sudo mkfs.hfsplus /dev/sdX1
   ```
   Esto crea un sistema de archivos compatible con macOS (HFS+).

---

### **3. Usar `parted` para GPT y APFS/HFS+ (recomendado)**
Para compatibilidad completa con macOS (GPT y APFS/HFS+):

1. Inicia `parted`:
   ```bash
   sudo parted /dev/sdX
   ```

2. Configura el disco con el esquema GPT:
   ```bash
   mklabel gpt
   ```

3. Crea una partición que ocupe todo el espacio:
   ```bash
   mkpart primary hfs+ 0% 100%
   ```

4. Verifica los cambios:
   ```bash
   print
   ```

5. Sal de `parted`:
   ```bash
   quit
   ```

6. Formatea la partición con HFS+:
   ```bash
   sudo mkfs.hfsplus /dev/sdX1
   ```

   Si deseas usar APFS (más moderno), esto deberá hacerse desde macOS.

---

### **4. Alternativa para formatear con APFS desde macOS**
Si planeas usar APFS, debes formatear el disco desde macOS:

1. Conecta el disco a una Mac.
2. Abre **Utilidad de Discos** (Disk Utility).
3. Selecciona el disco y haz clic en **Borrar**.
4. Configura:
   - **Formato**: APFS o Mac OS Extended (HFS+).
   - **Esquema**: GUID Partition Map (GPT).
5. Haz clic en **Borrar**.

---

### **Notas importantes**
- HFS+ es compatible con versiones anteriores de macOS y Windows (con software adicional).
- APFS es moderno, pero solo funciona con macOS 10.13 (High Sierra) o posterior.
- Usa GPT si el disco será usado exclusivamente con macOS. Para compatibilidad con sistemas antiguos o BIOS, usa MBR.


### **Instalar hfsprops**

```bash
   sudo apt install hfsprogs -y
```