# Rewiro · Hackea tu cerebro

App para dejar de fumar: cronómetro desde tu fecha de corte, botón **SOS** para antojos (respiración guiada de 5 minutos), cajetilla que no compraste, dinero ahorrado, premios, patrones de antojo y plan "si pasa esto, hago esto".

Todo funciona sin internet y los datos se guardan solo en el teléfono.

## Estructura

```
rewiro/
├── www/                  ← la app (HTML, fuentes, íconos). Aquí se edita.
├── ios/                  ← proyecto de Xcode ya generado (Capacitor 8)
├── assets/               ← ícono 1024 y splash, para regenerar los de iOS
├── capacitor.config.json ← nombre de la app e identificador (mx.moni.rewiro)
├── package.json
└── PRIVACY.md            ← política de privacidad (App Store la pide)
```

## 1 · Subir a GitHub

1. En github.com → **New repository** → nombre `rewiro` → *Create* (sin README, ya viene uno).
2. En la terminal, dentro de esta carpeta:

```bash
git init
git add .
git commit -m "Rewiro 1.0"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/rewiro.git
git push -u origin main
```

> Sin terminal: en el repositorio vacío usa **uploading an existing file** y arrastra todo el contenido de la carpeta (no la carpeta `node_modules`, que de todos modos no viene incluida).

## 2 · Probarla en la computadora

```bash
npx --yes serve www
```
Abre la dirección que aparece (por ejemplo `http://localhost:3000`) con el navegador en vista de teléfono.

## 3 · Llevarla a la App Store

Necesitas: una **Mac con Xcode** (gratis en la Mac App Store), **Node 22 o más reciente** y una cuenta de **Apple Developer Program** (USD 99 al año, developer.apple.com).

```bash
git clone https://github.com/TU-USUARIO/rewiro.git
cd rewiro
npm install
npx cap sync ios
npx cap open ios
```

En Xcode:
1. Selecciona el proyecto **App** → pestaña **Signing & Capabilities** → en *Team* elige tu cuenta de desarrollador.
2. Si Apple dice que `mx.moni.rewiro` ya está ocupado, cámbialo en *Bundle Identifier* y en `capacitor.config.json` (por ejemplo `com.tunombre.rewiro`).
3. Arriba, como destino, elige **Any iOS Device (arm64)**.
4. Menú **Product → Archive**. Al terminar, en el Organizer: **Distribute App → App Store Connect → Upload**.

En [App Store Connect](https://appstoreconnect.apple.com):
1. **Apps → + → Nueva app**: nombre "Rewiro", idioma Español (México), el mismo Bundle ID.
2. Llena la ficha: descripción, palabras clave, categoría **Salud y forma física**, capturas de pantalla de iPhone (6.9" o 6.5").
3. **Privacidad de la app** → "No recopilamos datos". Pega la URL pública de `PRIVACY.md` (en GitHub: abre el archivo y copia la dirección).
4. Elige la compilación que subiste desde Xcode → **Enviar a revisión**.

Se puede probar antes en tu iPhone con **TestFlight** (aparece en App Store Connect cuando la compilación termina de procesarse).

## Cambiar algo de la app

Edita `www/index.html` y después:

```bash
npx cap sync ios
```

Para una nueva versión en la tienda, sube el número en Xcode (*Version* 1.1, o *Build* 2) y vuelve a hacer Archive.

### Cambiar el ícono o el splash
Reemplaza `assets/icon-1024.png` (1024×1024, sin transparencia) y `assets/splash.png` / `splash-dark.png` (2732×2732) y corre:

```bash
npx capacitor-assets generate --ios --iconBackgroundColor '#0E7470' --splashBackgroundColor '#EDF2F4' --splashBackgroundColorDark '#0E171C'
```

## Notas

- Solo iPhone, en vertical. El idioma de la app es español (México).
- Los datos se guardan con `@capacitor/preferences` en el teléfono (y en `localStorage` cuando se abre en un navegador).
- Fuentes: Bricolage Grotesque, Atkinson Hyperlegible e IBM Plex Mono, con licencia SIL Open Font License (ver `www/fonts/`).
- Rewiro es una herramienta de apoyo; no sustituye atención médica.
