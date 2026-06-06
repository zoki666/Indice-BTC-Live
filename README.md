# 📊 Índice BTC-Live

**Índice macro de Bitcoin para acumulación y distribución a largo plazo.**

Índice BTC-Live publicado en Github Pages: https://zoki666.github.io/Indice-BTC-Live/

El Índice BTC-Live combina **8 indicadores clave** (sentimiento, análisis técnico, on-chain y macro) en una puntuación única de 0 a 100.  
Cada indicador se mide de 0 a 10 con la misma lógica:

- **10 = suelo del mercado → oportunidad de compra**
- **0 = techo del mercado → señal de venta**

El índice final es un promedio ponderado que da más peso a los indicadores con mejor historial predictivo.

---

## 🧭 Interpretación rápida

| Rango | Significado | Acción recomendada |
|-------|-------------|-------------------|
| **75 – 100** | Suelo / zona de acumulación | Compras DCA, aumentar exposición |
| **26 – 74** | Neutral | Mantener posición, cautela |
| **0 – 25** | Techo / zona de distribución | Vender parcialmente, proteger capital |

---

## 🧩 Indicadores incluidos

| Letra | Indicador | Peso | Rango 0 (Techo / Vender) | Rango 5 (Neutral) | Rango 10 (Suelo / Comprar) | Proveedor principal / cálculo |
|-------|-----------|------|---------------------------|--------------------|----------------------------|-------------------------------|
| **C** | Pi Cycle Top | 14% | Ratio > 1.0 (precio cruza o supera SMA350×2) | Ratio ≈ 0.75 | Ratio < 0.5 (precio muy por debajo del cruce) | Binance → Bybit → KuCoin (velas diarias) |
| **R** | RSI 14 diario | 8% | RSI > 80 (sobrecompra extrema) | RSI ≈ 50 | RSI < 20 (sobreventa extrema) | Binance → Bybit → KuCoin (velas diarias) |
| **E** | EMA 200 semanal | 20% | Precio > 2.0 × EMA (extremo alcista) | Precio ≈ EMA | Precio < 0.5 × EMA (extremo bajista) | Binance → Bybit → KuCoin (velas semanales) |
| **F** | Fear & Greed (SMA7) | 12% | SMA7 > 80 (codicia sostenida) | SMA7 ≈ 40-60 | SMA7 < 20 (miedo sostenido) | Alternative.me (principal) + RSI (respaldo) |
| **V** | Volatilidad 30d | 8% | < 25% (complacencia, techos) | ≈ 40-50% | > 70% (pánico, suelos) | Binance → Bybit → KuCoin (velas diarias) |
| **M** | MVRV Z‑Score | 20% | MVRV > 3.5 (sobrevalorado, euforia) | ≈ 1.5-2.5 | MVRV < 0.8 (infravalorado, capitulación) | CoinMetrics (principal) + Blockchain.info (respaldo) |
| **S** | Stablecoin Dom | 18% | < 3% (euforia, riesgo alto) | ≈ 5-6% | > 12% (miedo extremo, refugio) | CoinGecko (principal) + CoinPaprika (respaldo) |
| 💰 | Precio BTC | (no ponderado) | — | — | — | Binance (principal) → CoinCap → CoinGecko (respaldo) |

Cada indicador se calcula en tiempo real desde APIs públicas (Binance, Bybit, KuCoin, CoinGecko, CoinPaprika, Alternative.me, CoinMetrics, Blockchain.info) con **proveedores de respaldo** automáticos si el principal falla:

- **Pi Cycle Top (C)**: velas diarias de Binance → Bybit → KuCoin
- **RSI 14 diario (R)**: velas diarias de Binance → Bybit → KuCoin
- **EMA 200 semanal (E)**: velas semanales de Binance → Bybit → KuCoin
- **Fear & Greed (F)**: Alternative.me (principal) + RSI (respaldo estimado)
- **Volatilidad 30d (V)**: velas diarias de Binance → Bybit → KuCoin
- **MVRV Z‑Score (M)**: CoinMetrics (principal) → Blockchain.info (respaldo)
- **Stablecoin Dominance (S)**: CoinGecko (principal) → CoinPaprika (respaldo)
- **Precio BTC (💰)**: Binance (principal) → CoinCap → CoinGecko (respaldo, solo visual)

**Mecanismos de fiabilidad:**
- Timeout de 15 segundos con reintentos automáticos (2 reintentos por fallo)
- Si un indicador falla completamente, se muestra en gris y no participa en el índice
- El usuario puede hacer clic en cualquier indicador gris para reintentarlo manualmente
- El índice muestra un aviso "⚠ Puntuación provisional" si faltan datos de algún componente

---

## 📱 Instalación como App (PWA)

La web es una **Progressive Web App** instalable en Android, iOS y escritorio.

### Requisitos
- Un servidor con HTTPS (GitHub Pages, Netlify, Vercel, etc.)
- Los tres archivos: `index.html`, `manifest.json`, `sw.js`

### Instalación rápida con GitHub Pages
1. Sube los tres archivos a un repositorio público en GitHub.
2. Ve a *Settings → Pages* y activa GitHub Pages desde la rama `main`.
3. Abre la URL `https://tuusuario.github.io/repositorio` en Chrome (móvil o escritorio).
4. Aparecerá el aviso **"Añadir a pantalla de inicio"** (o búscalo en el menú del navegador).

### Probar en local (sin instalación definitiva)
En la carpeta del proyecto, ejecuta:

    python -m http.server 8000

Luego accede desde el móvil (misma red WiFi) a `http://IP_DEL_PC:8000`.

---

## 🌗 Tema oscuro / claro

La app incluye un botón flotante (🌙/☀️) que cambia entre tema oscuro (por defecto) y claro.  
La preferencia se guarda automáticamente.

---

## 💰 Donación

Si el índice te resulta útil, puedes apoyar el proyecto:

- **On-chain:** `bc1qthc87aykdj2tjrxlqe7k9emz3txphrprm0scu6`
- **Lightning:** `ffg@cake.cash`

El botón `₿` en la esquina inferior derecha abre un modal con QR y direcciones copiables.

---

## 🔄 Actualización de datos

Los datos se refrescan automáticamente cada **15 minutos**, el precio cada **5 minutos**.
Los indicadores basados en velas diarias cambian una vez al día, pero la consulta frecuente permite detectar caídas de proveedores y usar los respaldos.
Si algún indicador tardara en cargar, la puntuación sería provisional hasta que se actualice.
Se puede actualizar la página entera o pinchar en el indicador oscurecido para refrescarlo.

---

## 📤 Compartir por X

Hay un botón flotante para compartir la puntuación por X y dar la noticia u opinión a tus seguidores.

---

## 🧰 Tecnologías utilizadas

- HTML5 + CSS3 (glassmorphism, animaciones, variables CSS)
- JavaScript vanilla (fetch, async/await, cálculos de indicadores)
- Sin frameworks, sin dependencias externas
- PWA con Service Worker para caché offline

---

## ⚠️ Descargo de responsabilidad

Este índice es una **herramienta educativa** basada en datos históricos.  
**No constituye asesoramiento financiero.** El rendimiento pasado no garantiza resultados futuros. Invierte solo lo que estés dispuesto a perder.

---

## 📄 Licencia

Código abierto bajo licencia MIT.  
Creado con ❤️ para la comunidad Bitcoin.