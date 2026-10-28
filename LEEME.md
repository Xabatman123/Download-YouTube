# Descargar YouTube

Programa de escritorio para Windows con una interfaz basada en navegador que permite descargar audio y vídeo de YouTube, editar metadatos y gestionar subtítulos incrustados en vídeo.

## Funciones

- Descargar audio en MP3.
- Descargar vídeo en MP4 cuando existe un formato MP4 compatible.
- Guardar metadatos de origen y portada cuando el formato lo permite.
- Descargar por separado los subtítulos disponibles e intentar incrustarlos en el MP4 sin volver a codificar las pistas de audio/vídeo.
- Editar metadatos de MP3 y el texto de los subtítulos incrustados en MP4 (SRT/VTT).
- Abrir la interfaz en una ventana de aplicación de Microsoft Edge o Google Chrome cuando se detecta un navegador compatible.
- Guardar únicamente la preferencia del tema oscuro/claro.

La interfaz conserva los nombres: **«Descargar MP3»**, **«Descargar vídeo»** y **«Editar metadatos»**. La opción de añadir letras a los MP3 no está incluida.

## Estructura del proyecto

```text
Descargar Youtube/
├── Descargar Youtube.vbs
└── app/
    ├── launch_app.cmd
    ├── download_mp3.py
    ├── download_video.py
    ├── edit_metadata.py
    ├── gui_app.py
    ├── icon.ico
    ├── menu.py
    ├── prepare_portable.cmd
    └── ui/
        └── index.html
```

Durante el uso se crean las carpetas `Audios/` y `Videos/` en la raíz del proyecto. Las dependencias portables se instalan en `app/runtime/`.

## Requisitos

- Windows.
- Conexión a Internet para preparar el entorno portable por primera vez y descargar contenido.
- Se recomienda Microsoft Edge o Google Chrome. Si no se encuentran, el programa puede recurrir al navegador predeterminado.

El script `app/prepare_portable.cmd` descarga el Python portable configurado, las bibliotecas Python `yt-dlp`, Pillow y Mutagen, Deno y FFmpeg. Las versiones y las direcciones de descarga están definidas dentro de ese script.

## Instalación y primer inicio

1. Descarga o clona el repositorio completo. Mantén el lanzador de la raíz y la carpeta `app/` juntos.
2. Entra en `app/` y ejecuta **`prepare_portable.cmd`**. Espera a que termine y comprueba que las verificaciones finales sean correctas. Necesita conexión a Internet.
3. Vuelve a la raíz y ejecuta **` Descargar Youtube.vbs`**.
4. Utiliza las secciones de la interfaz en español para descargar audio/vídeo o editar metadatos y subtítulos incrustados.

**Importante:** `prepare_portable.cmd` elimina y vuelve a crear `app/runtime/`. No lo ejecutes mientras la aplicación esté abierta. No cambies el nombre de `app/` sin actualizar las rutas del lanzador VBS.

## Uso

### Descargar MP3

Introduce una o varias direcciones de YouTube y el nombre de salida, y comienza la descarga. Los archivos de audio se guardan en `Audios/`.

### Descargar vídeo

Introduce una o varias direcciones de YouTube y selecciona la calidad disponible. Los subtítulos se solicitan por separado y de forma no fatal: un fallo al descargar subtítulos no debería interrumpir una descarga de vídeo que ya se ha completado correctamente. Los vídeos se guardan en `Videos/`.

### Editar metadatos

Selecciona un archivo en el editor. Permite editar los campos de metadatos del MP3 y revisar o sustituir el texto de los subtítulos del MP4 mediante contenido SRT/VTT. La compatibilidad depende del archivo y de las capacidades de FFmpeg.

## Solución de problemas

- **El lanzador indica que falta preparar el programa:** ejecuta `app/prepare_portable.cmd` y espera a las comprobaciones finales.
- **La aplicación no se abre:** revisa `app/gui_app.log` si existe y comprueba que estén presentes Python, Deno y FFmpeg dentro de `app/runtime/`.
- **No aparece la ventana del navegador como aplicación:** instala o actualiza Microsoft Edge o Google Chrome.
- **No aparecen subtítulos:** puede que el vídeo de origen no ofrezca subtítulos, que la solicitud haya sido limitada o que el formato no se pueda incrustar. La incrustación de subtítulos es un intento que no debe invalidar la descarga principal.

## Desarrollo

- Punto de entrada de la interfaz: `app/gui_app.py`.
- Interfaz web: `app/ui/index.html`; se comunica con un servidor local que escucha en `127.0.0.1`.
- Preparación de dependencias: `app/prepare_portable.cmd`.
- Se mantienen los módulos de consola `download_mp3.py`, `download_video.py`, `edit_metadata.py` y `menu.py`, aunque la interfaz principal es la GUI.
- No subas al repositorio el entorno generado, los archivos multimedia descargados, los registros ni configuraciones personales. `.gitignore` excluye las rutas generadas habituales.

## Uso responsable

Utiliza el programa únicamente para contenido que tengas derecho a descargar y respeta las condiciones de YouTube, los derechos de autor y la legislación aplicable. El proyecto no concede derechos sobre el contenido descargado.

## Nota sobre vibe-coding y atribución

Este código se ha creado mediante **vibe-coding** (desarrollo iterativo asistido por IA). Es normal que no esté completamente optimizado, pulido ni estructurado como un proyecto de producción maduro. Eres libre de editarlo, reorganizarlo, mejorarlo u optimizarlo, siempre que des crédito al autor/proyecto original y enlaces este repositorio al redistribuirlo o publicar una versión derivada.
