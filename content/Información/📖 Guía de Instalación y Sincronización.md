Link Bodega:
https://drive.google.com/drive/folders/10ORM7XbxackULU4HBVB_mT3Ebnm7zIUG

Obsidian:
https://play.google.com/store/apps/details?id=md.obsidian

Drive sync:
https://play.google.com/store/apps/details?id=com.ttxapps.drivesync

Sigue estos pasos en orden para dejar listo el cancionero en tu celular.

---

### Paso 1: Agregar la carpeta compartida a tu Drive
1. Abre el **primer enlace** que se te compartió desde el correo que vas a utilizar.
   > **Nota:** Se recomienda tener al menos **10 MB libres** tanto en la memoria del teléfono como en el almacenamiento del correo.
2. Al abrir el enlace, la carpeta se agregará automáticamente a la sección **"Compartidos conmigo"** de tu Google Drive.

---

### Paso 2: Crear la bodega en Obsidian
1. Abre **Obsidian** y otorga todos los permisos que la aplicación solicite.
2. Selecciona **Crear nueva bodega** (*Create new vault*).
3. Escribe exactamente el nombre: `Material Iglesia` *(respeta las mayúsculas y minúsculas)*.
4. Cuando pregunte dónde guardarla en el dispositivo:
   * Navega a la carpeta **Documentos** o **Docs** (el nombre varía según la marca del teléfono).
   * Selecciona esa carpeta y confirma guardar allí.

---

### Paso 3: Iniciar sesión en Drive Sync / FolderSync
1. Abre la aplicación **Drive Sync** (o FolderSync).
2. Inicia sesión con el **mismo correo** que usaste en el Paso 1.
   > **¿Se queda cargando?** Si la app se queda en blanco al poner el correo, abre la pantalla de aplicaciones recientes de tu teléfono, cierra Drive Sync, limpia la memoria caché/apps recientes, vuelve a entrar e intenta de nuevo.

---

### Paso 4: Configurar la sincronización
En Drive Sync, ve a **Carpetas sincronizadas** y añade una nueva sincronización con estos datos:

* **Nombre:** *(Puedes dejar el que viene por defecto o poner `Material Iglesia`)*.
* **Carpeta remota (Google Drive):** Entra a `Compartidos conmigo` (o carpetas compartidas) y selecciona la carpeta **Material Iglesia**.
* **Carpeta local (Teléfono):** Selecciona `Almacenamiento interno` → `Documents` → `Material Iglesia`.
* **Método de sincronización:** Selecciona **Bajar en espejo** (*To local only / Mirror*).
* **⚙️ Ajuste especial de archivos ocultos:**
  1. Desmarca la casilla **"Excluir archivos ocultos"** para esta primera vez.
  2. Deja todo lo demás como está por defecto y presiona **Guardar**.
  3. Presiona **Sincronizar** y espera a que termine de descargar todos los archivos.
  4. **Importante:** Una vez terminada la primera descarga, vuelve a la configuración de la carpeta en Drive Sync y **vuelve a marcar** la casilla *"Excluir archivos ocultos"*.

---

### Paso 5: Activar en Obsidian
1. Regresa a la app de **Obsidian**.
2. Espera unos segundos a que la aplicación indexe y reconozca todos los archivos.
3. Cuando aparezca un aviso sobre **Plugins de la comunidad**, selecciona la opción **"Confiar en el autor de la bodega"** (*Trust author and enable plugins*).

¡Listo! Ya tienes el cancionero configurado y listo para usar.

### Paso 6: Configurar la sincronización automática
Para que las canciones se actualicen solas en el teléfono sin que tengas que abrir la aplicación manualmente:

1. En la pantalla principal de **Drive Sync**, arriba a la derecha (al lado del botón de sincronizar), presiona el **ícono de los 3 puntos**.
2. Entra en **Ajustes**.
3. Toca la opción de **Batería** y otorga los permisos necesarios para que la app pueda ejecutarse en segundo plano y actualizar los archivos.
4. Vuelve atrás y entra a **Ajustes** $\rightarrow$ **Sincronización**.
5. Busca y ajusta las siguientes opciones:
   * **Número máximo de intentos:** Ponlo en **5** (esto da un margen de reintento en caso de algún fallo puntual de internet).
   * **Activar sincronización automática:** Déjalo **encendido**.
   * **Programación automática:** 
     * Selecciona **Establecer programación personalizada**.
     * Marca **todos los días** (o los días que estimes conveniente).
     * Elige una hora para la sincronización (las horas de la madrugada, **entre 2:00 y 5:00**, son las óptimas).
     * Presiona **OK**.
   * **El nivel de batería debe ser al menos:** Ajústalo a **15%**.