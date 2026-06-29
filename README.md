# 📊 Índice BTC-Live

**Índice macro de Bitcoin para acumulación y distribución a largo plazo.**

Índice BTC-Live publicado en Github Pages: https://zoki666.github.io/Indice-BTC-Live/

El Índice BTC-Live combina **8 indicadores clave** (técnicos, on-chain, sentimiento, interés minorista y macro) en una puntuación única de 0 a 100.  
Cada indicador se mide de 0 a 10 con la misma lógica:

- **10 = suelo del mercado → oportunidad de compra**
- **0 = techo del mercado → señal de venta**

El índice final es un promedio ponderado optimizado para detectar **suelos y techos de medio/largo plazo**, combinando señales de ciclo largo con indicadores intradía para mayor sensibilidad.

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
| **E** | EMA 200 semanal | 22% | 0 = precio > 2x EMA (extremo). 10 = precio < 0.5x EMA (extremo). | Velas semanales: Binance → Bybit → KuCoin → Kraken |
| **S** | Stablecoin Dominance | 20% | 0 = dominancia < 1.5% (euforia máxima). 10 = dominancia > 10% (miedo extremo). | CoinGecko (principal) → CoinPaprika (respaldo) |
| **C** | Pi Cycle Top | 15% | 0 = precio cerca/cruce SMA350×2 (techo). 10 = precio muy por debajo (suelo). | Velas diarias: Binance → Bybit → KuCoin → Kraken |
| **F** | Fear & Greed (SMA7) | 12% | 0 = codicia extrema (>80). 10 = miedo extremo (<20). | Alternative.me (principal) + RSI (respaldo) |
| **X** | DXY (Índice del Dólar) | 12% | 0 = DXY < 82 (dólar muy débil, techo). 10 = DXY > 115 (dólar muy fuerte, suelo). | Fórmula geométrica ICE USDX: Frankfurter → Exchangerate.fun → Open.er-api |
| **R** | RSI 14 diario | 7% | 0 = RSI > 80 (sobrecompra). 10 = RSI < 20 (sobreventa). | Velas diarias: Binance → Bybit → KuCoin → Kraken (suavizado Wilder) |
| **N** | Funding Rate | 7% | 0 = funding > +0.15% (euforia long). 10 = funding < -0.10% (pánico short). | Binance Futures (avg 24h, últimas 3 velas de 8h) |
| **W** | Wiki Pageviews (percentil 365d) | 5% | 0 = percentil >90% (atención extrema, techo). 10 = percentil <3% (desinterés, suelo). | Wikipedia API (principal) + F&G (respaldo) |
| 💰 | Precio BTC | (informativo) | — | Binance → CoinCap → CoinGecko (cada minuto) |

**Criterios de ponderación (100%):**
- Mayor peso a indicadores con mejor historial predictivo comprobado (EMA 200 semanal 22%, Stablecoin Dominance 20%, Pi Cycle 15%)
- Peso equilibrado para el DXY (12%) como variable macro independiente, y para Fear & Greed (12%) como indicador de sentimiento consolidado
- Peso moderado a RSI (7%) y Funding Rate (7%) como señales complementarias de extremos
- Peso ligero a Wiki Pageviews (5%) como indicador testimonial de interés minorista
- BTC Dominance eliminado por correlación inversa poco fiable en crashes sistémicos
- Ningún indicador individual supera el 22%, evitando sobrerrepresentación de una sola señal
- Balance por grupos funcionales: valoración de ciclo 49%, sentimiento 19%, on-chain 20%, interés minorista 12%

---

## 🔄 Frecuencia de actualización real

| Indicador | ¿Cada cuánto cambia realmente? |
|-----------|--------------------------------|
| C, R (velas diarias) | **1 vez al día** (cierre vela diaria ~00:00 UTC) |
| E (velas semanales) | **1 vez a la semana** (cierre vela semanal domingo) |
| F (Fear & Greed) | **1 vez al día** (Alternative.me actualiza cada 24h) |
| N (Funding Rate) | **Cada 8 horas** (liquidaciones de futuros perpetuos) |
| W (Wiki Pageviews) | **1 vez al día** (datos diarios de Wikipedia, actualización con 1-2 días de retraso) |
| X (DXY) | **1 vez al día** (las APIs de divisas gratuitas actualizan tras cierre de mercados) |
| S (Stablecoin Dom) | **Cada pocos minutos** (cambios en market cap en vivo) |
| Precio BTC | **Cada minuto** (consulta a exchanges) |
| Índice completo | **Recálculo cada 15 minutos** (con reintentos automáticos y respaldos si algún proveedor falla) |

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

Alternancia entre español e inglés mediante botón flotante con bandera 🇪🇸/🇬🇧. Traducción completa de la interfaz, indicadores, guías de estrategia y modales de ayuda.

## 🔔 Alertas del navegador

Botón en el panel izquierdo para activar notificaciones push automáticas cuando el índice entre en zona de compra (≥80) o venta (≤20). Requiere permiso del usuario.

## 📤 Compartir por X

Botón 𝕏 que genera una imagen del panel del índice y la comparte en X (Twitter) con un texto automático. En móviles usa la Web Share API nativa.

## 💰 Donación

Si el índice te resulta útil, puedes apoyar el proyecto:

- **On-chain:** `bc1qthc87aykdj2tjrxlqe7k9emz3txphrprm0scu6`
- **Lightning:** `ffg@cake.cash`

El botón `₿` abre un modal con QR y direcciones copiables.

---

## 🧰 Tecnologías utilizadas

- HTML5 + CSS3 (glassmorphism, animaciones, variables CSS, diseño responsive)
- JavaScript vanilla (fetch, async/await, cálculos de indicadores)
- Sin frameworks ni dependencias externas
- PWA con Service Worker para caché offline
- APIs públicas sin clave (Binance, Bybit, KuCoin, Kraken, CoinGecko, CoinPaprika, Alternative.me, Wikipedia, Frankfurter, ExchangeRate.fun, Open Exchange Rates)

---

## ⚠️ Descargo de responsabilidad

Este índice es una **herramienta educativa** basada en datos históricos.  
**No constituye asesoramiento financiero.** El rendimiento pasado no garantiza resultados futuros. Invierte solo lo que estés dispuesto a perder.

---

## 📄 Licencia

Código abierto bajo licencia MIT.  
Creado con ❤️ para la comunidad Bitcoin.