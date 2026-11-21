# App Propóleo

App web con las recetas, calculadoras y bitácora del *Manual de elaboración de propóleo*.
Está hecha con HTML, CSS y JavaScript puros, sin librerías ni conexión a internet, para poder
convertirla después en app de Android o iOS sin reescribirla.

## Qué contiene

| Archivo | Para qué sirve |
| --- | --- |
| `index.html` | Toda la app: recetas 1 a 7, calculadoras, bitácora y guía |
| `manifest.webmanifest` | Nombre, colores e ícono para instalarla en el celular |
| `sw.js` | Guarda la app para que funcione sin conexión |
| `icon.svg` | Ícono de la app |

**Secciones:**

- **Recetas:** las 7 recetas del manual. Cada una trae su calculadora: escribes cuánto quieres
  hacer y te da las cantidades.
- **Calculadoras:** impurezas de limpieza, porcentaje de extracto seco, dilución de alcohol
  a cualquier graduación y calculadora de sosa para jabón en frío (varios aceites, índice editable,
  margen de grasa, agua y propóleo, con alertas de seguridad).
- **Bitácora:** un registro por lote, con cálculos automáticos (impurezas, alcohol, hora de
  filtrado) y exportación a CSV para Excel.
- **Guía:** resumen de la NOM-003-SAG/GAN-2017, precauciones, etiquetado, laboratorio y fuentes.

Los datos (bitácora y últimos valores de las calculadoras) se guardan solo en el dispositivo.

## Cómo probarla

- **En la computadora:** abre `index.html` con doble clic. Funciona todo excepto el modo sin
  conexión, que necesita un servidor.
- **Con servidor local:** desde la carpeta que contiene `app-propoleo`, ejecuta
  `python -m http.server 8765 --directory app-propoleo` y abre `http://localhost:8765`.

## Cómo llevarla al celular

### Opción 1. Instalarla como app web (la más rápida, sin tiendas)

1. Sube la carpeta `app-propoleo` a un hosting con HTTPS (por ejemplo GitHub Pages o Netlify).
2. Abre la dirección en el celular.
   - **Android (Chrome):** menú ⋮ › *Instalar app* o *Agregar a pantalla principal*.
   - **iPhone (Safari):** botón Compartir › *Agregar a inicio*.
3. Queda con ícono propio y funciona sin conexión.

### Opción 2. App nativa para Play Store y App Store (con Capacitor)

[Capacitor](https://capacitorjs.com) envuelve esta misma carpeta en una app de Android y de iOS.
Necesitas Node.js; para Android, Android Studio; para iOS, una Mac con Xcode.

```
npm init -y
npm install @capacitor/core @capacitor/cli @capacitor/android @capacitor/ios
npx cap init Propoleo mx.tudominio.propoleo --web-dir app-propoleo
npx cap add android
npx cap add ios
npx cap open android
```

Cada vez que cambies la app, ejecuta `npx cap copy` antes de compilar.

**Pendientes antes de publicar en tiendas:**

- Íconos PNG (192, 512 y 1024 px) generados a partir de `icon.svg`.
- La exportación a CSV usa una descarga del navegador; dentro de la app nativa conviene
  cambiarla por los complementos *Filesystem* y *Share* de Capacitor.
- Cuentas de desarrollador de Google Play y de Apple.
