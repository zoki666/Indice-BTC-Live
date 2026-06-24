# 📊 Índice BTC-Live

**Índice macro de Bitcoin para acumulación y distribución a largo plazo.**

Índice BTC-Live publicado en Github Pages: https://zoki666.github.io/Indice-BTC-Live/

El Índice BTC-Live combina **8 indicadores clave** (técnicos, on-chain, sentimiento y macro) en una puntuación única de 0 a 100.  
Cada indicador se mide de 0 a 10 con la misma lógica:

- **10 = suelo del mercado → oportunidad de compra**
- **0 = techo del mercado → señal de venta**

El índice final es un promedio ponderado optimizado para detectar **suelos y techos de medio/largo plazo**, minimizando el ruido de corto plazo.

---

## 🧭 Interpretación rápida

| Rango | Significado | Acción recomendada |
|-------|-------------|-------------------|
| **75 – 100** | Suelo / zona de acumulación | Compras DCA, aumentar exposición |
| **26 – 74** | Neutral | Mantener posición, cautela |
| **0 – 25** | Techo / zona de distribución | Vender parcialmente, proteger capital |

---

## 🧩 Indicadores incluidos

| Letra | Indicador | Peso | Lógica de puntuación (0=Techo, 10=Suelo) | Proveedores / Cálculo |
|-------|-----------|------|-------------------------------------------|------------------------|
| **C** | Pi Cycle Top | 16% | 0 = precio cerca/cruce SMA350×2 (techo). 10 = precio muy por debajo (suelo). | Velas diarias: Binance → Bybit → KuCoin → Kraken |
| **R** | RSI 14 diario | 5% | 0 = RSI > 80 (sobrecompra). 10 = RSI < 20 (sobreventa). | Velas diarias: Binance → Bybit → KuCoin → Kraken |
| **E** | EMA 200 semanal | 24% | 0 = precio > 2x EMA (extremo). 10 = precio < 0.5x EMA (extremo). | Velas semanales: Binance → Bybit → KuCoin → Kraken |
| **F** | Fear & Greed (SMA7) | 7% | 0 = codicia extrema (>80). 10 = miedo extremo (<20). | Alternative.me (principal) + RSI (respaldo) |
| **V** | Volatilidad 30d (percentil) | 4% | 0 = volatilidad baja/complacencia (techo). 10 = volatilidad alta/pánico (suelo). | Velas diarias: Binance → Bybit → KuCoin → Kraken |
| **X** | DXY (Índice del Dólar) | 10% | 0 = DXY > 115 (dólar extremo). 10 = DXY < 82 (dólar mínimo). | Fórmula geométrica ICE USDX con tasas de: Frankfurter → Exchangerate.fun → Open.er-api |
| **S** | Stablecoin Dominance | 17% | 0 = dominancia < 3% (euforia). 10 = dominancia > 12% (miedo). | CoinGecko (principal) → CoinPaprika (respaldo) |
| **D** | BTC Dominance | 17% | 0 = BTC.D < 40% (altseason/techo). 10 = BTC.D > 60% (capitulación/suelo). | CoinGecko (principal) → CoinPaprika (respaldo) |
| 💰 | Precio BTC | (informativo) | — | Binance → CoinCap → CoinGecko (cada minuto) |

**Pesos asignados en función del rendimiento histórico** real de cada indicador para detectar suelos y techos:
- Mayor peso a indicadores de ciclo largo con pocas falsas señales (EMA 200 semanal, BTC Dominance, Stablecoin Dom)
- Menor peso a indicadores de sentimiento de corto plazo (RSI, Fear & Greed, Volatilidad) para reducir ruido
- Incorporación del DXY como variable macro independiente (fórmula geométrica oficial del ICE)

---

## 🔄 Frecuencia de actualización real

| Indicador | ¿Cada cuánto cambia realmente? |
|-----------|--------------------------------|
| C, R, V (velas diarias) | **1 vez al día** (cierre vela diaria ~00:00 UTC) |
| E (velas semanales) | **1 vez a la semana** (cierre vela semanal domingo) |
| F (Fear & Greed) | **1 vez al día** (Alternative.me actualiza cada 24h) |
| X (DXY) | **1 vez al día** (las APIs de divisas suelen actualizar tras cierre de mercados) |
| S (Stablecoin Dom) | **Cada pocos minutos** (cambios en market cap en vivo) |
| D (BTC Dominance) | **Cada pocos minutos** (igual que S) |
| Precio BTC | **Cada minuto** (consulta a exchanges) |
| Índice completo | **Recálculo cada 15 minutos** (aunque la mayoría de indicadores solo cambiarán 1 vez/día) |

---

## 📱 Instalación como App (PWA)

La web es una **Progressive Web App** instalable en Android, iOS y escritorio.

### Requisitos
- Un servidor con HTTPS (GitHub Pages, Netlify, Vercel, etc.)
- Los archivos: `index.html`, `manifest.json`, `sw.js`

### Instalación rápida con GitHub Pages
1. Sube los archivos a un repositorio público en GitHub.
2. Ve a *Settings → Pages* y activa GitHub Pages desde la rama `main`.
3. Abre la URL `https://tuusuario.github.io/repositorio` en Chrome (móvil o escritorio).
4. Aparecerá el aviso **"Añadir a pantalla de inicio"**.

---

## 🌗 Tema oscuro / claro

Botón flotante 🌙/☀️ para cambiar entre tema oscuro (por defecto) y claro. Preferencia guardada automáticamente.

## 🌐 Idiomas

Alternancia entre español e inglés mediante botón flotante con bandera 🇪🇸/🇬🇧. Traducción completa de la interfaz e indicadores.

## 🔔 Alertas del navegador

Botón en el panel izquierdo para activar notificaciones push automáticas cuando el índice entre en zona de compra (≥80) o venta (≤20). Requiere permiso del usuario.

## 📤 Compartir por X

Botón 𝕏 que genera una imagen del panel del índice y la comparte en X (Twitter) con un texto automático.

## 💰 Donación

Si el índice te resulta útil, puedes apoyar el proyecto:

- **On-chain:** `bc1qthc87aykdj2tjrxlqe7k9emz3txphrprm0scu6`
- **Lightning:** `ffg@cake.cash`

El botón `₿` abre un modal con QR y direcciones.

---

## 🧰 Tecnologías utilizadas

- HTML5 + CSS3 (glassmorphism, animaciones, variables CSS, diseño responsive)
- JavaScript vanilla (fetch, async/await, cálculos de indicadores)
- Sin frameworks ni dependencias externas
- PWA con Service Worker para caché offline

---

## ⚠️ Descargo de responsabilidad

Este índice es una **herramienta educativa** basada en datos históricos.  
**No constituye asesoramiento financiero.** El rendimiento pasado no garantiza resultados futuros. Invierte solo lo que estés dispuesto a perder.

---

## 📄 Licencia

Código abierto bajo licencia MIT.  
Creado con ❤️ para la comunidad Bitcoin.