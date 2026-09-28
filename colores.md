# Enso · Colores para las wallets

Fuente: `docs/enso-marca-v2/tokens.json` y `TINTA` en `src/lib/designs.ts`. Las constantes `brand-*` no cambian con el tema claro/oscuro.

## Campos del pase

| Campo | Plataforma | Valor exacto | Token |
|---|---|---|---|
| `backgroundColor` | Apple `pass.json` | `rgb(28, 25, 23)` | brand-graphite `#1C1917` |
| `foregroundColor` | Apple `pass.json` | `rgb(255, 246, 232)` | brand-chalk `#FFF6E8` |
| `labelColor` | Apple `pass.json` | `rgb(255, 138, 91)` | brand-clay-light `#FF8A5B` |
| `hexBackgroundColor` | Google `LoyaltyClass` / `LoyaltyObject` | `"#1C1917"` | brand-graphite |

```json
{
  "backgroundColor": "rgb(28, 25, 23)",
  "foregroundColor": "rgb(255, 246, 232)",
  "labelColor": "rgb(255, 138, 91)"
}
```

```json
{ "hexBackgroundColor": "#1C1917" }
```

## Franja de sellos (strip.png / heroImage)

| Uso | HEX | RGB | Token |
|---|---|---|---|
| Fondo de la franja | `#2A2521` | 42, 37, 33 | brand-graphite-2 |
| Reglas arriba y abajo (solo Apple) | `#3A332D` | 58, 51, 45 | line (oscuro) |
| Sello ganado | `#FF8A5B` | 255, 138, 91 | brand-clay-light |
| Sello pendiente | `#5A5048` | 90, 80, 72 | brand-stamp-off |
| Pie del pase ("Un sello a la vez · enso") | `#BDB2A5` | 189, 178, 165 | ink-muted (oscuro) |

## Paleta de marca

| Nombre | Token | HEX | RGB | Uso |
|---|---|---|---|---|
| Tinta | brand-graphite | `#1C1917` | 28, 25, 23 | Texto, fondos oscuros, el pase |
| Crema | brand-chalk | `#FFF6E8` | 255, 246, 232 | Fondo principal (60 %), texto sobre Tinta |
| Naranja Sello | brand-clay | `#E4572E` | 228, 87, 46 | El color de Enso: acento, plantilla Oferta, avatar |
| Naranja Claro | brand-clay-light | `#FF8A5B` | 255, 138, 91 | Texto y sellos sobre Tinta; labelColor |
| Amarillo Oferta | brand-sun | `#FFC83D` | 255, 200, 61 | Solo precio, garantía o cupos (máx. 5 %) |
| Verde Retorno | brand-moss | `#17684A` | 23, 104, 74 | Resultados, testimonios |
| Arena | brand-sand | `#F3E3C7` | 243, 227, 199 | Fondo secundario |

Contrastes documentados: Crema sobre Tinta 16,3:1; Naranja Claro sobre Tinta 7,5:1; Tinta sobre Naranja Sello 4,75:1 (Crema sobre Naranja Sello solo a 24 px o más).
