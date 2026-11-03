# 📊 Índice BTC-Live

**Índice macro de Bitcoin para acumulación y distribución a largo plazo.**

Índice BTC-Live publicado en Github Pages: https://zoki666.github.io/Indice-BTC-Live/

El Índice BTC-Live combina **7 indicadores clave** (técnicos, sentimiento, interés minorista y macro) en una puntuación única de 0 a 100.  
Cada indicador se mide de 0 a 10 con la misma lógica:

- **10 = suelo del mercado → oportunidad de compra**
- **0 = techo del mercado → señal de venta**

El índice final es un promedio ponderado optimizado para detectar **suelos y techos de medio/largo plazo**, combinando señales de ciclo largo con indicadores intradía para mayor sensibilidad.

---

## 🧭 Interpretación rápida

El índice detecta la **fase del mercado** (modo 🤖 Auto, por defecto) y ajusta los umbrales recomendados de compra y venta. También se puede forzar manualmente con el selector (📈 Alcista / ⚖️ Neutral / 📉 Bajista).

| Fase del mercado | Zona de compra (DCA) | Zona neutral | Zona de venta |
|------------------|----------------------|--------------|---------------|
| ⚖️ **Neutral / sin definir** | ≥ 75 | 26 – 74 | ≤ 25 |
| 📈 **Alcista** (compra en retrocesos) | ≥ 55 | 21 – 54 | ≤ 20 |
| 📉 **Bajista** (vender en rebotes) | ≥ 75 (capitulación real) | 41 – 74 | ≤ 40 |

### Detección automática de la fase

Se analizan las últimas **200 velas diarias**, divididas en 4 bloques de 50 días. Para cada par de bloques consecutivos se compara el máximo y el mínimo: cuenta como *creciente* (↑) o *decreciente* (↓) solo si cambia más de un 5%, para ignorar el ruido. Con `score = ↑ − ↓` (de −6 a +6):

- `score ≥ +3` → **alcista** (máximos y mínimos crecientes)
- `score ≤ −3` → **bajista** (máximos y mínimos decrecientes)
- en cualquier otro caso → **neutral** (hasta poder definirlo)

Los parámetros (`REGIME_DETECT`) y los umbrales (`REGIMES`) están al principio del script de `index.html`. Son valores orientativos, pendientes de validar con un backtest histórico. La elección del modo se guarda en el navegador y las alertas usan los umbrales de la fase activa.

---------------------|----------------------|--------------|------------------------------|
| ⚖️ **Neutral** (por defecto) | ≥ 75 | 26 – 74 | ≤ 25 |
| 📈 **Alcista** | ≥ 50 (compras en correcciones) | 26 – 49 | ≤ 25 |
| 📉 **Bajista** | ≥ 75 (capitulación real) | 46 – 74 | ≤ 45 (aprovechar rebotes) |

Los umbrales viven en la constante `REGIMES` de `index.html`. Son valores orientativos, pendientes de validar con un backtest histórico. La elección se guarda en el navegador y las alertas usan los umbrales de la lectura elegida.

-------|-------------|-------------------|
| **75 – 100** | Suelo / zona de acumulación | Compras DCA, aumentar exposición |
| **26 – 74** | Neutral | Mantener posición, cautela |
| **0 – 25** | Techo / zona de distribución | Vender parcialmente, proteger capital |

---

## 🧩 Indicadores incluidos

