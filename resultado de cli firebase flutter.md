Para trabajar con Firebase CLI en tu proyecto Flutter, esta guía te llevará paso a paso. Primero, asegurémonos de que tienes las herramientas base necesarias.

### ⚙️ Software Necesario para Windows

Antes de empezar, confirma que tu sistema cumple con los requisitos fundamentales para ejecutar las herramientas de línea de comandos (CLI).

*   **Node.js y npm**: Necesarios para ejecutar JavaScript fuera del navegador y para gestionar paquetes de código.
*   **Firebase CLI**: La herramienta principal que te permite interactuar con los servicios de Firebase desde la terminal.
*   **FlutterFire CLI**: Un complemento específico para proyectos Flutter que simplifica la configuración de Firebase.

### ✅ Paso 1: Verificar e Instalar Node.js y npm

Node.js incluye `npm`, su gestor de paquetes oficial. Primero verificaremos si ya los tienes y, si no, te guiaré en la instalación.

#### Cómo Verificar si Node.js y npm Están Instalados

Abre el **Símbolo del sistema (CMD) o PowerShell** y ejecuta estos comandos para ver las versiones instaladas:

*   Para **Node.js**: `node -v`
*   Para **npm**: `npm -v`

Si los comandos devuelven un número de versión (p. ej., `v20.10.0`, `10.2.3`), ya están instalados. Si aparece un error, continúa con la instalación paso a paso. Recuerda que se requiere **Node.js v16.13.0 o posterior**.

#### Instalación Paso a Paso de Node.js en Windows

1.  **Descargar el instalador**: Ve al sitio oficial de Node.js. Se recomienda la versión **LTS (Long-Term Support)** por ser la más estable.
2.  **Ejecutar el instalador**: Abre el archivo `.msi` descargado y sigue los pasos del asistente. La configuración por defecto suele ser adecuada. Como buena práctica, instálalo en una ruta como `C:\Program Files\nodejs`.
3.  **Verificar de nuevo**: Una vez finalizado, abre una **nueva ventana** del Símbolo del sistema o PowerShell y repite los comandos `node -v` y `npm -v` para confirmar que la instalación fue exitosa.

### 🚀 Paso 2: Instalar Firebase CLI de Manera Global

Con Node.js listo, puedes instalar la herramienta de Firebase.

1.  Abre una terminal (Símbolo del sistema o PowerShell) como **Administrador**. Esto es importante para que la instalación tenga los permisos necesarios.
2.  Ejecuta el comando de instalación global:
    ```bash
    npm install -g firebase-tools
    ```
    El flag `-g` indica que se instalará de manera global en tu sistema, accesible desde cualquier proyecto.
3.  Para verificar la instalación, comprueba la versión de Firebase CLI con:
    ```bash
    firebase --version
    ```
    Si el comando no se reconoce, cierra y vuelve a abrir la terminal para que el sistema actualice las rutas de las variables de entorno.

### 💻 Paso 3: Usar los Comandos de Firebase Tools

Una vez instalada la CLI, estos son los comandos más importantes.

#### 1. Acceder a Firebase con tu Cuenta de Google

Para conectar la terminal con tu proyecto en la nube, necesitas autenticarte:

*   **Comando de inicio de sesión**: Ejecuta `firebase login`. Se abrirá una ventana de tu navegador para que elijas la cuenta de Google asociada a Firebase y otorgues los permisos.

*   **Otros comandos de autenticación útiles**:
    *   Para ver qué cuenta está activa: `firebase login:list`.
    *   Para agregar una cuenta adicional: `firebase login:add`.
    *   Para cerrar sesión: `firebase logout`.

#### 2. Instalar y Usar FlutterFire CLI

Esta herramienta complementaria facilita la conexión de tu proyecto Flutter con Firebase.

*   **Instalación**: Ejecuta `dart pub global activate flutterfire_cli`. Durante la instalación, es posible que veas una advertencia sobre una ruta que no está en el `PATH` de Windows. Es fundamental que **copies esa ruta** para el siguiente paso.
*   **Configurar la variable de entorno `PATH` (importante)**:
    1.  Busca "Editar variables de entorno del sistema" en el menú de inicio de Windows.
    2.  Haz clic en "Variables de entorno...".
    3.  En la sección "Variables del sistema", busca la variable `Path` y edítala.
    4.  Añade la ruta completa que copiaste en el paso anterior (similar a `C:\Users\TuUsuario\AppData\Local\Pub\Cache\bin`).
    5.  Guarda los cambios y **reinicia la terminal** para aplicar la modificación.
*   **Configurar tu proyecto Flutter**: Navega en la terminal hasta la carpeta raíz de tu proyecto y ejecuta `flutterfire configure`. Este comando te guiará para seleccionar tu proyecto y las plataformas (Android, iOS) que usará, generando automáticamente la configuración en tu app.

Para gestionar tus proyectos, puedes usar `firebase projects:list`, que te mostrará un listado de todos los proyectos asociados a tu cuenta de Google.

Espero que esta guía te sea de gran ayuda. Si tienes alguna otra duda en el camino, aquí estoy para ayudarte.
