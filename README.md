<p align="center"><img src="./app/assets/images/SealCircle.png" width="150px" height="150px" alt="aventium softworks"></p>
<h1 align="center">Launcher</h1>
<em><h5 align="center">(anteriormente Electron Launcher)</h5></em>

[<p align="center"><img src="https://img.shields.io/github/actions/workflow/status/dscalzi/HeliosLauncher/build.yml?branch=master&style=for-the-badge" alt="gh actions">](https://github.com/dscalzi/HeliosLauncher/actions) [<img src="https://img.shields.io/github/downloads/dscalzi/HeliosLauncher/total.svg?style=for-the-badge" alt="downloads">](https://github.com/dscalzi/HeliosLauncher/releases) <img src="https://forthebadge.com/images/badges/winter-is-coming.svg"  height="28px" alt="winter-is-coming"></p>

<p align="center">Únete a servidores modificados sin preocuparte por instalar Java, Forge u otros mods. Nosotros nos encargamos de eso por ti.</p>

![Screenshot 1](https://i.imgur.com/6o7SmH6.png)

![Screenshot 2](https://i.imgur.com/x3B34n1.png)

## Características

* 🔒 Gestión completa de cuentas.
  * Agrega múltiples cuentas y cambia fácilmente entre ellas.
  * Autenticación de Microsoft (OAuth 2.0) y Mojang (Yggdrasil) totalmente compatible.
  * Las credenciales nunca se almacenan y se transmiten directamente a Mojang.
* 📂 Gestión eficiente de archivos.
  * Recibe actualizaciones del cliente tan pronto como las publicamos.
  * Los archivos se validan antes de iniciar. Los archivos corruptos o incorrectos se volverán a descargar.
* ☕ **Validación automática de Java.**
  * Si tienes una versión incompatible de Java instalada, instalaremos la correcta *por ti*.
  * No necesitas tener Java instalado para ejecutar el launcher.
* 📰 Feed de noticias integrado nativamente en el launcher.
* ⚙️ Gestión de configuración intuitiva, incluyendo un panel de control de Java.
* Compatible con todos nuestros servidores.
  * Cambia entre configuraciones de servidor con facilidad.
  * Consulta el número de jugadores del servidor seleccionado.
* Actualizaciones automáticas. Así es, el launcher se actualiza solo.
*  Consulta el estado de los servicios de Mojang.

Esta no es una lista exhaustiva. ¡Descarga e instala el launcher para conocer todo lo que puede hacer!

#### ¿Necesitas ayuda? [Consulta la wiki.][wiki]

#### ¿Te gusta el proyecto? ¡Deja una ⭐ en el repositorio!

## Descargas

Puedes descargarlo desde [GitHub Releases](https://github.com/dscalzi/HeliosLauncher/releases)

#### Última versión

[![](https://img.shields.io/github/release/dscalzi/HeliosLauncher.svg?style=flat-square)](https://github.com/dscalzi/HeliosLauncher/releases/latest)

#### Última versión preliminar

[![](https://img.shields.io/github/release/dscalzi/HeliosLauncher/all.svg?style=flat-square)](https://github.com/dscalzi/HeliosLauncher/releases)

**Plataformas compatibles**

Si descargas desde la pestaña [Releases](https://github.com/dscalzi/HeliosLauncher/releases), selecciona el instalador para tu sistema.

| Plataforma | Archivo |
| -------- | ---- |
| Windows x64 | `Helios-Launcher-setup-VERSION.exe` |
| macOS x64 | `Helios-Launcher-setup-VERSION-x64.dmg` |
| macOS arm64 | `Helios-Launcher-setup-VERSION-arm64.dmg` |
| Linux x64 | `Helios-Launcher-setup-VERSION.AppImage` |

## Consola

Para abrir la consola, usa el siguiente atajo de teclado.

```console
ctrl + shift + i
```

Asegúrate de tener seleccionada la pestaña de consola. No pegues nada en la consola a menos que estés 100% seguro de lo que hará. Pegar algo incorrecto puede exponer información sensible.

#### Exportar salida a un archivo

Si deseas exportar la salida de la consola, simplemente haz clic derecho en cualquier lugar de la consola y selecciona **Guardar como...**

![console example](https://i.imgur.com/T5e73jP.png)

## Desarrollo

Esta sección detalla la configuración de un entorno de desarrollo básico.

### Primeros pasos

**Requisitos del sistema**

* [Node.js][nodejs] v22

---

**Clonar e instalar dependencias**

```console
> git clone https://github.com/dscalzi/HeliosLauncher.git
> cd HeliosLauncher
> npm install
```

---

**Iniciar la aplicación**

```console
> npm start
```

---

**Compilar instaladores**

Para compilar para tu plataforma actual.

```console
> npm run dist
```

Compilar para una plataforma específica.

| Plataforma    | Comando              |
| ----------- | -------------------- |
| Windows x64 | `npm run dist:win`   |
| macOS       | `npm run dist:mac`   |
| Linux x64   | `npm run dist:linux` |

Las compilaciones para macOS pueden no funcionar en Windows/Linux y viceversa.

---

### Visual Studio Code

Todo el desarrollo del launcher debe realizarse usando [Visual Studio Code][vscode].

Pega lo siguiente en `.vscode/launch.json`

```JSON
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug Main Process",
      "type": "node",
      "request": "launch",
      "cwd": "${workspaceFolder}",
      "program": "${workspaceFolder}/node_modules/electron/cli.js",
      "args" : ["."],
      "outputCapture": "std"
    },
    {
      "name": "Debug Renderer Process",
      "type": "chrome",
      "request": "launch",
      "runtimeExecutable": "${workspaceFolder}/node_modules/.bin/electron",
      "windows": {
        "runtimeExecutable": "${workspaceFolder}/node_modules/.bin/electron.cmd"
      },
      "runtimeArgs": [
        "${workspaceFolder}/.",
        "--remote-debugging-port=9222"
      ],
      "webRoot": "${workspaceFolder}"
    }
  ]
}
```

Esto agrega dos configuraciones de depuración.

#### Depurar el proceso principal (Main Process)

Esto te permite depurar el [proceso principal][mainprocess] de Electron. Puedes depurar scripts en el [proceso de renderizado][rendererprocess] abriendo la ventana de DevTools.

#### Depurar el proceso de renderizado (Renderer Process)

Esto te permite depurar el [proceso de renderizado][rendererprocess] de Electron. Esto requiere instalar la extensión [Debugger for Chrome][chromedebugger].

Ten en cuenta que **no puedes** abrir la ventana de DevTools mientras usas esta configuración de depuración. Chromium solo permite un depurador; abrir otro hará que el programa se bloquee.

---

### Nota sobre el uso por terceros

Por favor, da crédito al autor original y proporciona un enlace a la fuente original. Este es software libre, por favor haz al menos esto.

Para instrucciones sobre cómo configurar la autenticación de Microsoft, consulta https://github.com/dscalzi/HeliosLauncher/blob/master/docs/MicrosoftAuth.md.

---

## Recursos

* [Wiki][wiki]
* [Nebula (crear Distribution.json)][nebula]
* [Rama de reescritura v2 (inactiva)][v2branch]

La mejor forma de contactar a los desarrolladores es en Discord.

[![discord](https://discordapp.com/api/guilds/211524927831015424/embed.png?style=banner3)][discord]

---

### Nos vemos en el juego.

[nodejs]: https://nodejs.org/en/ 'Node.js'
[vscode]: https://code.visualstudio.com/ 'Visual Studio Code'
[mainprocess]: https://electronjs.org/docs/tutorial/application-architecture#main-and-renderer-processes 'Main Process'
[rendererprocess]: https://electronjs.org/docs/tutorial/application-architecture#main-and-renderer-processes 'Renderer Process'
[chromedebugger]: https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome 'Debugger for Chrome'
[discord]: https://discord.gg/zNWUXdt 'Discord'
[wiki]: https://github.com/dscalzi/HeliosLauncher/wiki 'wiki'
[nebula]: https://github.com/dscalzi/Nebula 'dscalzi/Nebula'
[v2branch]: https://github.com/dscalzi/HeliosLauncher/tree/ts-refactor 'v2 branch'
