# FastFood — Sistema de Pedidos (App de Escritorio)

Esta carpeta convierte tu web `fastfood-sistemaN.html` en una app de escritorio
real para **Windows** y **Mac**, usando [Electron](https://www.electronjs.org/).

No se tocó la lógica de tu sistema (login, menú, carrito, factura, panel admin,
inventario, ventas, usuarios): el archivo `index.html` es exactamente tu web
original, ahora cargada dentro de una ventana nativa con su propio ícono,
menú y acceso directo de escritorio.

> ⚠️ Importante: para compilar la app necesitas hacerlo en **tu propia
> computadora** con Node.js e internet (este entorno de chat no tiene acceso
> a internet, así que no puedo generar el `.exe`/`.dmg` directamente aquí).
> El proceso de compilar toma solo 2-3 comandos.

---

## 1. Requisitos

- [Node.js](https://nodejs.org/) (versión 18 o superior) instalado en tu PC/Mac.
- Conexión a internet (solo para instalar las dependencias la primera vez).

## 2. Probar la app (modo desarrollo)

Abre una terminal dentro de esta carpeta y ejecuta:

```bash
npm install
npm start
```

Esto abre la app en una ventana de escritorio, sin necesidad de empaquetarla.
Úsalo para verificar que todo funciona antes de generar el instalador.

## 3. Generar el instalador

### Windows (genera un instalador `.exe`)
```bash
npm run dist:win
```
> Puedes compilar el `.exe` desde Windows, o desde Mac/Linux (electron-builder
> soporta compilación cruzada para Windows).

### Mac (genera un `.dmg`)
```bash
npm run dist:mac
```
> El `.dmg` **debe compilarse en una Mac** (Apple no permite generar
> instaladores de Mac desde Windows/Linux).

### Ambos a la vez (desde Mac)
```bash
npm run dist
```

Los archivos finales quedan en la carpeta `dist/`.

## 4. Instalar

- **Windows**: ejecuta el `.exe` generado en `dist/` y sigue el asistente de
  instalación (crea acceso directo en escritorio y menú inicio).
- **Mac**: abre el `.dmg` y arrastra la app a la carpeta `Aplicaciones`.

---

## Estructura del proyecto

```
fastfood-app/
├── index.html       ← tu web original (sin cambios en su lógica)
├── main.js           ← proceso principal de Electron (crea la ventana, menú)
├── preload.js         ← puente seguro (listo para futuras integraciones nativas)
├── package.json       ← dependencias y configuración de empaquetado
└── build/
    └── icon.png        ← ícono de la app (1024×1024, puedes reemplazarlo)
```

## Notas

- **Los datos no se guardan entre sesiones**: igual que tu web original, el
  sistema (pedidos, inventario, usuarios) vive en memoria mientras la app
  está abierta. Si cierras la app, los datos se reinician. Si más adelante
  quieres que los pedidos/inventario se guarden en el disco del usuario
  (para no perderlos al cerrar), puedo agregar eso usando un archivo local
  o una base de datos SQLite — solo dímelo.
- **Ícono propio**: si quieres tu propio logo, reemplaza `build/icon.png`
  por una imagen cuadrada de al menos 512×512px (idealmente 1024×1024) y
  vuelve a compilar.
- **Imprimir facturas**: el menú "Archivo → Imprimir / Exportar factura"
  (o `Ctrl/Cmd+P`) abre el diálogo de impresión nativo del sistema operativo,
  igual que en el navegador.
- **Fuentes**: tu web usa fuentes de Google Fonts vía internet. Sin conexión,
  la app usará la fuente del sistema como respaldo (el diseño se ve casi
  igual). Si quieres que funcione 100% offline con la tipografía exacta,
  puedo incluir los archivos de fuente localmente.
