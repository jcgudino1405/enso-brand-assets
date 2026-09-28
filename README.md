# Enso Loyalty Systems · Imágenes de marca para Google Wallet y Apple Wallet

> **Copia pública, solo imágenes.** Estas imágenes se publican aquí para que Google Wallet y Apple Wallet puedan leerlas desde una URL pública. Las direcciones de cada archivo están en [URLS.md](URLS.md). El código de Enso y el generador de estas imágenes están en un repositorio privado; los comandos de abajo se refieren a ese repositorio.

Carpeta lista para subir a mano: logos, íconos, franjas de sellos y logos del programa que pide la **Google Pay & Wallet Console** (antes de solicitar el acceso de publicación) y el **pase de Apple Wallet** (`storeCard`), más el avatar y la imagen para redes.

Todo sale de las fuentes oficiales de marca v2 (`docs/enso-marca-v2/`, `tokens.json`, `public/brand/*.svg`, `src/components/enso/ensoPath.ts`, paleta `TINTA` de `src/lib/designs.ts`) y se regenera con un solo comando:

```bash
node brand-assets/scripts/generate.mjs
```

El generador dibuja cada PNG con Chromium (Playwright) a su tamaño exacto, usa el trazo exacto del ensō, carga Bricolage Grotesque 800 y Figtree 700 desde Google Fonts (se detiene si no cargan), lee la cabecera de cada PNG para comprobar sus medidas y reescribe la tabla de inventario de abajo. Paleta y valores para `pass.json` / clase de Google: [colores.md](colores.md).

## Estructura

```
brand-assets/
├── README.md                       este archivo
├── colores.md                      paleta HEX / RGB y campos de color de las wallets
├── scripts/generate.mjs            generador reproducible
├── logos/
│   ├── svg/                        los 7 SVG oficiales, sin metadatos C2PA
│   └── png/                        ensō (5 variantes × 512 y 1024) y lockups horizontal / apilado
├── app-icon/                       1024, 512, 192 (esquinas redondeadas), 180 apple-touch y 1024 cuadrado
├── google-wallet/
│   ├── program-logo-clay-*.png     logo del programa (recomendado) 1200 y 660
│   ├── program-logo-graphite-*.png alternativa
│   ├── wide-program-logo-*.png     logo ancho 1280×400 transparente
│   ├── business-logo-1024.png      logo del perfil de negocio en la consola
│   ├── hero-1032x812/              heroImage vigente, 0 a 10 sellos
│   ├── hero-1032x336/              heroImage apaisado (franja 3:1), 0 a 10 sellos
│   └── sample-pass-mock.png        maqueta del pase (7 de 10), para referencia y capturas
├── apple-wallet/
│   ├── icon/                       icon.png, icon@2x.png, icon@3x.png (38 pt)
│   ├── logo/                       logo.png, @2x, @3x (50×50 pt, dentro de 160×50)
│   ├── strip-375x144/stamps-00…10/ strip.png, @2x, @3x (tamaño vigente de Apple)
│   └── strip-375x123/stamps-00…10/ strip.png, @2x, @3x (tamaño de la guía de marca)
└── social/
    ├── enso-avatar-1080.png        foto de perfil
    └── og-image-1200x630.png       og:image, plantilla Oferta
```

Cada carpeta `stamps-NN/` de Apple es un juego completo: copia `strip.png`, `strip@2x.png` y `strip@3x.png` tal cual al paquete del pase con NN sellos.

## Especificaciones oficiales verificadas (28 sep 2026)

### Google Wallet

