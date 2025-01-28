Clonar un disco duro en Mac es útil si deseas hacer una copia exacta de tu disco, ya sea para reemplazarlo, respaldarlo o migrar tus datos a una nueva unidad. Aquí te explico los métodos más comunes:

---

## **Método 1: Clonar usando `diskutil`**

1. **Abre el Terminal**:
   - Ve a `Aplicaciones > Utilidades > Terminal`.

2. **Verifica las rutas de los discos**:
   - Usa este comando para identificar las rutas de los discos:
     ```bash
     diskutil list
     ```
   - Nota las rutas de tu disco de origen (por ejemplo, `/dev/disk2`) y de destino (por ejemplo, `/dev/disk3`).

3. **Ejecuta el comando de clonación**:
   ```bash
   sudo asr restore --source /dev/disk2 --target /dev/disk3 --erase
   ```
   - **`--source`**: Especifica el disco de origen.
   - **`--target`**: Especifica el disco de destino.
   - **`--erase`**: Borra los datos del disco de destino antes de copiar.

4. **Espera a que termine**:
   - El proceso puede tardar dependiendo del tamaño del disco.

---


## **Método 2: Clonar usando `diskutil`**
En lugar de usar `asr`, puedes usar el comando `diskutil` para clonar todo el disco, incluyendo particiones APFS.

1. **Desmonta las unidades**:
   - Asegúrate de desmontar las unidades antes de clonar:
     ```bash
     diskutil unmountDisk /dev/disk4
     diskutil unmountDisk /dev/disk6
     ```

2. **Usa `diskutil` para clonar**:
   Ejecuta este comando para clonar el disco físico completo:
   ```bash
   sudo diskutil partitionDisk /dev/disk6 1 GPTFormat APFS "Clonado" R
   sudo dd if=/dev/disk4 of=/dev/disk6 bs=1m
   ```
   - `if=/dev/disk4`: Especifica el disco de origen.
   - `of=/dev/disk6`: Especifica el disco de destino.
   - `bs=1m`: Define el tamaño del bloque para la copia, optimizando la velocidad.

3. **Espera a que termine**:
   - Este proceso puede tardar dependiendo del tamaño del disco.

---