| Letra | Indicador | Peso | Lógica de puntuación (0=Techo, 10=Suelo) | Proveedores / Cálculo |
|-------|-----------|------|-------------------------------------------|------------------------|
| **X** | DXY (Índice del Dólar) | 10% | 0 = DXY ≤ 90 (dólar débil, techo). 10 = DXY ≥ 110 (dólar fuerte, suelo). Interpolación lineal. | Fórmula geométrica ICE USDX: Frankfurter → Exchangerate.fun → Open.er-api |
| **E** | EMA 200 semanal | 28% | 0 = precio ≥ 2.2× EMA (techo). 10 = precio ≤ 0.8× EMA (suelo). Escala logarítmica. | Velas semanales: Binance → Bybit → KuCoin → Kraken |
| **C** | Pi Cycle Top | 16% | 0 = SMA111 a ≤ 25% de la SMA350×2 (techo). 10 = distancia ≥ 65% (suelo). | Velas diarias: Binance → Bybit → KuCoin → Kraken |
| **F** | Fear & Greed (SMA7) | 18% | 0 = SMA7 ≥ 80 (codicia extrema). 10 = SMA7 ≤ 20 (miedo extremo). | Alternative.me (principal) + RSI (respaldo) |
| **R** | RSI 14 diario | 10% | 0 = RSI ≥ 80 (sobrecompra). 10 = RSI ≤ 25 (sobreventa). | Velas diarias: Binance → Bybit → KuCoin → Kraken (suavizado Wilder) |
| **N** | Funding Rate | 10% | 0 = funding ≥ +0.05% (euforia long). 5 = +0.01% (nivel base). 10 = funding ≤ -0.03% (pánico short). | Binance Futures (avg 24h, últimas 3 velas de 8h) |
| **W** | Wiki Pageviews (percentil 365d) | 8% | 0 = percentil ≥ 90 (atención extrema, techo). 10 = percentil ≤ 10 (desinterés, suelo). | Wikipedia API (principal) + F&G (respaldo) |
| 💰 | Precio BTC | (informativo) | — | Binance → CoinCap → CoinGecko (cada minuto) |

**Criterios de ponderación (100%):**
- Mayor peso a la valoración de ciclo (EMA 200 semanal 28%, Pi Cycle 16%) y al sentimiento (Fear & Greed 18%)
- DXY baja al 10%: es una variable macro de movimiento lento que casi no depende del ciclo propio de BTC y comprimía el índice hacia el centro
- RSI (10%) y Funding Rate (10%) como indicadores complementarios de extremos; Wiki Pageviews (8%) como indicador testimonial de interés minorista
- Escalas calibradas con los extremos realmente observados en los ciclos de BTC (no con extremos teóricos), para que cada indicador use su rango completo 0-10
- Ningún indicador individual supera el 28%
- Balance por grupos funcionales: macro (DXY) 10%, valoración de ciclo (E+C) 44%, sentimiento (F+N) 28%, momentum e interés minorista (R+W) 18%

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

Gracias a estos pasos podemos usarlo como una web.
---

## 🌗 Tema oscuro / claro

Botón flotante 🌙/☀️ para cambiar entre tema oscuro (por defecto) y claro. Preferencia guardada automáticamente.

## 🌐 Idiomas

Alternancia entre español e inglés mediante botón flotante con bandera 🇪🇸/🇬🇧. Traducción completa de la interfaz, indicadores, guías de estrategia y modales de ayuda.

## 🔔 Alertas del navegador

Botón en el panel izquierdo para activar notificaciones push automáticas cuando el índice entre en zona de compra o venta (según la lectura de mercado elegida). Requiere permiso del usuario.

## 📤 Compartir por X

Botón 𝕏 que genera una imagen del panel del índice y la comparte en X (Twitter) con un texto automático. En móviles usa la Web Share API nativa.

## 💰 Donación

Si el índice te resulta útil, puedes apoyar el proyecto:

- **On-chain:** `bc1qjh6txpqel5tanhd2y8ynyypl0rujalnn9j3fah`
- **Lightning:** `ffg@cake.cash`

El botón `₿` abre un modal con QR y direcciones copiables.

---

## 🧰 Tecnologías utilizadas

- HTML5 + CSS3 (glassmorphism, animaciones, variables CSS, diseño responsive)
- JavaScript vanilla (fetch, async/await, cálculos de indicadores)
- Sin frameworks ni dependencias externas
- PWA con Service Worker para caché offline
- APIs públicas sin clave (Binance, Bybit, KuCoin, Kraken, Alternative.me, Wikipedia, Frankfurter, ExchangeRate.fun, Open Exchange Rates)

---

## ⚠️ Descargo de responsabilidad

Este índice es una **herramienta educativa** basada en datos históricos.  
**No constituye asesoramiento financiero.** El rendimiento pasado no garantiza resultados futuros. Invierte solo lo que estés dispuesto a perder.

---

## 📄 Licencia

Código abierto bajo licencia MIT.  
Creado con ❤️ para la comunidad Bitcoin.