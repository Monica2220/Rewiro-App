# Rewiro · Hackea tu cerebro

App para dejar de fumar: cronómetro desde tu fecha de corte, botón **SOS** (respiración de 5 minutos), cajetilla que no compraste, dinero ahorrado, premios, patrones de consumo.


## Estructura

```
rewiro/
├── www/                  ← la app (HTML, fuentes, íconos). 
├── ios/                  ← proyecto de Xcode generado (Capacitor 8)
├── assets/               ← ícono 1024 y splash, para regenerar los de iOS
├── capacitor.config.json ← nombre de la app e identificador (mx.moni.rewiro)
├── package.json
└── PRIVACY.md            ← política de privacidad 
```


## Notas

- Solo iPhone, en vertical. El idioma de la app es español (México).
- Los datos se guardan con `@capacitor/preferences` en el teléfono (y en `localStorage` cuando se abre en un navegador).
- Fuentes: Bricolage Grotesque, Atkinson Hyperlegible e IBM Plex Mono, con licencia SIL Open Font License (ver `www/fonts/`).
- Rewiro es una herramienta de apoyo; no sustituye atención médica.