| Imagen | Especificación oficial | Fuente | Qué se generó |
|---|---|---|---|
| `programLogo` (obligatorio) | PNG, mínimo **660 × 660 px**, 1:1. Google lo **recorta en círculo**: no enmascararlo, dejarlo cuadrado con fondo a sangre y **15 % de margen** (área segura de **840 × 840 px**). | [Brand guidelines · Loyalty](https://developers.google.com/wallet/retail/loyalty-cards/resources/brand-guidelines) | 1200 × 1200 (840 / 1200 = 70 %, el mismo encuadre que `enso-avatar.svg`) y 660 × 660. El lienzo de 1200 es una inferencia del área segura de 840 con margen de 15 %: **por confirmar**; el de 660 cumple el mínimo documentado. |
| `wideProgramLogo` (opcional) | **PNG transparente**, recomendado **1280 × 400 px**, alto mínimo 400, proporción **16:5**. Sobre fondo oscuro, color muy claro. Reemplaza al logo redondo arriba a la izquierda. | misma página; [LoyaltyClass](https://developers.google.com/wallet/reference/rest/v1/loyaltyclass) | 1280 × 400 Crema (pase oscuro) y Tinta (solo pase claro). |
| `heroImage` (opcional) | PNG (transparente si quieres que se vea el fondo), recomendado **1032 × 812 px** (~5:4), **20 dp** de aire arriba y abajo, sin texto incrustado, **no usar imágenes finas** ni cuadradas. Se muestra al 100 % del ancho. | misma página ("Pass creation guidelines", actualizado) | 1032 × 812, 0–10 sellos. También 1032 × 336 (franja 3:1, la que usa hoy `GoogleWalletCard.tsx`), que Google ahora desaconseja. |
| `hexBackgroundColor` | `#rrggbb`; si falta, Google usa el color dominante del hero o del logo. Evitar colores saturados "vibrantes". | [LoyaltyClass](https://developers.google.com/wallet/reference/rest/v1/loyaltyclass) | `#1C1917` (ver colores.md). |
| Logo del **perfil de negocio** (Pay & Wallet Console) | Opcional. Mínimo **640 × 640**, máximo **1024 × 1024 px**, máximo **5 MB**. Formato y forma no documentados. | [Business Profile page](https://support.google.com/google-pay-and-wallet-console/answer/10877772?hl=en) | 1024 × 1024, Naranja Sello a sangre (seguro también si lo recortan en círculo). |

### Apple Wallet (`storeCard`)

Todas las medidas en puntos; se entregan @1x, @2x y @3x ([archivo de Apple](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/PassKit_PG/Creating.html): "provide the original, @2x, and @3x versions").

| Imagen | Especificación oficial vigente | Fuente | Qué se generó |
|---|---|---|---|
| `icon.png` (obligatorio) | **38 × 38 pt**. El sistema redondea las esquinas: no redondearlas. (La guía antigua decía 29 × 29 pt.) | [HIG · Wallet](https://developer.apple.com/design/human-interface-guidelines/wallet) | 38 / 76 / 114 px, ensō Naranja Sello sobre Tinta a sangre. |
| `logo.png` | Alto **50 pt**, ancho **50–160 pt**. Sin sombras interiores. | HIG · Wallet | 50 / 100 / 150 px, `enso-mark-bold-chalk` (lo que pide la guía de canal cuando no hay logo del comercio). |
| `strip.png` | **375 × 144 pt** para coupon y store card (HIG vigente). La guía antigua: 375 × 144 para gift cards y coupons y **375 × 123** "en los demás casos". Puede ir texto encima: sin texto en la imagen, zonas detrás del texto limpias. | HIG · Wallet; guía antigua (enlace arriba) | Dos juegos, 0–10 sellos cada uno: **375 × 144** (vigente) y **375 × 123** (el que fija `04-guias-por-canal-v2.md`). |

## Qué subir y dónde

**Google Pay & Wallet Console** (pay.google.com/business/console)
- Perfil de negocio → logo: `google-wallet/business-logo-1024.png`.
- Clase de fidelización de ejemplo (la que Google revisa para publicar): `programLogo` = `google-wallet/program-logo-clay-1200.png`, `hexBackgroundColor` = `#1C1917`, `heroImage` = `google-wallet/hero-1032x812/hero-stamps-00.png` (o el hero en cada objeto según los sellos del cliente). `wideProgramLogo` solo si se decide mostrar el nombre en vez del logo redondo.
- Las imágenes de Google van por URL pública (`sourceUri.uri`): hay que alojarlas en el dominio de Enso (por ejemplo `/brand/wallet/...`) antes de crear la clase.

**Apple Wallet** (paquete `.pkpass`)
- `icon.png`, `icon@2x.png`, `icon@3x.png` de `apple-wallet/icon/`.
- `logo.png`, `@2x`, `@3x` de `apple-wallet/logo/` solo si el comercio no da su logo.
- `strip.png`, `@2x`, `@3x` de `apple-wallet/strip-375x144/stamps-NN/` según los sellos (o `strip-375x123/` si se mantiene la guía de marca).

**Redes y web**: `social/enso-avatar-1080.png` como foto de perfil; `social/og-image-1200x630.png` como `og:image`; `app-icon/apple-touch-icon-180.png` y `app-icon/enso-app-icon-192.png` / `-512.png` para el favicon y el manifest.

## Lista para la solicitud de publicación en Google Wallet

- [ ] Perfil de negocio completo (nombre público, sitio, URL y correo de soporte, teléfono) y logo `business-logo-1024.png`.
- [ ] Issuer ID aprobado y cuenta de servicio añadida como usuario del emisor (ALTA_CUENTAS_WALLET.md, pasos 2–5).
- [ ] Imágenes alojadas en una URL pública HTTPS del dominio definitivo.
- [ ] Clase de fidelización de ejemplo creada con el branding real: `programLogo`, `programName`, `issuerName`, `hexBackgroundColor: "#1C1917"` y `heroImage`.
- [ ] Probar el pase con las cuentas de prueba en modo demo (Android real) y revisar el recorte circular del logo.
- [ ] Política de privacidad y términos accesibles sin iniciar sesión en el dominio definitivo.
- [ ] Sitio web que describe el programa de fidelización de forma reconocible.
- [ ] Capturas del pase en el teléfono (o `google-wallet/sample-pass-mock.png` como referencia visual; no es una captura real).
- [ ] Enviar la solicitud de publicación desde la consola.

## Qué NO usar (reglas de marca)

- No rotar el ensō: la abertura va siempre a la 1 en punto. No cerrarlo, rellenarlo, duplicarlo, ni poner texto o íconos dentro.
- Nada de degradados, sombras, contornos ni efectos. Siempre una sola tinta plana.
- No usar el trazo normal por debajo de 32 px (usar `bold`); nunca por debajo de 16 px en pantalla.
- Respetar el aire: ¼ del diámetro del ensō a cada lado. Los lockups de `logos/png/` ya lo incluyen.
- No cambiar las fuentes, el orden ni la proporción entre ensō y nombre en el lockup; no escribir "enso" en otra fuente. No dos logos en una pieza.
- No usar `enso-mark-graphite` sobre Tinta ni `enso-mark-chalk` sobre Crema. `wide-program-logo-graphite` no sirve sobre el pase `#1C1917`.
- `clay` (Naranja Sello) es un acento: una vez por pieza. `brand-sun` solo en precio, garantía o cupos (máximo 5 %).
- En la franja de sellos solo ensōs: ni estrellas, ni tazas, ni el ensō como patrón de fondo. Sin texto dentro de las imágenes del pase (Apple y Google no lo traducen).
- No cambiar el fondo del pase (siempre `#1C1917`) ni el color de etiquetas (siempre `#FF8A5B`).
- El pase es del comercio: su logo va primero; Enso solo firma en el pie ("Un sello a la vez · enso").
- No usar los SVG de `docs/enso-marca-v2/logos/` para publicar: llevan metadatos C2PA. Usar los de `logos/svg/`.
- No usar emoji.

## Inventario

<!-- inventario:inicio -->

_134 archivos. Medidas leídas de la cabecera de cada PNG por el generador._

| Archivo | Tamaño (px) | Formato | Fondo | Dónde se sube | Notas |
|---|---|---|---|---|---|
| `logos/svg/enso-mark-graphite.svg` | vectorial (viewBox 100) | SVG · 5.3 KB | transparente | Web, imprenta, diseño | Oficial, sin metadatos C2PA. |
| `logos/svg/enso-mark-clay.svg` | vectorial (viewBox 100) | SVG · 5.3 KB | transparente | Web, imprenta, diseño | Oficial, sin metadatos C2PA. |
| `logos/svg/enso-mark-chalk.svg` | vectorial (viewBox 100) | SVG · 5.3 KB | transparente | Web, imprenta, diseño | Oficial, sin metadatos C2PA. |
| `logos/svg/enso-mark-bold-graphite.svg` | vectorial (viewBox 100) | SVG · 5.3 KB | transparente | Web, imprenta, diseño | Oficial, sin metadatos C2PA. |
| `logos/svg/enso-mark-bold-chalk.svg` | vectorial (viewBox 100) | SVG · 5.3 KB | transparente | Web, imprenta, diseño | Oficial, sin metadatos C2PA. |
| `logos/svg/enso-avatar.svg` | vectorial (viewBox 100) | SVG · 5.4 KB | Naranja Sello | Web, imprenta, diseño | Oficial, sin metadatos C2PA. |
| `logos/svg/enso-app-icon.svg` | vectorial (viewBox 100) | SVG · 5.4 KB | baldosa Tinta | Web, imprenta, diseño | Oficial, sin metadatos C2PA. |
| `logos/png/enso-mark-graphite-512.png` | 512 × 512 | PNG (RGBA) · 15.3 KB | transparente | Web, documentos, presentaciones | Fondos Crema, Arena o Naranja Sello. Marca por defecto. |
| `logos/png/enso-mark-graphite-1024.png` | 1024 × 1024 | PNG (RGBA) · 33.6 KB | transparente | Web, documentos, presentaciones | Fondos Crema, Arena o Naranja Sello. Marca por defecto. |
| `logos/png/enso-mark-chalk-512.png` | 512 × 512 | PNG (RGBA) · 14.0 KB | transparente | Web, documentos, presentaciones | Fondos Tinta o Verde Retorno. |
| `logos/png/enso-mark-chalk-1024.png` | 1024 × 1024 | PNG (RGBA) · 31.2 KB | transparente | Web, documentos, presentaciones | Fondos Tinta o Verde Retorno. |
| `logos/png/enso-mark-clay-512.png` | 512 × 512 | PNG (RGBA) · 15.3 KB | transparente | Web, documentos, presentaciones | Acento, una vez por pieza. Sobre Crema o Tinta. |
| `logos/png/enso-mark-clay-1024.png` | 1024 × 1024 | PNG (RGBA) · 33.8 KB | transparente | Web, documentos, presentaciones | Acento, una vez por pieza. Sobre Crema o Tinta. |
| `logos/png/enso-mark-bold-graphite-512.png` | 512 × 512 | PNG (RGBA) · 15.4 KB | transparente | Web, documentos, presentaciones | Trazo grueso: solo si se mostrará por debajo de 32 px. |
| `logos/png/enso-mark-bold-graphite-1024.png` | 1024 × 1024 | PNG (RGBA) · 33.9 KB | transparente | Web, documentos, presentaciones | Trazo grueso: solo si se mostrará por debajo de 32 px. |
| `logos/png/enso-mark-bold-chalk-512.png` | 512 × 512 | PNG (RGBA) · 14.2 KB | transparente | Web, documentos, presentaciones | Trazo grueso sobre Tinta: solo por debajo de 32 px. |
| `logos/png/enso-mark-bold-chalk-1024.png` | 1024 × 1024 | PNG (RGBA) · 31.5 KB | transparente | Web, documentos, presentaciones | Trazo grueso sobre Tinta: solo por debajo de 32 px. |
| `logos/png/enso-lockup-horizontal-graphite-on-chalk-2000.png` | 2000 × 634 | PNG · 45.7 KB | Crema #FFF6E8 | Web (cabecera), firmas, documentos | Aire incluido: 25 % del diámetro del ensō. |
| `logos/png/enso-lockup-horizontal-chalk-on-graphite-2000.png` | 2000 × 634 | PNG · 46.4 KB | Tinta #1C1917 | Web (cabecera), firmas, documentos | Aire incluido: 25 % del diámetro del ensō. |
| `logos/png/enso-lockup-horizontal-graphite-2000.png` | 2000 × 634 | PNG (RGBA) · 49.0 KB | transparente | Web (cabecera), firmas, documentos | Aire incluido: 25 % del diámetro del ensō. |
| `logos/png/enso-lockup-horizontal-chalk-2000.png` | 2000 × 634 | PNG (RGBA) · 45.7 KB | transparente | Web (cabecera), firmas, documentos | Aire incluido: 25 % del diámetro del ensō. |
| `logos/png/enso-lockup-stacked-graphite-on-chalk-1600.png` | 1600 × 1580 | PNG · 63.2 KB | Crema #FFF6E8 | Portadas, piezas cuadradas | Aire incluido: 25 % del diámetro del ensō. |
| `logos/png/enso-lockup-stacked-chalk-on-graphite-1600.png` | 1600 × 1580 | PNG · 64.2 KB | Tinta #1C1917 | Portadas, piezas cuadradas | Aire incluido: 25 % del diámetro del ensō. |
| `logos/png/enso-lockup-stacked-graphite-1600.png` | 1600 × 1580 | PNG (RGBA) · 67.7 KB | transparente | Portadas, piezas cuadradas | Aire incluido: 25 % del diámetro del ensō. |
| `logos/png/enso-lockup-stacked-chalk-1600.png` | 1600 × 1580 | PNG (RGBA) · 63.7 KB | transparente | Portadas, piezas cuadradas | Aire incluido: 25 % del diámetro del ensō. |
| `app-icon/enso-app-icon-1024.png` | 1024 × 1024 | PNG (RGBA) · 34.4 KB | baldosa Tinta con esquinas redondeadas (esquinas transparentes) | PWA / manifest, favicon grande | De enso-app-icon.svg. |
| `app-icon/enso-app-icon-512.png` | 512 × 512 | PNG (RGBA) · 15.6 KB | baldosa Tinta con esquinas redondeadas (esquinas transparentes) | PWA / manifest, favicon grande | De enso-app-icon.svg. |
| `app-icon/enso-app-icon-192.png` | 192 × 192 | PNG (RGBA) · 5.4 KB | baldosa Tinta con esquinas redondeadas (esquinas transparentes) | PWA / manifest, favicon grande | De enso-app-icon.svg. |
| `app-icon/apple-touch-icon-180.png` | 180 × 180 | PNG · 3.4 KB | Tinta #1C1917 a sangre (sin redondear) | Web: <link rel="apple-touch-icon"> | iOS redondea solo; sin transparencia. |
| `app-icon/enso-app-icon-1024-square.png` | 1024 × 1024 | PNG · 23.3 KB | Tinta #1C1917 a sangre (sin redondear) | Tiendas / plataformas que redondean solas | Misma composición que el ícono, sin esquinas. |
| `google-wallet/program-logo-clay-1200.png` | 1200 × 1200 | PNG · 27.6 KB | Naranja Sello #E4572E a sangre | LoyaltyClass.programLogo | Recomendado: igual que enso-avatar. Google lo recorta en círculo; el ensō queda en el 70 % central. |
| `google-wallet/program-logo-graphite-1200.png` | 1200 × 1200 | PNG · 27.7 KB | Tinta #1C1917 a sangre | LoyaltyClass.programLogo (alternativa) | Sobre un pase #1C1917 el círculo se funde con la tarjeta. |
| `google-wallet/program-logo-clay-660.png` | 660 × 660 | PNG · 14.0 KB | Naranja Sello #E4572E a sangre | LoyaltyClass.programLogo | Recomendado: igual que enso-avatar. Google lo recorta en círculo; el ensō queda en el 70 % central. |
| `google-wallet/program-logo-graphite-660.png` | 660 × 660 | PNG · 14.0 KB | Tinta #1C1917 a sangre | LoyaltyClass.programLogo (alternativa) | Sobre un pase #1C1917 el círculo se funde con la tarjeta. |
| `google-wallet/business-logo-1024.png` | 1024 × 1024 | PNG · 23.1 KB | Naranja Sello #E4572E a sangre | Pay & Wallet Console → Business profile (logo) | Consola: 640–1024 px, máx. 5 MB. |
| `google-wallet/wide-program-logo-chalk-1280x400.png` | 1280 × 400 | PNG (RGBA) · 26.0 KB | transparente | LoyaltyClass.wideProgramLogo (pase oscuro) | Lockup Crema, alineado a la izquierda, centrado en alto. |
| `google-wallet/wide-program-logo-graphite-1280x400.png` | 1280 × 400 | PNG (RGBA) · 27.7 KB | transparente | LoyaltyClass.wideProgramLogo (solo si el pase fuera claro) | No usar sobre #1C1917. |
| `google-wallet/hero-1032x812/hero-stamps-00.png` | 1032 × 812 | PNG · 25.2 KB | Franja #2A2521 | LoyaltyObject.heroImage (o LoyaltyClass.heroImage para 0) | 0 de 10 sellos. Formato vigente 1032×812. |
| `google-wallet/hero-1032x812/hero-stamps-01.png` | 1032 × 812 | PNG · 29.1 KB | Franja #2A2521 | LoyaltyObject.heroImage (o LoyaltyClass.heroImage para 0) | 1 de 10 sellos. Formato vigente 1032×812. |
| `google-wallet/hero-1032x812/hero-stamps-02.png` | 1032 × 812 | PNG · 32.0 KB | Franja #2A2521 | LoyaltyObject.heroImage (o LoyaltyClass.heroImage para 0) | 2 de 10 sellos. Formato vigente 1032×812. |
| `google-wallet/hero-1032x812/hero-stamps-03.png` | 1032 × 812 | PNG · 32.3 KB | Franja #2A2521 | LoyaltyObject.heroImage (o LoyaltyClass.heroImage para 0) | 3 de 10 sellos. Formato vigente 1032×812. |
| `google-wallet/hero-1032x812/hero-stamps-04.png` | 1032 × 812 | PNG · 30.2 KB | Franja #2A2521 | LoyaltyObject.heroImage (o LoyaltyClass.heroImage para 0) | 4 de 10 sellos. Formato vigente 1032×812. |
| `google-wallet/hero-1032x812/hero-stamps-05.png` | 1032 × 812 | PNG · 27.3 KB | Franja #2A2521 | LoyaltyObject.heroImage (o LoyaltyClass.heroImage para 0) | 5 de 10 sellos. Formato vigente 1032×812. |
| `google-wallet/hero-1032x812/hero-stamps-06.png` | 1032 × 812 | PNG · 30.8 KB | Franja #2A2521 | LoyaltyObject.heroImage (o LoyaltyClass.heroImage para 0) | 6 de 10 sellos. Formato vigente 1032×812. |
| `google-wallet/hero-1032x812/hero-stamps-07.png` | 1032 × 812 | PNG · 33.7 KB | Franja #2A2521 | LoyaltyObject.heroImage (o LoyaltyClass.heroImage para 0) | 7 de 10 sellos. Formato vigente 1032×812. |
| `google-wallet/hero-1032x812/hero-stamps-08.png` | 1032 × 812 | PNG · 33.8 KB | Franja #2A2521 | LoyaltyObject.heroImage (o LoyaltyClass.heroImage para 0) | 8 de 10 sellos. Formato vigente 1032×812. |
| `google-wallet/hero-1032x812/hero-stamps-09.png` | 1032 × 812 | PNG · 31.5 KB | Franja #2A2521 | LoyaltyObject.heroImage (o LoyaltyClass.heroImage para 0) | 9 de 10 sellos. Formato vigente 1032×812. |
| `google-wallet/hero-1032x812/hero-stamps-10.png` | 1032 × 812 | PNG · 28.5 KB | Franja #2A2521 | LoyaltyObject.heroImage (o LoyaltyClass.heroImage para 0) | 10 de 10 sellos. Formato vigente 1032×812. |
| `google-wallet/hero-1032x336/hero-strip-00.png` | 1032 × 336 | PNG · 23.9 KB | Franja #2A2521 | heroImage alternativo (franja 3:1) | 0 de 10 sellos. Google ahora desaconseja imágenes finas. |
| `google-wallet/hero-1032x336/hero-strip-01.png` | 1032 × 336 | PNG · 24.9 KB | Franja #2A2521 | heroImage alternativo (franja 3:1) | 1 de 10 sellos. Google ahora desaconseja imágenes finas. |
| `google-wallet/hero-1032x336/hero-strip-02.png` | 1032 × 336 | PNG · 25.7 KB | Franja #2A2521 | heroImage alternativo (franja 3:1) | 2 de 10 sellos. Google ahora desaconseja imágenes finas. |
| `google-wallet/hero-1032x336/hero-strip-03.png` | 1032 × 336 | PNG · 26.1 KB | Franja #2A2521 | heroImage alternativo (franja 3:1) | 3 de 10 sellos. Google ahora desaconseja imágenes finas. |
| `google-wallet/hero-1032x336/hero-strip-04.png` | 1032 × 336 | PNG · 26.4 KB | Franja #2A2521 | heroImage alternativo (franja 3:1) | 4 de 10 sellos. Google ahora desaconseja imágenes finas. |
| `google-wallet/hero-1032x336/hero-strip-05.png` | 1032 × 336 | PNG · 26.4 KB | Franja #2A2521 | heroImage alternativo (franja 3:1) | 5 de 10 sellos. Google ahora desaconseja imágenes finas. |
| `google-wallet/hero-1032x336/hero-strip-06.png` | 1032 × 336 | PNG · 27.1 KB | Franja #2A2521 | heroImage alternativo (franja 3:1) | 6 de 10 sellos. Google ahora desaconseja imágenes finas. |
| `google-wallet/hero-1032x336/hero-strip-07.png` | 1032 × 336 | PNG · 27.7 KB | Franja #2A2521 | heroImage alternativo (franja 3:1) | 7 de 10 sellos. Google ahora desaconseja imágenes finas. |
| `google-wallet/hero-1032x336/hero-strip-08.png` | 1032 × 336 | PNG · 28.0 KB | Franja #2A2521 | heroImage alternativo (franja 3:1) | 8 de 10 sellos. Google ahora desaconseja imágenes finas. |
| `google-wallet/hero-1032x336/hero-strip-09.png` | 1032 × 336 | PNG · 28.2 KB | Franja #2A2521 | heroImage alternativo (franja 3:1) | 9 de 10 sellos. Google ahora desaconseja imágenes finas. |
| `google-wallet/hero-1032x336/hero-strip-10.png` | 1032 × 336 | PNG · 28.2 KB | Franja #2A2521 | heroImage alternativo (franja 3:1) | 10 de 10 sellos. Google ahora desaconseja imágenes finas. |
| `google-wallet/sample-pass-mock.png` | 1200 × 1500 | PNG · 72.1 KB | Crema #FFF6E8 | Referencia / capturas para la solicitud de publicación | Maqueta: 7 de 10 sellos. La app real usa Roboto. |
| `apple-wallet/icon/icon.png` | 38 × 38 | PNG · 0.7 KB | Tinta #1C1917 a sangre | pass: icon.png (obligatorio) | Apple redondea las esquinas. Composición de enso-app-icon sin esquinas. |
| `apple-wallet/logo/logo.png` | 50 × 50 | PNG (RGBA) · 1.3 KB | transparente | pass: logo.png (sin comercio) | enso-mark-bold-chalk, 50×50 pt dentro de 160×50. |
| `apple-wallet/icon/icon@2x.png` | 76 × 76 | PNG · 1.4 KB | Tinta #1C1917 a sangre | pass: icon.png (obligatorio) | Apple redondea las esquinas. Composición de enso-app-icon sin esquinas. |
| `apple-wallet/logo/logo@2x.png` | 100 × 100 | PNG (RGBA) · 2.5 KB | transparente | pass: logo.png (sin comercio) | enso-mark-bold-chalk, 50×50 pt dentro de 160×50. |
| `apple-wallet/icon/icon@3x.png` | 114 × 114 | PNG · 2.1 KB | Tinta #1C1917 a sangre | pass: icon.png (obligatorio) | Apple redondea las esquinas. Composición de enso-app-icon sin esquinas. |
| `apple-wallet/logo/logo@3x.png` | 150 × 150 | PNG (RGBA) · 3.8 KB | transparente | pass: logo.png (sin comercio) | enso-mark-bold-chalk, 50×50 pt dentro de 160×50. |
| `apple-wallet/strip-375x144/stamps-00/strip.png` | 375 × 144 | PNG · 9.2 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 0 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-00/strip@2x.png` | 750 × 288 | PNG · 19.8 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 0 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-00/strip@3x.png` | 1125 × 432 | PNG · 31.0 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 0 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-01/strip.png` | 375 × 144 | PNG · 9.7 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 1 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-01/strip@2x.png` | 750 × 288 | PNG · 20.8 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 1 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-01/strip@3x.png` | 1125 × 432 | PNG · 32.4 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 1 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-02/strip.png` | 375 × 144 | PNG · 10.0 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 2 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-02/strip@2x.png` | 750 × 288 | PNG · 21.4 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 2 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-02/strip@3x.png` | 1125 × 432 | PNG · 33.3 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 2 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-03/strip.png` | 375 × 144 | PNG · 10.2 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 3 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-03/strip@2x.png` | 750 × 288 | PNG · 21.7 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 3 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-03/strip@3x.png` | 1125 × 432 | PNG · 33.9 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 3 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-04/strip.png` | 375 × 144 | PNG · 10.3 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 4 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-04/strip@2x.png` | 750 × 288 | PNG · 22.0 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 4 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-04/strip@3x.png` | 1125 × 432 | PNG · 34.2 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 4 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-05/strip.png` | 375 × 144 | PNG · 10.3 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 5 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-05/strip@2x.png` | 750 × 288 | PNG · 22.0 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 5 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-05/strip@3x.png` | 1125 × 432 | PNG · 34.3 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 5 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-06/strip.png` | 375 × 144 | PNG · 10.6 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 6 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-06/strip@2x.png` | 750 × 288 | PNG · 22.6 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 6 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-06/strip@3x.png` | 1125 × 432 | PNG · 35.3 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 6 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-07/strip.png` | 375 × 144 | PNG · 10.8 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 7 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-07/strip@2x.png` | 750 × 288 | PNG · 23.1 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 7 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-07/strip@3x.png` | 1125 × 432 | PNG · 36.0 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 7 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-08/strip.png` | 375 × 144 | PNG · 11.0 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 8 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-08/strip@2x.png` | 750 × 288 | PNG · 23.5 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 8 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-08/strip@3x.png` | 1125 × 432 | PNG · 36.5 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 8 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-09/strip.png` | 375 × 144 | PNG · 11.0 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 9 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-09/strip@2x.png` | 750 × 288 | PNG · 23.6 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 9 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-09/strip@3x.png` | 1125 × 432 | PNG · 36.7 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 9 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-10/strip.png` | 375 × 144 | PNG · 11.0 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 10 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-10/strip@2x.png` | 750 × 288 | PNG · 23.5 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 10 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x144/stamps-10/strip@3x.png` | 1125 × 432 | PNG · 36.6 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 10 de 10 sellos. HIG vigente (375×144 pt). |
| `apple-wallet/strip-375x123/stamps-00/strip.png` | 375 × 123 | PNG · 8.0 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 0 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-00/strip@2x.png` | 750 × 246 | PNG · 17.0 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 0 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-00/strip@3x.png` | 1125 × 369 | PNG · 26.3 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 0 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-01/strip.png` | 375 × 123 | PNG · 8.4 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 1 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-01/strip@2x.png` | 750 × 246 | PNG · 17.7 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 1 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-01/strip@3x.png` | 1125 × 369 | PNG · 27.5 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 1 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-02/strip.png` | 375 × 123 | PNG · 8.6 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 2 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-02/strip@2x.png` | 750 × 246 | PNG · 18.3 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 2 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-02/strip@3x.png` | 1125 × 369 | PNG · 28.3 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 2 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-03/strip.png` | 375 × 123 | PNG · 8.8 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 3 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-03/strip@2x.png` | 750 × 246 | PNG · 18.6 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 3 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-03/strip@3x.png` | 1125 × 369 | PNG · 28.7 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 3 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-04/strip.png` | 375 × 123 | PNG · 8.9 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 4 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-04/strip@2x.png` | 750 × 246 | PNG · 18.8 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 4 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-04/strip@3x.png` | 1125 × 369 | PNG · 29.1 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 4 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-05/strip.png` | 375 × 123 | PNG · 8.9 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 5 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-05/strip@2x.png` | 750 × 246 | PNG · 18.8 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 5 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-05/strip@3x.png` | 1125 × 369 | PNG · 29.1 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 5 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-06/strip.png` | 375 × 123 | PNG · 9.1 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 6 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-06/strip@2x.png` | 750 × 246 | PNG · 19.3 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 6 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-06/strip@3x.png` | 1125 × 369 | PNG · 30.0 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 6 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-07/strip.png` | 375 × 123 | PNG · 9.3 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 7 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-07/strip@2x.png` | 750 × 246 | PNG · 19.7 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 7 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-07/strip@3x.png` | 1125 × 369 | PNG · 30.5 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 7 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-08/strip.png` | 375 × 123 | PNG · 9.4 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 8 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-08/strip@2x.png` | 750 × 246 | PNG · 20.0 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 8 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-08/strip@3x.png` | 1125 × 369 | PNG · 30.9 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 8 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-09/strip.png` | 375 × 123 | PNG · 9.5 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 9 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-09/strip@2x.png` | 750 × 246 | PNG · 20.1 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 9 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-09/strip@3x.png` | 1125 × 369 | PNG · 31.1 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 9 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-10/strip.png` | 375 × 123 | PNG · 9.5 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 10 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-10/strip@2x.png` | 750 × 246 | PNG · 20.0 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 10 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `apple-wallet/strip-375x123/stamps-10/strip@3x.png` | 1125 × 369 | PNG · 31.1 KB | Franja #2A2521 con reglas #3A332D | pass: strip.png (storeCard) | 10 de 10 sellos. Guía de marca / guía antigua de Apple (375×123 pt). |
| `social/enso-avatar-1080.png` | 1080 × 1080 | PNG · 24.6 KB | Naranja Sello #E4572E | Foto de perfil (Instagram, LinkedIn, Facebook, Google) | De enso-avatar.svg; seguro para recorte circular. |
| `social/og-image-1200x630.png` | 1200 × 630 | PNG · 53.5 KB | Naranja Sello #E4572E | Web: og:image / twitter:image | Plantilla Oferta, "desde USD 40 al mes". |

<!-- inventario:fin -->
