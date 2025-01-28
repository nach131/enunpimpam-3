Para listar ficheros en un directorio ordenados por fecha en Linux usando el comando `ls`, puedes usar la opción `-lt` o `-ltr` (dependiendo si deseas el orden ascendente o descendente). Si te refieres a un sistema específico como **Hyp** o alguna configuración particular, podemos ajustarlo.

### Comandos básicos para listar por fecha:
1. **Orden descendente por fecha (más recientes primero):**
   ```bash
   ls -lt
   ```
   - `-l`: Muestra los detalles de los archivos.
   - `-t`: Ordena por fecha de modificación (los más recientes primero).

2. **Orden ascendente por fecha (más antiguos primero):**
   ```bash
   ls -ltr
   ```
   - `-r`: Invierte el orden (más antiguos primero).

3. **Incluir subdirectorios:**
   Si necesitas incluir archivos en subdirectorios también:
   ```bash
   ls -ltR
   ```
   - `-R`: Lista de forma recursiva.

4. **Mostrar fechas completas y ficheros ocultos:**
   Si quieres más detalles, como fechas completas y archivos ocultos:
   ```bash
   ls -lthA
   ```
   - `-h`: Tamaños legibles (human-readable).
   - `-A`: Muestra archivos ocultos (excepto `.` y `..`).

---

### Ejemplo con directorios específicos:
Si quieres listar ficheros en un directorio llamado `hyp`, navega al directorio y ejecuta el comando:

```bash
cd hyp
ls -lt
```

O puedes especificar el directorio directamente:

```bash
ls -lt /ruta/a/hyp
```

---

Si necesitas algo más avanzado, como buscar archivos creados en fechas específicas o procesar logs, házmelo saber. 😊